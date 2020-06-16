---
layout: post
title: '打点 API 和 bitsv 对数据上链的不同处理'
date: 2020-02-02 23:00:00
comments: true
status: public
categories: [BitcoinSV]
tags: 数据上链, BSV
glid: Bt-003-2002
---

## (2020.02) 数据上链：从 bitsv 到打点 API

可能是因为临近二月份创世纪升级，前段时间几个常用的外部服务都略有不稳。[小聪游戏](https://satoplay.com)用到的开源 bsv 库偶尔也会出现上链失败的情况。几次故障之后，我把数据上链方式由 [bitsv](https://github.com/AustEcon/bitsv) 换成了[打点开放平台的 API](https://developers.dotwallet.com/dev/doc)。

替换之后，果然稳定许多，再也没有出现因为 API 不可用而导致游戏分数上链失败的情况了。

然而，我们发现本来可以被 [https://trends.cash/ranking/](https://trends.cash/ranking/) 收录的 [satoplay.com](https://satoplay.com) 前缀变得无法识别了。在调查和解决这个问题的过程中，我对两个 API 的数据上链差异有了更多的了解。记录下来以备忘。 

## bitsv - send_op_return

[bitsv](https://github.com/AustEcon/bitsv) 提供了一个数据上链接口 [send_op_return](https://austecon.github.io/bitsv/guide/op_return.html#send-op-return)。这个接口接受一个由 bytes 组成的 list，内部处理了拼接的细节。使用的时候可以直接这样：

``` python
data_group = ['hello_001'.encode('utf-8'), 'world_002'.encode('utf-8')]
my_key.send_op_return(data_group)
```

这种情况下，`hello_001` 会被认为是合法的前缀而被收录，小聪游戏的 [satoplay.com](https://satoplay.com) 正是这样被识别的。

## 打点 API - pay_small_money (opreturn)

而情况在 [打点提供的 API](https://developers.dotwallet.com/dev/api/micropay) 这边则略有不同。

打点的 opreturn 参数是 string ，可以直接写入一般性的上链信息。而想要像上面那样区分出前缀，需要用到高级用法，也就是自己构造整个 op_return 脚本。这个脚本不复杂，甚至可以说是 bitcoin 脚本中最简单的类型，具体的结构是：

```
0 + OP_RETURN + PUSHDATAn + PUSHDATAn + PUSHDATAn + ...
```

其中每一段 PUSHDATAn 都有前缀： OP_PUSHDATA1/OP_PUSHDATA2/OP_PUSHDATA4 + 这段数据的长度，其中数据长度小于等于76个字符 (即 '0x4c'，也就是 OP_PUSHDATA1 的值) 时则无需指明 OP_PUSHDATAn。

## 为打点 API 完整构造一个 OP_RETURN 脚本

完整的代码逻辑见下：

``` python
OP_PUSHDATA1 = b'\x4c'
OP_PUSHDATA2 = b'\x4d'
OP_PUSHDATA4 = b'\x4e'

def get_op_pushdata_code(data):
    length_data = len(data)
    if length_data <= 0x4c:  # (https://en.bitcoin.it/wiki/Script)
        return length_data.to_bytes(1, byteorder='little')
    elif length_data <= 0xff:
        return OP_PUSHDATA1 + length_data.to_bytes(1, byteorder='little')  # OP_PUSHDATA1 format
    elif length_data <= 0xffff:
        return OP_PUSHDATA2 + length_data.to_bytes(2, byteorder='little')  # OP_PUSHDATA2 format
    else:
        return OP_PUSHDATA4 + length_data.to_bytes(4, byteorder='little')  # OP_PUSHDATA4 format

OP_0 = b'\x00'
OP_RETURN = b'\x6a'

def dot_opreturn_build_hex_str(content):
    bytes_list = []
    if isinstance(content, str):
        bytes_list = [content.encode('utf-8')]
    else:
        bytes_list = [x.encode('utf-8') for x in content]

    prefix = OP_0 + OP_RETURN
    pushdata = b''
    for data in bytes_list:
        pushdata += get_op_pushdata_code(data) + data
    return (prefix + pushdata).hex()
```

备注：

1. 上半部分 OP_PUSHDATAn 的获取是直接调用 bitsv 的逻辑
2. 下半部分里，我们判断了传入的是单个 string，还是多个 string 构成的 list 并分别处理

-------

后续小聪游戏平台进行 MetaNet 改造时，还会回来这里进一步拓展，目前就先这样吧。

（全文完）

- Gu Lu, 2020-02-02 于免成居 (公众号：**免成居**) 
- 本文遵循 [Creative Commons BY-NC-ND 4.0 许可协议](http://creativecommons.org/licenses/by-nc-nd/4.0/)。
- 永久链接 [https://gulu-dev.com/post/2020/2020-02-02-opreturn-of-dotapi-and-bitsv](https://gulu-dev.com/post/2020/2020-02-02-opreturn-of-dotapi-and-bitsv)
- 2020-06-16 新增编号 `Bt-003-2002` 并入库

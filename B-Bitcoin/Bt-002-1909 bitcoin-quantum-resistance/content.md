---
layout: post
title: '比特币的量子抵抗'
date: 2019-09-28 22:00:00
comments: true
status: public
categories: [Blockchain]
tags: Bitcoin, 量子计算
glid: Bt-002-1909
---

# (2019.09) 比特币的量子抵抗

![bitcoin-qr](bitcoin-qr.jpg)

前两天刷屏的 Google 量子计算，已被证明是新闻效应远大于实质的 breakthrough。目前所能知道的信息是，实际上并未很好地解决量子退相干（Quantum Decoherence），我们离可运行传统计算的量子计算机还有很远的路要走。但思考下比特币的量子抵抗能力，仍是有意义的。

看了下量子计算抵抗 (quantum-resistant, QR)，得出了以下几点 (待补充)

1. 从公钥弄出私钥是可能最先被破解的，但是到主公钥 (xpub) 本身信息量不足，目前可能性相对较低，到 seed 可能性也较低。
2. 一旦有了主公钥，再配合任意一个单个破解的私钥，可以推导出这个 xpub 下的所有私钥，这样虽然没得到 seed 效果也差不多了。
3. 更换新的 QR 签名算法的话，如果使用目前已知较好的 Lamport signature 每个签名至少长达若干 KB (目前长度的 40-170 倍)，所以不先充分扩容就不用谈了。

具体的安全实践：

1. 每个地址只使用 1 次，把公钥破解的性价比降到最低。
2. 对于大量的币，尽量均匀切分开，每个地址只存少量的币。
3. 不要在任何场合暴露自己的主公钥 (xpub) 一些离线冷钱包告诉你，可以在在线钱包里导入 xpub 来查看资金变动情况，不要这么做，如果你需要查询余额，直接查看具体的地址即可，不要在联网的机器上输入你的 xpub。

- [1] [https://en.bitcoin.it/wiki/Quantum_computing_and_Bitcoin](https://en.bitcoin.it/wiki/Quantum_computing_and_Bitcoin)
- [2] [https://bitcointalk.org/index.php?topic=5063390.0](https://bitcointalk.org/index.php?topic=5063390.0)
- [3] [https://en.wikipedia.org/wiki/Post-quantum_cryptography](https://en.wikipedia.org/wiki/Post-quantum_cryptography)
- [4] [https://en.wikipedia.org/wiki/Quantum_decoherence](https://en.wikipedia.org/wiki/Quantum_decoherence)

（全文完）

-----------------

- 2019-09-28 于免成居 (公众号：**免成居**) 
- 本文遵循 [Creative Commons BY-NC-ND 4.0 许可协议](http://creativecommons.org/licenses/by-nc-nd/4.0/)。
- 永久链接 [https://gulu-dev.com/post/2019/2019-09-28-bitcoin-quantum-resistance](https://gulu-dev.com/post/2019/2019-09-28-bitcoin-quantum-resistance)
- 2020-06-16 新增编号 `Bt-002-1909` 并入库

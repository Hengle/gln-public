---
layout: post
title: '2020.09 使用简易支付验证确保前序交易的签名有效性和交易完整性'
date: 2020-09-01 23:00:00
comments: true
status: public
categories: [Bitcoin]
tags: Bitcoin, BSV, SPV
num: Bt-005-2009
---

# 2020.09 使用简易支付验证确保前序交易的签名有效性和交易完整性

- Use SPV to validate the previous transaction signature integrity

本文起因是 Volt CTO 淘小杰同学在一篇文章中提出了签名有效性的问题，然后 nChain 的 Zhang Wei 老师特别为此写了一篇文章，说明了应利用 SPV 来校验前序交易。

## 淘小杰文中提出的问题

**创世升级后输入解锁脚本内签名不可靠问题** 

1. 创世升级后，很容易构造一个不含 'OP_CHECKSIG' 的锁定脚本并被矿工接受，这样矿工就不会验证解锁脚本内的签名是否有效，这样解锁脚本里的签名成了非强制性的。
2. 这个时候，如果在解锁脚本里伪造一个签名，同样能顺利完成交易。在这种情况下，就不能利用解锁脚本的签名来确认交易的发起者了。
3. 后果： MetaNet 和 Tokenized 都依赖输入脚本里的签名来确认所有权，因此会被此问题影响。

## 淘小杰文中提出的两个方案

- 方案1:  **向前回溯查询交易合法性**
    + 查询此交易所用到的所有 outpoints，确保这些 outpoints 都是有效且合法的交易。（Zhang Wei 文中提到的，这些前序交易需要使用 SPV 校验）
- 方案2:  **借用 op_return 单独存签名信息**
    + 构造一个仅包含签名的 OP_RETURN，注意这个签名不需要包含此 outpoint 的余额，因为余额部分有矿工校验，不会有问题。

## nChain 对此问题的看法

**前序交易必须要保证提供了有效的 output。** （这里的有效是指 **提供了针对特定公钥的数字签名**）

这么看是基于以下的假设：

- 从法律角度讲，数字签名具有法律约束力。（含有有效的数字签名，在法庭上是有效的证据）
- “当购买金额超过某一额度时，要求付款者提供可验证的身份证明。”是合情合理的需求

可以使用 SPV 来快速验证前序交易的存在及完整性。（也就是上述的解决方案1，不好之处按淘小杰的说法是多了 utxo 查询的工作，好处是在 bitcoin 框架内，无需引入新的协议或经由 op_return 的 hack）

## nChain 文中关于 SPV 的其他信息

SPV 核心过程：假设验证者可以访问区块头列表，以及一笔比特币交易的数据和这笔交易的Merkle Proof，而且通过这个Merkle Proof推导出Merkle root出现在某个区块头中，那么这就能证明这笔交易的确已被纳入了该区块头对应的区块中。

这个验证之所以被认为是“简易”的，是因为整个过程只需要三样信息：

- 区块头列表（截至目前，这个列表只有52MB）；
- 一笔交易的完整数据（对于支付至公钥哈希P2PKH的简单交易（脚注1）来说，这个数据不到400字节）；
- 一个Merkle Proof（即使一个区块包括10亿笔交易，这个Merkle Proof也仅有928字节）

当某些场景中需特别使用到解锁脚本中的数字签名和公钥时，前序交易的完整性，或者更准确地说，前序交易中锁定脚本的完整性就变得极其重要。完整性证明确保了解锁脚本中的数字签名和特定公钥会在比特币网络中被有效验证。如上所述，这完整性证明可以通过对前序交易进行简易支付验证来实现。

SPV不仅可以用于证明已发布交易的存在性，而且还可以用于证明交易的完整性，而交易的完整性就意味着该交易中的任何数据的完整性。

## 相关链接

- [淘小杰 Bitcoin identity issue](https://www.yuque.com/docs/share/0b224413-7987-4ebf-b0e3-6b268ae18f27)
- [Wei Zhang Simplified Payment Verification Instant payment, signature validity, and the importance of integrity (en)](https://medium.com/nchain/simplified-payment-verification-48ac60f1b26c)
- [Wei Zhang 简易支付验证：即时支付、签名的有效性和交易的完整性 (cn)](https://blog.csdn.net/BitcoinSV/article/details/108276783)

[完]  

----------

- 顾露 (Gu Lu) 于免成居
- 时间: 2020-09-01
- 编号: Bt-005-2009
- 本文遵循 [Creative Commons BY-NC-ND 4.0 许可协议](http://creativecommons.org/licenses/by-nc-nd/4.0/)。
- 永久链接 [https://gulu-dev.com/post/2020/2020-09-01-use-spv-for-previous-tx-validation](https://gulu-dev.com/post/2020/2020-09-01-use-spv-for-previous-tx-validation)

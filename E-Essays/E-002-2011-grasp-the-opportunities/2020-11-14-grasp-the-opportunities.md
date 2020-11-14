+++
title = "2020.11 抓住机会"
date = "2020-11-14"
description = ""
featured = false
tags = [ "2020", "随笔" ]
categories = [ "Essays" ]
aliases = ["2020-11-14-grasp-the-opportunities"]
thumbnail = "images/apple.svg"
+++

注：本文以彩云小译的输出为主。费解之处请[参考原文](https://fabiensanglard.net/silicone/index.html)。 

本文与 2014.03 发在 blog 上的 [不要说谎 (Don't Lie.)](https://gulu-dev.com/post/2014-03-22-dont-lie) 正好组成了一组文章，相互呼应。

“不要说谎” 一文主要的着眼点在于，**项目开发中的历次迭代（在任何时候）都不应打破产品的质量标准。** 而本文则指出，那些无法维持标准的产品会 **因为退化** 而给新的产品带来机会。

<!--more-->

## 这些就是所谓的机会 (These are called opportunities)

昨天苹果公司更新了他们的三款机器。在发布会上，据说 MacBook Air、 MacBook Pro 和 Mac Mini 将采用自研的 M1 芯片。这些“One more thing...”事件通常伴随着夸张的数字，这一次并没有偏离传统。

- 高达3.9倍的视频处理速度。
- 高达7.1倍的图像处理速度。
- 高达3.5倍更快的 CPU 性能。
- 每瓦CPU效能功耗比提升至3倍。
- 高达2倍的图形处理器性能。
- 更快的机器学习性能高达15倍。
- 高达2倍速度的固态硬盘。
- 速度超过 98% 的 PC 笔记本电脑。

如果觉得最后一个说法难以置信 <sup id="a1">[1](#f1)</sup>，Geekbench 展示了一款 ARM MacBook Air 2020，这让英特尔 MacBook Pro 2019在单核性能上相形见绌 <sup id="a2">[2](#f2)</sup>。可以肯定的是，这些新的笔记本电脑提供了很大的性能提升。

## 前进一步，后退两步

结构更迭和性能提升确实让人印象深刻，不过这里也许有个情况。

在接下来的几个月里，那些购买 M1 机器的人将享受到强大的响应能力和迅速的启动时间。一些曾经臃肿的应用程序将再次像大多数工具那样运行。但是很快这些指标就会开始下降。响应能力和启动时间将逐渐恢复到以前的状态，老的“非 m1”机器将变得比以前更慢。

对于硬件工程师节省的每个周期，软件工程师将增加两条指令 <sup id="a3">[3](#f3)</sup>。

我对这个问题最清晰的记忆是在2008年，当时我用 ssd 替换了我的 hdd。它改变了我的生活，所以我写了这篇文章 <sup id="a4">[4](#f4)</sup>，这样读我博客的五个人也可以改变他们的生活。 Photoshop 在一秒钟内就开始了。可以立即启动 XCode。那真是太美妙了。

10年后，一台有着 M.2 NVMe 和 Ryzen 5 2600 的机器需要13秒来启动 Photoshop。我也不再使用 XCode 了。

## 有人在乎吗？

做更多的事情需要更多的资源，这很正常。现代的射线跟踪器需要更大的处理能力，来产生更好的图像。同样，2020年的编译器拥有令人敬畏的静态代码分析器，这是他们在2009年没有的。

但是做同样的事情永远不应该变慢。启动一个应用程序不应该比以前花费更长的时间。如果一个特性要花费启动时间，我宁愿不要它。

是因为我们不在乎启动时间，还是因为我们别无选择？

## 我昨天就想要

早在2008年，当我亲眼目睹第二次浏览器大战时，火狐从网景公司的灰烬中崛起，对 Internet Explorer 进行报复，谷歌发布了一款新的浏览器。

火狐有很多很棒的功能。它有选项卡、调试工具和常规的 bug 修复等大量有用的功能。 Chrome 也有这些功能。但是当我看到它几乎立即启动，而不是像火狐那样花上5秒钟(才启动)的时候，我立刻换了它，再也没有回头。

正如后来谷歌工程师解释的那样，速度是核心优先考虑的事情。


> 我们使用自动化测试来仔细监视启动性能，该测试几乎对代码的每个更改都运行。这个测试是在项目很早的时候创建的，当时谷歌 Chrome 几乎什么功能都还没开始做。我们一直遵循一个非常简单的规则:  
> 
> 这个测试的指标不能退化。  
> 
> 因为在出现性能问题时立刻处理它们，比拖到以后再修复它们要容易得多，所以我们可以很快地修复或回滚任何的（有问题的）改动。因此，我们这个（已经变得）非常大的应用程序，现在启动的速度和我们开始时使用的非常轻量级的应用程序一样快。  
> 
> -- Brett Wilson，Chrome 软件工程师 <sup id="a5">[5](#f5)</sup>

一旦行动迟缓，就很难走出泥潭，让人们重新审视自己。众所周知，Firefox 开发者在2010年试图通过 bug # 627591 修复（长达5秒的）启动时间问题 <sup id="a6">[6](#f6)</sup>。他们可能解决了许多问题，但这也不再能唤起我第二次尝试的勇气了。

## 机会

有了像苹果这样更好的硬件，创造者们大多能得到更好的工具。一些（不那么好的）公司的工程质量会降低，或者不再进行这类 “确保系统不会退化的测试” ，但即使这样也是一件好事。因为对有些人来说，这些缺陷有另一个名字。这些就是 **所谓的机会** (These are called opportunities)。

## 参考文献

- <b id="f1">1. </b> [No, the new MacBook Air is not faster than 98% of PC laptops](https://www.pcworld.com/article/3596814/no-the-new-macbook-air-is-not-faster-than-98-of-pc-laptops.html) [↩](#a1)
- <b id="f2">2. </b> [MacBook Pro (16-inch Late 2019) vs MacBookAir10,1](https://browser.geekbench.com/v5/cpu/compare/4651583?baseline=4651916) [↩](#a2)
- <b id="f3">3. </b> [Andy and Bill's law](https://en.wikipedia.org/wiki/Andy_and_Bill%27s_law) [↩](#a3)
- <b id="f4">4. </b> [SSD Reboot your thing](https://fabiensanglard.net/ssd/) [↩](#a4)
- <b id="f5">5. </b> [I/O in Google Chrome](https://blog.chromium.org/2008/10/io-in-google-chrome.html) [↩](#a5)
- <b id="f6">6. </b> [Bug: preload dlls on windows](https://bugzilla.mozilla.org/show_bug.cgi?id=627591) [↩](#a6)

----------

- [留言点这里](https://gitee.com/gu-lu/blog-comments/issues)

----------

- 顾露 (Gu Lu) 于免成居
- 时间: 2020-11-14
- 编号: E-002-2011 ([Gu Lu's Public Writings](https://github.com/gl-notes/gln-public))
- 协议: [Creative Commons BY-NC-ND 4.0](http://creativecommons.org/licenses/by-nc-nd/4.0/)。

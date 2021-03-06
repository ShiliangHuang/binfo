---
title: 什么是 ASIC 挖矿?
---

ASIC 的全称是 Application-Specific Integrated Circuit 指的是专门设计来完成特定计算任务的集成电路。在区块链领域用 ASIC 来进行挖矿是非常常见的，本文来分析一下 ASIC 挖矿的原理以及为何要反 ASIC 。

## ASIC 的基本原理

先来聊聊 ASIC 的基本原理，看看为何用 ASIC 挖矿能有大幅度的效率提升。

挖矿过程的本质是很多机器去竞赛谁可以先算出一道复杂数学问题的答案。对于比特币来说，解决这个数学问题就是看谁可以在单位时间内完成更多次的 SHA256 运算。所以说优化 SHA256 的计算时间，就可以提升挖矿效率。

![](https://img.haoqicat.com/2019071601.jpg)

CPU 去运算一个数学问题是通过编程思路来解决的。CPU 面向的是通用的计算任务，所以硬件层面上只能去完成加法或者乘法这样的基础运算。所以要完成一个复杂运算，例如 `A*B + C` ，就需要多个运算操作，要耗时多个时钟周期才能完成。但是如果开发一种集成电路，使得可以在硬件层面上直接完成 `A*B + C` 的操作，那么执行这个运算就只需要一个计算操作，消耗一个时钟周期了。这样的集成电路的特点是不再具有通用型，但是完成特定任务是效率却奇高，这就是所谓的 ASIC 了。SHA256 运算比上面的先乘后加操作要复杂，但是道理是一样的。

对应比特币来说，挖矿就经历了 CPU ，GPU ，FPGA 和 ASIC 四个阶段。GPU 天生的特点是适合并行简单运算，所以执行 SHA256 要比 CPU 高很多。FPGA 是有可编程性的硬件，因为本身还是有一定的通用性的，所以单价会比较贵。ASIC 初期设计投入大，但是量产后单价就会比较便宜。所以，如果能够确定市场规模比较大，使用 ASIC 技术，经济上会最为划算。

这就是 ASIC 的基本原理了。

## 反 ASIC 的算法

ASIC 由于早期投入太大，所以很容易造成挖矿的中心化问题，于是区块链领域一直没有停下对反 ASIC 的挖矿算法的研究。

Bitcoin 的挖矿哈希算法 SHA256 本身其实是对 ASIC 非常友好的。因为 SHA256 属于传统的密码学原语，主要用来进行签名摘要等传统运算，并不是为挖矿这个任务专门来设计的，也没有任何对抗 ASIC 的考虑，所以制作 ASIC 矿机非常方便，可以获得千倍的效率提升。

Zcash 使用的挖矿算法是 Equihash ，ASIC 实现起来就比较难了，但是真的实现后，依然可以提升一百倍的挖矿效率。底层的原理是，挖矿的时候需要存储150M 的状态数据，那么即使实现 ASIC 芯片之后，也要承受这150M的存储成本，所以效率提升就没有那么明显了，但是百倍还是没有问题。

门罗币使用的挖矿算法是 CryptoNight ，ASIC 实现就更困难了。因为算法本身的复杂度很高，实现到硬件层面上也会依然很复杂，成本也就相对比较高。同时需要2M的状态存储，这个对于普通 CPU 来说是友好的，因为刚好可以存下，但是实现到 ASIC 上，也部分成本依然存在。所以总的效果是只能有50倍的效率提升。

以太坊使用的 ETHash 是对 ASIC 极端不友好的，所以到目前为止也没有人有动力去研发以太坊的矿机。底层原理主要是有巨量的数据需要存储。但是计算方面依然可以通过硬件化来提升效率。总体上，如果实现成 ASIC 来挖矿，效率还是能提升一倍的。

所以总结起来，反 ASIC 的挖矿算法的实现起来主要有两种思路：第一，增大数据存储量，因为 ASIC 主要是压缩计算步骤，对存储来说依然是要有对应的规模的硬件去存的，优化空间不大。第二，增加计算步骤的复杂度，可以把计算步骤设计的对很难去用硬件优化，甚至有 ProgPOW 这样的算法，专门针对主流 GPU 的硬件去设计非常复杂的计算步骤，而且算法是动态可调整的，所以如果把算法固化到硬件上，一旦算法变了，这样硬件就失效了。这样导致实现 ASIC 的时候也必须把硬件功能做的很通用，也就是跟一个通用的 GPU 很像了，所以成本就非常高，还不如直接买大厂商的 GPU 去挖矿合算。

## 反 ASIC 真的有意义吗？

最后一部分，咱们思考一个问题：反 ASIC 真的有意义吗？

首先，ASIC 厂商其实跟区块链是利益共同体。以 ProgPOW 为例，也有意见认为 ProgPOW 会把挖矿绑定到少数机构大显卡厂商身上，这样做的安全性真的比依托 ASIC 厂商安全度更高吗？要知道 ASIC 厂商的利益是跟币价深度并且长期绑定的，而大 GPU 厂商就不是，所以如果攻击某种币是有利可图的，通用 GPU 厂商不会在乎对某种币的长期声誉影响，所以攻击动机更充分。

第二，挖矿本身还是比较复杂的一项工作，所以专业化是不可避免的趋势。矿机角度总有可以优化的空间，另外大矿池可以统一把机器都搬到电力比较便宜的偏远地区，这些事情都是散户矿工很难做到的。

第三，挖矿从一个侧面来讲，就是烧钱，不管用什么硬件挖，只要有钱，都可以一下子购置很多。

所以说，反 ASIC 的意义是值得思考的。不过目前很多人认为，起码在一条区块链的启动阶段，如果有人投巨资设计了 ASIC 去挖这条链，会让这条链的持币变得非常中心化，这显然是不好的，所以早期考虑反 ASIC 是有意义的。

## 总结

关于 ASIC 挖矿的内容，就介绍这些了。总结一下。首先，ASIC 主要是用硬件的方式来压缩挖矿运算需要的计算步骤来获得效率提升的，但是如果运算本身是需要大量数据存储的，可优化空间就不大了。第二，反 ASIC 的意义可能主要体现在区块链的启动阶段。

参考：

- https://www.youtube.com/watch?v=vdvkkoR4oFk
- https://en.bitcoin.it/wiki/ASIC

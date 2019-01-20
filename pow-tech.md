---
title: POW 的技术细节
---

比特币系统有一个众所周知的特点，就是很多矿工参与挖矿，但是每十分钟网络上产生的比特币却不是给所有矿工均分的，而是谁抢到记账权，就把所有的比特币奖励给谁。而抢到记账权需要的是进行运算能力的比拼，也就是说哪个矿工的机器速度更快，那他就更有可能跑赢这次算力赛跑，从而拿到记账权。本节我们就一起探索一下这个赛跑背后的 POW 机制。换句话说，就是看看大家是怎么知道哪台计算机的运算能力是最强的。

## POW 本意

POW 这个概念是1993年的时候提出的，要比比特币出现得早。最早的用途也不是实现加密货币的，而是用来防止垃圾邮件。所以我们先说说 POW 自身的基本含义。

POW ，英文全称是 Proof of Work ，直接翻译过来是工作量证明。这个词的中文直接听起来有点不知所云。实际上如果我跟你说结婚证明，离职证明，那你是不是首先想到的是一张上面印着一些东西的纸呢？别人看到这张纸就知道你的确结婚了，或者你的确从某单位离职了。工作量证明从语法上也是一个逻辑，也可以理解成一张纸，通过这张纸就可以证明你的确完成了一定量的工作。这就是工作量证明的字面意思。

那工作量证明有什么特点呢？我们抛开计算机，用现实世界的例子来说明。例如我上课不认真，老师罚我把《桃花源记》抄写十遍，我用了两个小时的劳动，最后给老师的就是一张纸，而老师要确认我的确付出了大量劳动，其实只需要看一眼就可以了。这个例子道出了 POW 机制的一大特点，那就是生成需要花费大量劳动，但是验证只需一瞬间。另外一个工作量证明的例子可以是，老师给我出一道题，我给老师的运算结果，或者说就是最后的那个数字，就是我的工作量证明。回到计算机情形下，纸当然是不存在的，所以所谓的工作量证明就是花费了很多劳动而得到的[一个数](nonce)了。

再说说 POW 最早的用途。人们在使用电子邮件的时候会收到垃圾邮件的骚扰。如果没有成本，那么发送一百万封邮件的确是很轻松的事情了。所以，聪明的人就会想，如果让每一封邮件发送时候，都有一个微小的成本，那么垃圾邮件就会被很大程度的遏制了。而 POW 就是为了服务这个目的产生的。基本过程就是邮件接收方会先广播一道题出去，邮件发送方发邮件的时候必须附带上这道题的答案，这样邮件才会被接受，否则就会被认为是垃圾邮件。

这样我们就理解了 POW 的最基本的含义了。

## 哈希函数

但是我们知道，计算机解题速度很快，人类觉得很难的题，计算机根本就不用花什么时间就能给出答案。所以什么样的题才能让计算机形成工作压力呢？这就要说到哈希函数了。

哈希函数，也有人翻译为散列函数，是一个公开的算法。输入可以是任意长度的数据，算法拿到输入之后，把数据拆散，然后重新排列，得到的输出是一个位数固定的数字，这个数字就叫做哈希值，简称哈希。哈希函数最大的特点是，如果输入的数据不同，哪怕只有一个微小的差异，那么输出结果也会看起来完全不同。这个特点保证了，根据输出结果去反向运算输入是不可能的，甚至也没有办法去缩小输入的可能值范围。另一方面，如果输入相同，那么运算得到的哈希也一定相同。这一点保证了任何人都可以在一瞬间内验证最终的哈希值是否正确。

哈希函数的这些特点，决定了很多场合下都可能用到哈希。例如可以用哈希值作为一个数据指纹，给定一个确定的哈希，就可以判定原来的数据有没有被篡改过。不过，这些其他用途都不是这次要关心的，我们重点来看看哈希在 POW 机制下的作用，或者说就是如何用哈希函数来给计算机出题。

比特币中的 POW
比特币的 POW 机制，宏观上要达成的就是判定哪个矿工的运算能力最强。系统会给所有的矿工出一道题，哪个矿工最早提交答案，也就是提交 POW，系统就可以判定这个矿工的算力是最强的，就会把记账权给他。

这道题用到了哈希函数，但是非常有意思的是，系统要的答题结果，也就是所谓的 POW，不是哈希函数的输出，而是输入。因为要从输入算输出，这是一个非常直白的过程，计算机很快就会完成，同时出题的时候也需要给全网广播一个超级大的数据，考虑到网速，这样显然是不可行的。所以比特币系统的做法是反过来，给全网广播一个哈希值，让大家去找到它的输入。因为哈希函数本身其实是不能进行反向运算的，所以如果矿工们要去得到输入，唯一的做法就是去瞎蒙，类似于去掷骰子，每次选一个数，运算它的输出是否符合系统给的哈希值。如果不是，就换下一个数再试。最终谁能找到这个输入，显然是一个概率问题，但是哪个矿工的运算能力强，也就意味着单位时间内他掷骰子的次数就多，所以大概率上肯定是他会首先拿到正确的输入。这就是运算 POW 的基本原理了。

当然实际中，比特币系统是每十分钟会记账一次，也就需要大家每十分钟就比一次。而十分钟之内想要给定一个精确的哈希值，让大家拿到输入，是根本不可能的。所以其实每次系统给定的是一个哈希值范围。具体规则就是，只要可以保证运算出的哈希值小于某个特定数值，就认为提交的 POW 是正确的。这也就意味着，矿工要去拼命找到一个输入，让它对应的哈希值的前面几位都是0，因为0越多，数值就越小。同时，系统如果要求的0越多，那么对应的运算难度就会越大。比特币矿工们的算力多年来提高了很多，但是为何比特币系统还是能保证算出 POW 的时间大致保证在十分钟左右呢？秘密就是系统可以通过调整0的个数，来改变出题难度，算力高，但是题变难，所以需要花费的解题时间就会保持相对稳定。矿工得到结果之后，会把自己的结果提交给全网，因为哈希函数的特点，每个矿工都会很容易的验证这个结果是符合系统要求的，于是大家就会承认这个矿工抢到了记账权。

这样，我们就理解了比特币系统是如何用 POW 机制，给矿工铺开了一条算力赛跑的跑道了。

总结
这节中我们讲 POW，介绍了 POW 的本意，哈希算法的特征，最后介绍了比特币系统中如何通过一个难度可控的反向哈希运算的数学题，来判定哪个矿工的运算能力最强。这样，对于 POW 机制，我们就有了比较清晰的了解。但是，站在更高的角度，比特币如何通过 POW 机制来达成共识，进行防欺诈，似乎不是我们目前这些知识能够充分解释的，需要涉及到时间戳机制和最长链原则等更多的细节，Peter 会在后续内容中继续为大家介绍，敬请关注。
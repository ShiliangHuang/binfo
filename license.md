---
title: 如何为自己的 Github 项目选择 License?
---

Github 官方专门制作了一个网站 https://choosealicense.com/ 帮助大家选择合适的开源，License。中文版也有 http://choosealicense.online/ 。这里我对这些如果选择 Github 项目的 License ，给出一些具体的操作建议。

## 可不可以不选择 License ？

没有 License 的内容是默认会被版权保护。所以如果你想要的是让大家都放心使用，就需要选择一个合适的 License ，只有这样才能赋予任何人使用，分享和修改这个软件的权力。

所以，如果你只是想奉献爱心，想让大家无限制的使用自己仓库的代码，选择 MIT 协议即可 https://choosealicense.com/licenses/mit/ 。MIT License 是一个宽松的 License ，允许别人用你的代码做任何事情，但必须保证你的所有权，并且你无须承担代码使用产生的风险。

## 具体选择标准

开源 License 很多，https://choosealicense.com/licenses/ ，具体的差别可以看一下下面这个图。

![](https://img.haoqicat.com/2018113001.jpg)

总结一下，MIT 最自由，简直就是没有任何限制，任何人都可以售卖我的软件，甚至可以用我的名字促销。BSD 和 Apache 协议也很自由，跟 MIT 的区别分别是不允许用作者本人名义促销和保护作者版权。GPL 可以说最霸道，对代码的修改部分也必须是 GPL 的，同时基于 GPL 代码而开发的代码也必须按照 GPL 发布，而 MPL ，也就是 Mozilla Public License 就温和一些，如果后续开发的代码中添加了新文件，同时新文件中也没有用到原来的代码，那么新文件可以不必继续沿用 MPL 。

这就是几个常见 License 的核心差异了。

## GPL 家族

GPL 是最著名的开源 License，没有之一。目前在 Github 创建项目的时候，一共有12个备选 License ，其中5个都是 GPL 家族的。

人们对 GPL 感情是复杂的。激进的人会比较喜欢 GPL ，因为它要求任何人修改了软件后，修改后的内容也必须开源。但是商业公司有时候会非常有顾虑，因为 GPL 有病毒性，一旦公司使用了 GPL 的代码，那么自己辛辛苦苦做出的修改内容也必须要通过 GPL 开源，让竞争对手也可以直接拿来用，很难形成竞争壁垒。

GPL 协议也发展出了很多分支，其中 GPL v3 是最为激进的，基本上跟原始代码沾点边的代码就必须也得是 GPL 的，例如，最极端的，如果我的代码调用了 GPL 的库，那么我的代码就必须是 GPL 的。这基本意味着如果我是一个商业软件系统，那么我就没有权利使用 GPL v3 的代码了。v3 的背后是 GPL 之父 Richard Stallman 不断在宣传推进，代表了开源激进派的最前沿。而其他的 GPL 版本可以说都是略微温和版的 GPL ，例如 Linux 项目的 GPL v2 ，也是 Richard 自己写的，由于发布的早，所以很多问题他没有考虑都，所以让商业运用有了一些空间。另外还有 GNU Lesser General Public License ，GNU较宽松通用公共许可证
，看名字就知道是比较温和的了。

这就是 GPL 的基本情况了。关于 GPL 可以专门写一本《GPL 传奇》了，我们这里不展开，大家可以去 gnu.org 学习或者听一下 Richard Stallman 的演讲。

## 总结

关于，在 Github 使用开源 license ，还有其他一些要注意的地方，例如 license 要存放到哪个文件中，如果按照协议类似搜索项目等，这些内容可以参考官方文档 https://help.github.com/articles/licensing-a-repository/ 。另外，如果项目内容不是代码，而是书稿或者其他作品，可以参考这里的说明 http://choosealicense.online/non-software/ 使用 CC License 。

参考：

- http://www.ruanyifeng.com/blog/2011/05/how_to_choose_free_software_licenses.html
- https://help.github.com/articles/licensing-a-repository/

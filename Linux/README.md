# Linux 教程

## 历史

原文链接：https://en.wikipedia.org/wiki/Linux

### 简介

Linux是一个基于Linux内核的开源类Unix操作系统家族。

这个操作系统的内核由 Linus Torvalds 于 1991 年 9 月 17 日发布。 

wiki链接：https://en.wikipedia.org/wiki/Linus_Torvalds

百度链接：

Linux 通常被打包为 Linux 发行版（distro），其中包括内核以及支持系统软件和库，其中许多是由GNU 项目。许多Linux发行版的名称中都使用“Linux”一词，但自由软件基金会使用并推荐名称“GNU/Linux”来强调GNU软件在许多发行版中的使用和重要性。

流行的 Linux 发行版，包括 Debian、Fedora Linux、Arch Linux 和 Ubuntu。商业发行版包括 Red Hat Enterprise Linux 和 SUSE Linux Enterprise。桌面 Linux 发行版包括 X11 或 Wayland 等窗口系统以及 GNOME 或 KDE Plasma 等桌面环境。用于服务器的发行版可能根本没有图形用户界面，或者包括 LAMP 等解决方案堆栈。由于 Linux 是可自由再发行的，因此任何人都可以出于任何目的创建发行版。

Linux 最初是为基于 Intel x86 架构的个人计算机开发的，但后来被移植到比任何其他操作系统更多的平台上。由于基于 Linux 的 Android 在智能手机上占据主导地位，截至 2022 年 5 月，Linux（包括 Android）在所有通用操作系统中拥有最大的安装基数。尽管截至 2022 年 11 月，只有约 2.6% 的台式电脑使用 Linux。

Chromebook 运行基于 Linux 内核的 ChromeOS，在美国 K-12 教育市场占据主导地位，占美国 300 美元以下笔记本电脑销量的近 20%。

Linux 是服务器上领先的操作系统（排名前 100 万的 Web 服务器操作系统中超过 96.4% 是 Linux），领先于大型机、并被用于全球所有最快的 500 台超级计算机（截至 2017 年 11 月，已逐渐取代所有竞争对手）。

Linux 还可以在嵌入式系统上运行，即操作系统通常内置于固件中并且针对系统进行高度定制的设备。这包括路由器、自动化控制、智能家居设备、视频游戏机、电视（三星和 LG 智能电视）、和航天器（猎鹰 9 号火箭、龙飞船和毅力号火星车）。 

Linux 是自由和开源软件协作最突出的例子之一。任何人都可以根据其各自许可证的条款（例如 GNU 通用公共许可证 (GPL)）以商业或非商业方式使用、修改和分发源代码。例如，Linux 内核根据 GPLv2 获得许可，但系统调用除外，该系统调用允许通过系统调用调用内核的代码不在 GPL 下获得许可。

### Precursors 前身

Unix 操作系统于 1969 年在美国 AT&T 贝尔实验室由 Ken Thompson、Dennis Ritchie、Douglas McIlroy 和 Joe Ossanna 构思并实施。Unix 于 1971 年首次发布，完全用汇编语言编写，这在当时是常见的做法。 1973 年，丹尼斯·里奇 (Dennis Ritchie) 采用 C 编程语言重写了它（除了一些硬件和 I/O 例程）。 Unix 高级语言实现的可用性使其更容易移植到不同的计算机平台。

由于早期的反垄断案件禁止其进入计算机业务，AT&T 将操作系统的源代码作为商业秘密授权给任何提出要求的人。结果，Unix 迅速发展并被学术机构和企业广泛采用。 1984年，AT&T剥离了其区域运营公司，并免除了不进入计算机业务的义务；由于摆脱了这一义务，贝尔实验室开始将 Unix 作为专有产品销售，法律上不允许用户对其进行修改。

Onyx Systems 于 1980 年开始销售早期基于微型计算机的 Unix 工作站。后来，作为斯坦福大学学生项目的衍生公司而成立的 Sun Microsystems 也于 1982 年开始销售基于 Unix 的桌面工作站。虽然 Sun 工作站不使用商品Linux 最初是为 PC 硬件开发的，它代表了首次成功的商业尝试，即分发运行 Unix 操作系统的单用户微型计算机。

随着 Unix 越来越“锁定”为专有产品，Richard Stallman 于 1983 年启动的 GNU 项目的目标是创建一个完全由自由软件组成的“完整的 Unix 兼容软件系统”。工作开始于 1984 年。后来，在 1985 年，斯托曼创立了自由软件基金会，并于 1989 年编写了 GNU 通用公共许可证 (GNU GPL)。到 20 世纪 90 年代初期，运行中所需的许多程序系统（例如库、编译器、文本编辑器、命令行 shell 和窗口系统）已经完成，尽管设备驱动程序、守护进程和称为 GNU Hurd 的内核等低级元素已停滞且不完整。

MINIX 由计算机科学教授 Andrew S. Tanenbaum 创建，于 1987 年发布，作为一个最小的类 Unix 操作系统，面向学生和其他想要学习操作系统原理的人。尽管 MINIX 的完整源代码可以免费获得，但许可条款使其无法成为自由软件，直到 2000 年 4 月许可发生变化。

尽管由于法律上的复杂性，386BSD（NetBSD、OpenBSD 和 FreeBSD 的前身）直到 1992 年才发布，但它的发展早于 Linux。 Linus Torvalds 在不同场合表示，如果当时（1991 年）GNU 内核或 386BSD 已经可用，他可能就不会创建 Linux。

### Creation 创建

1990 年秋天，在赫尔辛基大学就读时，Torvalds 报名参加了 Unix 课程。该课程使用运行 Ultrix 的 MicroVAX 小型计算机，所需课本之一是 Andrew S. Tanenbaum 的《操作系统：设计与实现》。这本教科书包含一份 Tanenbaum 的 MINIX 操作系统。正是通过这门课程，Torvalds 第一次接触了 Unix。 1991年，他对操作系统产生了好奇。由于对 MINIX 的许可感到沮丧，当时该许可仅限于教育用途，他开始研究自己的操作系统内核，最终成为 Linux 内核。

1991 年 7 月 3 日，为了实现 Unix 系统调用，Linus Torvalds 试图向 comp.os.minix 新闻组请求获取 POSIX 标准文档的数字副本，但没有成功。在找不到 POSIX 文档后，Torvalds 最初从该大学拥有的 SunOS 文档中确定系统调用，以用于操作其 Sun Microsystems 服务器。他还从 Tanenbaum 的 MINIX 文本中学到了一些系统调用。

Torvalds 开始在 MINIX 上开发 Linux 内核，为 MINIX 编写的应用程序也在 Linux 上使用。后来，Linux 逐渐成熟，在 Linux 系统上进行了进一步的 Linux 内核开发。GNU 应用程序还取代了所有 MINIX 组件，因为在刚刚起步的操作系统中使用来自 GNU 项目的免费代码是有利的；根据 GNU GPL 许可的代码可以在其他计算机程序中重复使用，只要它们也是在相同或兼容的许可证下发布的。 Torvalds 发起将其原始许可证（禁止商业再分发）转换为 GNU GPL。开发人员致力于将 GNU 组件与 Linux 内核集成，创建一个功能齐全且免费的操作系统。

### Naming 命名

Linus Torvalds 曾想将他的发明称为“Freax”，这是“free”、“freak”和“x”（暗指 Unix）的合成词。在他开始从事该系统的工作期间，该项目的一些 makefile 包含“Freax”这个名称大约有半年时间。最初，托瓦兹考虑使用“Linux”这个名字，但认为它太自负了。

为了方便开发，这些文件于 1991 年 9 月上传到 FUNET 的 FTP 服务器 ( ftp.funet.fi )。 Ari Lemmke，Torvalds 在赫尔辛基科技大学 (HUT) 的同事，也是该项目的志愿者管理员之一。当时的 FTP 服务器，并不认为“Freax”是一个好名字，因此他在没有咨询 Torvalds 的情况下将服务器上的项目命名为“Linux”。然而，后来 Torvalds 同意使用“Linux”

根据 Torvalds 的新闻组帖子，单词“Linux”的发音应为 ( /ˈlɪnʊks/ ⓘ LIN-uuks)，并带有一个短的“i”，如“print”和“u”中的那样如“投入”。为了进一步演示“Linux”这个词应该如何发音，他提供了带有内核源代码的音频指南。然而，在这段录音中，他将 Linux 发音为 /ˈlinʊks/ (LEEN-uuks)，带有短但紧密的前不圆唇元音，而不是像这样的近近近前不圆唇元音在他的新闻组帖子中。

### Commercial and popular uptake 商业化和大众化

Linux 在生产环境中的采用，不仅仅由业余爱好者使用，在 20 世纪 90 年代中期首先在超级计算社区中开始兴起，NASA 等组织开始用运行着廉价商用计算机的集群来取代日益昂贵的机器。 Linux。当戴尔和IBM以及惠普开始提供Linux支持以摆脱微软在桌面操作系统市场的垄断时，商业用途就开始了。

如今，Linux 系统广泛用于计算领域，从嵌入式系统到几乎所有超级计算机 ，并在服务器安装中占据一席之地，例如流行的 LAMP 应用程序堆栈。 Linux 发行版在家庭和企业桌面中的使用一直在增长。Linux发行版在上网本市场也变得流行，许多设备都安装了定制的 Linux 发行版，谷歌也发布了自己专为上网本设计的 ChromeOS。

Linux 在消费市场上最成功的可能是移动设备市场，Android 是智能手机上的主导操作系统，在平板电脑以及最近的可穿戴设备上非常流行。 Linux 游戏也在兴起，Valve 展示了对 Linux 的支持，并推出了 SteamOS，这是它自己的面向游戏的 Linux 发行版，后来在他们的 Steam Deck 平台中实施。 Linux 发行版也受到各个地方和国家政府的欢迎，例如巴西联邦政府。
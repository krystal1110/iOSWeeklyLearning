# iOS摸鱼周报 第十三期

![](https://gitee.com/zhangferry/Images/raw/master/gitee/iOS摸鱼周报模板.png)

iOS摸鱼周报，主要分享开发过程中遇到的经验教训、优质的博客、高质量的学习资料、实用的开发工具等。周报仓库在这里：https://github.com/zhangferry/iOSWeeklyLearning ，如果你有好的的内容推荐可以通过 issue 的方式进行提交。另外也可以申请成为我们的常驻编辑，一起维护这份周报。另可关注公众号：iOS成长之路，后台点击进群交流，联系我们，获取更多内容。

## 开发Tips

### CocoaPods 常见操作

#### pod install 和 pod update 的区别

 什么时候使用pod install：用这个命令安装或者删除一些pods。即使在执行这个命令之前已经有Podfile文件。
 什么时候使用pod update: 当我们想更新某个pods 到某个新的版本。（注意我们不建议直接使用这个命令，使用pod update podName）。
 
#### pod install 使用时机

当我们的工程首次想使用cocoapods 管理第三方库的时候。当我们每次编辑我们的Podfile时候比如（添加，删除或者编辑一个pod库的时候）。

* 每次我们执行pod install 命令的时候，会下载安装新的pod,并把每个pod的版本写到Podfile.lock 文件里。这个文件跟踪所有的pod库的版本并锁定他们的版本。
* 当执行pod install的时候，只解析Podfile.lock中没有列出的pod依赖项。1. 对于Podfile.lock 列出的版本，会不需要检查pods是否有更新直接使用既有的版本安装。2. 对于Podfile.lock 未列出的版本，会根据Podfile 描述的版本安装。

#### pod outdated 使用时机

之前说如果想更新某个库采用例如pod update podName 而不是整体更新。在之前想列出Podfile.lock 里哪些库有新的版本可以使用这个命令pod outdated。

#### pod update 使用时机

当我们执行pod update podName 的时候。CocoaPods将试着找到podName的最新版本，会忽略Podfile.lock文件的版本，会尽可能的更新到最新的版本。如果Podfile写了版本，会匹配Podfile的版本。如果不写版本会更新到最新的版本，并更新Podfile.lock文件版本。

如果我们直接使用pod update命令。CocoaPods会更新Podfile里所列出的所有的库到可能的最新的版本。并更新Podfile.lock版本。

### CocoaPods 一个完整使用场景

#### 阶段一：团队成员七七创建了一个项目

七七创建这个项目，想使用库AFN，SDWebImage等库。因此七七在Podfile列出来这些库，然后使用pod install。这时候AFN使用了1.0.0版本，SDWebImage使用了1.0.0版本。
Podfile.lock会跟踪锁定AFN，SDWebImage 到1.0.0版本。

#### 阶段二：七七添加一个新的pod

后面，七七添加一个库YYmodel到Podfile里。这时候SDWebImage维护者更新了2.0.0版本。七七 pod install后更新下来的是YYmodel。由于之前Podfile.lock跟踪锁定了SDWebImage等库，这时候安装仍然是1.0.0版本。、

#### 阶段三：灰灰加入了这个项目

由于灰灰电脑上从来没有这个项目。clone项目并且使用pod install。由于七七把Podfile.lock文件纳入了版本控制。这时候灰灰pod install 后安装的版本是个七七一样的版本。因为之前库的版本都在Podfile.lock跟踪锁定了，即使那些库的维护者更新了N个版本。

#### 阶段四：检查某个库是否有新的版本

七七想检查这些pods是否有新的版本。使用pod outdated 会告诉七七SDWebImage最新版已经更新到了2.0.0。正好由于SDWebImage 有个crash问题，因此七七决定更新SDWebImage到2.0.0版本。因此使用pod update SDWebImage命令更新SDWebImage到2.0.0版本，这时Podfile.lock会更新锁定版本到2.0.0版本。

#### 阶段五：项目持有管理者七七同步版本给其他团队成员

如果灰灰想使用最新的版本，只能通过七七提交的Podfile.lock 和 Podfile 来更新相应的库。

### CocoaPods 使用建议

* 工程持有管理者对项目进行cocoapods初始化的时候会有一个Podfile.lock 这个文件我们需要纳入版本控制里。这些其他团队协作人员直接使用pod install来安装使用。

* 如果需要更新某个库到某一个版本，由项目持有管理者采用pod update podName的方式更新某个库到一定的版本。然后提交Podfile.lock 和 Podfile 文件。其他团队直接pod install使用。


## 那些Bug


## 编程概念

整理编辑：[师大小海腾](https://juejin.cn/user/782508012091645)，[zhangferry](https://zhangferry.com)


### 什么是 BIOS

BIOS 全称为 Basic Input Output System，即基本输入输出系统，亦称为 ROM BIOS、System BIOS、PC BIOS。BIOS 是预先内置在计算机主机内部的程序，也是计算机开机后加载的第一个程序。BIOS 保存着计算机最重要的基本输入输出的程序、开机后自检程序和系统自启动程序，它可从 CMOS（是电脑主板上的一块可读写的 RAM 芯片）中读写系统设置的具体信息。早年，BIOS 存储于 ROM 芯片上；现在的 BIOS 多存储于闪存芯片上，这方便了 BIOS 的更新。

BIOS 除了键盘，磁盘，显卡等基本控制程序外，还有引导程序的功能。引导程序是存储在启动驱动器起始区域的小程序，操作系统的启动驱动器一般是硬盘。不过有时也可能是 CD-ROM 或软盘。

电脑开机后，BIOS 会确认硬件是否正常运行，没有异常的话就会直接启动引导程序，引导程序的功能就是把在硬盘等记录的 OS 加载到内存中运行，虽然启动应用是 OS 的功能，但 OS 不可以自己启动自己，而是通过引导程序来启动。

![](https://gitee.com/zhangferry/Images/raw/master/iOSWeeklyLearning/20210527232231.png)


### 什么是汇编

汇编语言（Assembly Language）是任何一种用于电子计算机、微处理器、微控制器或其他可编程器件的低级语言，亦称为符号语言。在汇编语言中，用助记符代替机器指令的操作码，用地址符号或标号代替指令或操作数的地址。在不同的设备中，汇编语言对应着不同的机器语言指令集，通过汇编过程转换成机器指令。特定的汇编语言和特定的机器语言指令集是一一对应的，不同平台之间不可直接移植。

汇编语言是计算机提供给用户的最快最有效的语言，也是能够利用计算机的所有硬件特性并能够直接控制硬件的唯一语言。但是由于编写和调试汇编语言程序要比高级语言复杂，因此目前其应用不如高级语言广泛。

汇编语言比机器语言的可读性要好，但跟高级语言比较而言，可读性还是较差。不过采用它编写的程序具有存储空间占用少、执行速度快的特点，这些是高级语言所无法取代的。在实际应用中，是否使用汇编语言，取决于具体应用要求、开发时间和质量等方面作权衡。


### 什么是虚拟机

虚拟机（Virtual Machine）是指通过软件模拟的具有完整硬件系统功能的、运行在一个完全隔离环境中的完整计算机系统。在实体计算机中能够完成的工作在虚拟机中都能够实现。在计算机中创建虚拟机时，需要将实体机的部分硬盘和内存容量作为虚拟机的硬盘和内存容量。每个虚拟机都有独立的 CMOS、硬盘和操作系统，可以像使用实体机一样对虚拟机进行操作。

虚拟机的主要用处有：

1. 演示环境，可以安装各种演示环境，便于做各种例子
2. 保证主机的快速运行，减少不必要的垃圾安装程序，偶尔使用的程序，或者测试用的程序在虚拟机上运行
3. 避免每次重新安装，银行等常用工具，不经常使用，而且要求保密比较好的，单独在一个环境下面运行
4. 想测试一下不熟悉或者有风险的应用，在虚拟机中随便安装和彻底删除
5. 体验不同版本的操作系统，如 Linux、Mac 等。

虚拟机目前可分为三类：

* 系统虚拟机，例如：VMware
* 程序虚拟机，例如：JVM（Java Virtual Machine）
* 操作系统层虚拟化，例如：Docker


### 什么是外围中断

IRQ（Interrupt Request）代表的就是中断请求。IRQ 是用来暂停当前正在运行的程序，并跳转到其他程序运行的必要机制。该机制被称为处理中断。中断处理在硬件控制中担当着重要的角色。因为如果没有中断处理，就有可能无法顺畅进行处理的情况。

从中断处理开始到请求中断的程序（中断处理程序）运行结束之前，被中断的程序（主程序）的处理是停止的。这种情况就类似于在处理文档的过程中有电话打进来，电话就相当于是中断处理。假如没有中断处理的发生，就必须等到文档处理完成后才能够接听电话。由此可见，中断处理有着巨大的价值，就像是接听完电话后会返回原来的文档作业一样，中断程序处理完成后，也会返回到主程序中继续。

![中断请求示意图](https://gitee.com/zhangferry/Images/raw/master/iOSWeeklyLearning/20210526233248.png)

**实施中断请求的是连接外围设备的 I/O 控制器，负责实施中断处理的是 CPU**，外围设备的中断请求会使用不同于 I/O 端口的其他编号，该编号称为中断编号。在控制面板中查看软盘驱动器的属性时，IRQ 处现实的数值是 06，表示的就是用 06 号来识别软盘驱动器发出的请求。还有就是操作系统以及 BIOS 则会提供响应中断编号的中断处理程序。

假如有多个外围设备进行中断请求的话， CPU 需要做出选择进行处理，为此，我们可以在 I/O 控制器和 CPU 中间加入名为中断控制器的 IC 来进行缓冲。中断控制器会把从多个外围设备发出的中断请求有序的传递给 CPU。中断控制器的功能相当于就是缓冲。下面是中断控制器功能的示意图

![中断控制器的功能](https://gitee.com/zhangferry/Images/raw/master/iOSWeeklyLearning/20210526233322.png)


CPU 在接受到中断请求后，会把当前正在运行的任务中断，并切换到中断处理程序。中断处理程序的第一步处理，就是把 CPU 所有寄存器的数值保存到内存的栈中。在中断处理程序中完成外围设备的输入和输出后，把栈中保存的数值还原到 CPU 寄存器中，然后再继续进行对主程序的处理。

假如 CPU 寄存器数值还没有还原的话，就会影响到主程序的运行，甚至还有可能会使程序意外停止或发生运行时异常。这是因为主程序在运行过程中，会用到 CPU 寄存器进行处理，这时候如果突然插入其他程序的运行结果，此时 CPU 必然会受到影响。所以，在处理完中断请求后，各个寄存器的值必须要还原。只要寄存器的值保持不变，主程序就可以像没有发生过任何事情一样继续处理。

![请求中断的处理](https://gitee.com/zhangferry/Images/raw/master/iOSWeeklyLearning/20210526234046.png)


### 什么是 DMA

DMA 全称为 Direct Memory Access，即直接存储器访问。DMA 是一种内存访问机制，它是指在不通过 CPU 的情况下，外围设备直接和主存进行数据传输。磁盘等硬件设备都用到了 DMA 机制，通过 DMA，大量数据就可以在短时间内实现传输，之所以这么快，是因为 CPU 作为中介的时间被节省了，下面是 DMA 的传输过程


![使用 DMA 的外部设备和不使用 DMA 的外部设备](https://gitee.com/zhangferry/Images/raw/master/iOSWeeklyLearning/20210527220519.png)


I/O 端口号、IRQ、DMA 通道可以说是识别外围设备的 3 点组合。不过，IRQ、DMA 通道并不是所有外围设备都具备的。计算机主机通过软件控制硬件时所需要的信息的最低限，是外围设备的 I/O 端口号。IRQ 只对需要中断处理的外围设备来说是必须的，DMA 通道则只对需要 DMA 机制的外围设备来说必须的。假设多个外围设备都设定成相同的端口号、IRQ 和 DMA 的话，计算机就无法正常工作，会提示设备冲突。





## 优秀博客

整理编辑：[皮拉夫大王在此](https://www.jianshu.com/u/739b677928f7)


本期博客汇总的主题是 `watchdog`

1、[iOS watchdog (看门狗机制)](https://www.jianshu.com/p/6cf4aeced795 "iOS watchdog (看门狗机制)") -- 来自简书：__Mr_Xie__


先来简单了解什么是 watchdog。

2、[iOS App 后台任务的坑](http://www.cocoachina.com/articles/27303 "iOS App 后台任务的坑") -- 来自cocoachina ：米米狗


后台任务泄漏是导致触发 watchdog 常见情况之一，还有一种情况就是主线程卡死，文章中有介绍如何区分。


3、[Addressing Watchdog Terminations](https://developer.apple.com/documentation/xcode/addressing-watchdog-terminations "Addressing Watchdog Terminations")


苹果的官方文档。对我个人而言，了解 scene-create 和 scene-update 的含义在排查问题过程中起到了一定的作用。


4、[你的 App 在 iOS 13 上被卡死了吗](https://zhuanlan.zhihu.com/p/99232749 "你的 App 在 iOS 13 上被卡死了吗")


进入实践阶段，其实我们很少真的在主线程做大量耗时操作如网络请求等。触发 watchdog 往往是不经意的，甚至你不会怀疑你的代码有任何问题。这篇文章介绍的是 58 同城团队如何定位到剪切板造成的启动卡死。


5、[iOS 稳定性问题治理：卡死崩溃监控原理及最佳实践](https://juejin.cn/post/6937091641656721438 "iOS 稳定性问题治理：卡死崩溃监控原理及最佳实践")


这篇文章是字节跳动 APM 团队早些时候发表的，是业界少有的公开介绍卡死崩溃的原因的文章，具有很强的借鉴意义。我们在做启动卡死优化的过程中，文中提到的相关问题基本都有遇到，只不过在此之前并不知道什么原因以及如何解决。所以说如果你想做卡死治理，可以参考下这篇文章。

6、[面试过 500+ 位候选人之后，想谈谈面试官视角的一些期待](https://mp.weixin.qq.com/s/kv-_oZObp7QRHeAbrkdfsA "面试过500+位候选人之后，想谈谈面试官视角的一些期待")


《iOS 稳定性问题治理：卡死崩溃监控原理及最佳实践》的作者在面试了 500+ 候选人后写的文章，有需要的同学可以针对性的做些准备。


## 学习资料

整理编辑：[Mimosa](https://juejin.cn/user/1433418892590136)

## 工具推荐

整理编辑：[brave723](https://juejin.cn/user/307518984425981/posts)

### Application Name

**地址**：

**软件状态**：

**使用介绍**



## 联系我们

[摸鱼周报第五期](https://zhangferry.com/2021/02/28/iOSWeeklyLearning_5/)

[摸鱼周报第六期](https://zhangferry.com/2021/03/14/iOSWeeklyLearning_6/)

[摸鱼周报第七期](https://zhangferry.com/2021/03/28/iOSWeeklyLearning_7/)

[摸鱼周报第八期](https://zhangferry.com/2021/04/11/iOSWeeklyLearning_8/)

![](https://gitee.com/zhangferry/Images/raw/master/gitee/wechat_official.png)
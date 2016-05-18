# platform


##  iOS 日志打印库
###   关于选择CocoaLumberjack第三方库作为iOS项目中日志打印工具的说明    
CocoaLumberjack 最早是由Robbie Hanson 开发的日志库，是Mac 和iOS上一个集快捷、简单、强大和灵活于一身的日志框架，专为Objective-C设计，以下为选择CocoaLumberjack 的几个理由:    

1、Star数目，在github 上搜索iOS Log，筛选Star 数目最多的一个，CocoaLumberjack排在了第一位，有7000 多个stars,相比第二名1200多个，差不多是第二名的7倍，是第三名的30多倍，和其他的开源库的star就不在一个等级，由于前三名的差别甚大，本人就选取了前两名作为对比。    

2、作者在github中的活跃度，CocoaLumberjack 的作者是Robbie Hanson，查看他的github, Follwers 有1.6K之多，并且自己的好几个开源项目star数都很多，在github 上的活跃度也挺好。Star数排名第二的开源项目https://github.com/marcoarment/BugshotKit 的作者marcoarment 他的github主页如下：除了Followers指标在一个数量级之外，其他的指标和Robbie Hanson 都不在一个数量级。所以，通过对比作者影响力，Robbie Hanson >> marcoarment 。对比到这个指标的时候，已经可以初定为CocoaLumberjack了。    

3、	README详情，详见：https://github.com/CocoaLumberjack/CocoaLumberjack/blob/master/README.md 和https://github.com/marcoarment/BugshotKit/blob/master/README.md 通过对比，无论是从README详细程度还是局限性方面CocoaLumberjack 都比BugshotKit 更全。BugshotKit 有局限性在它的README里面这样写到：For development and beta tests only!。    

4、	最后更新时间、issues、fork等CocoaLumberjack 最近一直都有所更新，而BugshotKit 最后一次更新为去年。

5、开源协议：CocoaLumberjack 遵守BSD, BugshotKit 遵守WTF。

6、综合考虑，CocoaLumberjack 是最佳的选择。

###   使用CocoaLumberjack时安装XcodeColors的坑    

1、直接安装方式    

在使用Lumberjack的时候，如果需要打印出来的日志多彩多样，具有等级划分，需要安装XcodeColors的支持，通常的电脑直接安装XcodeColors之后就可以使用得畅通无阻，一般安装XcoedeColorsCocoaLumberjack可通过两种方式进行安装，一种是直接下载安装，地址：https://github.com/robbiehanson/XcodeColors ，这里最好下Robbiehanson 的，解压XcodeColors压缩包并打开工程Scheme项选择XcodeColors直接运行，如果没问题在如下的目录/Library/Application Support/Developer/Shared/Xcode/Plug-ins/下 会有这么一个.xcplugin文件XcodeColors.xcplugin,说明XcodeColors插件已经在Mac上安装成功。
重启Xcode会弹出一个提示框：提示你是否Load Bundle(由于我的Mac在安装的时候遇到了一些问题，这个弹框没能截屏)，在此，直接Load Bundle就 OK ,选择刚才打开的工程这次选择TestXcodeColors Scheme测试是否安装成功。通常的情况下在终端下都能正常显示各种带颜色的字体。但万事都有例外，
一开始我就只这么做的，可是字体颜色还是白色，这是一个大坑，整了很久还是没整好，重新移除插件之后再安装，还是不行，最后知道还有另外一种方法即：用插件Alcatraz 进行安装    

2、用插件Alcatraz 进行安装    

用插件Alcatraz 进行安装，https://github.com/alcatraz/Alcatraz 打开并重启Load Bundle  点击 Window->Pakage Manager 如果列表里没有可直接搜索XcodeColors，直接点击INSTALL ，自动安装，安装好了之后，重启Xcode，再次打开Xcode 的时候，Load Bundle一下,一般情况下，到了这一步就装好了，测试也不会有太大问题，终端能正常打印多种颜色的字体，如果还不能，请把XcodeColors移除，再重新安装，问题得到了解决（我的问题就是这么解决了），在使用Lunmerjack进行测试的时候用也能正常打印不同等级的日志输出。并且Alcatraz里面含有很多的插件，丰富多彩，Alcatraz这个插件挺好用，推荐使用。





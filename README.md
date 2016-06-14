# platform

## iOS 未使用资源的检测工具    
经多方调查研究，在检测Xcode 工程中未使用的代码的检测暂时还没有结果，对未使用资源的检测，经多方比较得出目前好的工具列出如下：（[参考博客](http://blog.lessfun.com/blog/2015/09/02/find-unused-resources-in-xcode-project/)）    

#### 方案1、脚本（这里展示了shell 的）    
	#!/bin/sh    
	PROJ=`find . -name '*.xib' -o -name '*.[mh]'`    
	for png in `find . -name '*.png'`    
	do 
	    name=`basename $png`    
	    if ! grep -qhs "$name" "$PROJ"; then    
	    	echo "$png is not referenced"    
	    fi    
	done    
这种方法的缺点是：不够智能，不够通用，速度太慢，结果不正确。    

#### 方案2、脚本界面化Unused    
Unused对脚本的调用做了封装，通过界面可以配置一定的信息，然后比较清晰的输入结果。    
缺点：实际上，Unused 的内部还是调用了方案1的脚本，所以方案1的缺点也就是方案2的缺点。    

#### 方案3、LSUnusedResources    
LSUnusedResources 有以下的优点：    
##### 1、LSUnusedResources提高了匹配速度    
LSUnusedResources 很大程度上受Unused的影响，比如界面、交互，以及部分代码。但是，本工具在核心代码上做了优化，使其在搜索速度、结果的正确上有很大的提高    

 核心步骤简述如下：    
 查找：选定目录下的所有资源文件。这一步与上述方案1区别不大，都是调用find命令进行查找指定后缀的文件。    
 匹配：与上述方案不同，这里不是对每个资源文件名都做一次全文匹配，因为加入项目的资源太多，这里会导致性能快速下降。这里只是针对源码、xib、storyboard和plist等文件，先全文搜索其中可能是引用了资源的字符串，然后用资源名和字符串做匹配    

##### 2、LSUnusedResources优化了匹配结果    
Unused 会把大量实际上有使用的资源，当做未使用的资源输出。LSUnusedResources 则不会出现这样的问题，并且使得结果更加优化。    
例如：添加了下面的资源：    
     icon_tag_0.png    
     icon_tag_1.png    
     icon_tag_2.png    
     icon_tag_3.png    
     icon_tag_4.png    
     
然后用字符串拼接在代码中引用    

     NSInteger index = random() % 4;    
     UIImage *img = [UIImage imageNamed:[NSString stringWithFormat:@"icon_tag_%d", index]];    
     
icon_tag_x.png 是不应该被当做未使用的资源的，只是以一种比较隐晦的方式间接引用了，所以不应该出现在结果列表中    


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

#Andorid-Log日志第三方库选择的说明

本次Log库的选择主要通过以下细节来确定最终选择使用的Log库结果，首先根据github的star来进行初步筛选，其次根据更新速度，评价，维护人数以及维护公司，README来确定，当然最终是根据具体的使用情况和兼容性来确定，目前选择的结果为github：orhanobut/logger，之前star排名第二，目前观察已经超过第一，排名第一。简单解释不选择JakeWharton/hugo的原因，从开发人员来看JakeWharton相对于前者有名。但从使用结果，README,引入方式，Log支持版本来看，都略差于orhanobut/logger 。所以最终选择orhanobut/logger。


下面简单介绍一下github：orhanobut/logger的使用方法

##1、支持环境
经过测试确认，目前发现此Log日志无SDK与JDK要求，Android可完美运行，eclipse只要能支持Maven即可。 
##2、引用方法：
这里主要以Android Studio为例。
###第一步：引入Maven的URL
需要在我们项目的build.gradle中引用：具体代码如下：
	repositories {
    		jcenter()
    	maven {
        	url "https://jitpack.io"
    	}
}
###第二步：在我们APP下的bulid.gradle中需要进行远程依赖：具体代码如下：
	dependencies {
	
	    compile 'com.github.orhanobut:logger:1.12'
	}
配置以上两步后，重新加载gradle即可引入Log日志。

###此Log日志与传统Log日志的优势：
	1、	相对于传统Log日志输出更多样化，更加美观。
	2、	可打印当前Log日志输出的多层级方法。
	3、	打印代码更简洁，如：Logger.i(“value”),而传统的每一个Log都需要对应的一个key,如：Log.i(“key”,”value”).
	4、	过滤层级可很好控制。
	5、	可区分正式版本与测试版本，可通过Logger.logLevel(LogLevel.NONE) ; 与 Logger.logLevel(LogLevel.FILL) ;来控制，NONE为正式版本，不会输出任何一个日志，FILL为测试版本，及会输出Log日志。
	6、	源码可查看，也可自定义输出格式。
	7、	显示格式很灵活，可根据项目需求来输出内容。
	8、	对json.xml等有特殊、美观的输出格式，可很方便的进行过滤。
	9、	有很好的维护性。
	10、	对严重级的错误可用标红处理，更加显眼。


###使用方法介绍：
	 Logger
                .init(MY_TAG)                 // default PRETTYLOGGER or use just init()
                .methodCount(0)                 // default 2
                .hideThreadInfo()               // default shown
                .logLevel(LogLevel.NONE) ;      // default LogLevel.FULL
                //.methodOffset(0)               // default 0
                //.logTool(new AndroidLogTool()); // custom log tool, optional
####初始化：日志打印初始化，注意LogLevel.NONE表示为版本发布
Log日志提供的方法如下：

	Log.i();    //打印info信息
	Log.d();   // 打印debug信息 
	Log.e();   // 打印Error 信息
	Log.v();   //打印Verbose信息
	Log.w();  	//打印warn信息
	
	Log.t(“”);     //添加标记
	Log.t(0);     // 打印方法数
	Log.wtf();   //输出wtf格式的信息
	Log.json();  //输出json格式的信息 
	Log.xml();  //输出xml个数的信息


##注意事项：
###1、	使用前必须进行初始化，否则会出现空指针，导致程序崩溃。
###2、	发布正式版本时。一定要把LOG版本设为正式版本调用如下代码：Logger.logLevel(LogLevel.NONE);



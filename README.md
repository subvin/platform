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






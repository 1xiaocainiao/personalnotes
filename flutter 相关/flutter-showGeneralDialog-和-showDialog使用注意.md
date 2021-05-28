##showDialog使用
在首页视图使用showDialog弹窗时发现，在iOS上，顶部和下部当有SafeArea时，会留有一片区域空白，原因是showDialog有个属性useSafeArea默认为 true，改为fasle即可

##showGeneralDialog使用
barrierDismissible 当将这个属性设置为true时，发现此时弹窗永远都不出现，查看控制台报错如下
```
Unhandled Exception: 'package:flutter/src/widgets/routes.dart': Failed assertion: line 1825 pos 10: '!barrierDismissible || barrierLabel != null': is not true.
```
谷歌一圈没搜到，正在愁眉之际，还是去翻了下方法中的文档，其中有一段
```
/// The `barrierDismissible` argument is used to determine whether this route
/// can be dismissed by tapping the modal barrier. This argument defaults
/// to true. If `barrierDismissible` is true, a non-null `barrierLabel` must be
/// provided.
```
很明显当设置为true时必须要提供barrierLabel，设置好后正常弹窗.

遇到问题还是要查阅文档啊!!!特此记录

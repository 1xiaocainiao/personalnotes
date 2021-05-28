遇到的问题
1.手动配置IntentConfiguration时，Provider 中实现的协议方法中的Intent 和 Entry需要替换为确定的类型，否则会报错，坑了我好久。。。
Provider 错误信息
Type 'Provider' does not conform to protocol 'IntentTimelineProvider

@main
struct GKWYWidget 中的错误信息
Initializer 'init(kind:intent:provider:content:)' requires the types 'ConfigurationIntent' and 'Provider.Intent' be equivalent

widget 需要单独在配置一份identifier（即bundle id），并且是以主app的identifier为prefix，注意identifier中开启对App group的支持，创建app group，在工程中需要注意添加App group,添加后会生成文件.entitlements后缀的文件，需要将创建的App group 的id填入如图![image.png](https://upload-images.jianshu.io/upload_images/167849-fe2d579a58537f43.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



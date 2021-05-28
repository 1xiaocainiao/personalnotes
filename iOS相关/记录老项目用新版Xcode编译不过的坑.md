今天用Xcode12跑了一下以前的老项目(模拟器)，项目是workspace模块化的，其中有自己制作的framework依赖，其中一个报错 no such module "framework", 一直没有头绪，就暂时放那儿了，过了一会儿查看在报no such module的地址多了信息，Could not find module '' for target 'x86_64-apple-ios-simulator': found: arm64, arm64-apple-ios-simulator
根据这个错误搜到如下文章[关于适配XCode 12 跑模拟器编译报错的错误](https://juejin.cn/post/6875270871083286542),其中提到了Xcode12的变化，以前的Valid Architectures 变为了VALID_ARCHS, 我刚开始是粗暴的把这项删除了，模拟器也能跑，真机暂时没证书没试过，楼下评论有更简单且同时支持真机模拟器的方法,
其中有童鞋提到新版本的 Xcode 12.0.1已经没有VALID_ARCHS，后续版本没试过，不过应该也没了吧😁
```
将VALID_ARCHS设置为$(ARCHS_STANDARD)可以同时支持真机和模拟器，
将VALID_ARCHS设置为$(ARCHS_STANDARD)可以同时支持真机和模拟器,
将VALID_ARCHS设置为$(ARCHS_STANDARD)可以同时支持真机和模拟器,
```
[stackoverflow](https://stackoverflow.com/questions/63391793/xcode-12-build-target-in-wrong-order-for-simulator/64150387#64150387)


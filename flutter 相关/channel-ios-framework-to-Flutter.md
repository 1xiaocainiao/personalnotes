今天开发Flutter插件，踩了些坑，记录一下
1.Android Studio 新建Flutter 项目，选择plugin,如图
![image.png](https://upload-images.jianshu.io/upload_images/167849-f29974f5e8610375.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
2.添加第三方库，如下图打开 iOS 下的 .podspec文件，编辑时注意红色框框，s.dependency 'SVProgressHUD', '2.2.5'，可不加版本号。
![image.png](https://upload-images.jianshu.io/upload_images/167849-60fbfe0559ec4bbf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这个废了我点时间，终于在Stack Overflow上找到了 [How to use cocoapods with a Flutter plugin?](https://stackoverflow.com/questions/54349138/how-to-use-cocoapods-with-a-flutter-plugin)

添加完成后，cd flutter_plugin_demo/example/iOS/ 执行一次 pod install



3.剩下的就是按照[Flutter插件开发](https://juejin.im/post/6844903822251425805#heading-5)步骤一步步做了，注意要编写相关iOS平台代码时一定要先编译成功一次
flutter build ios --no-codesign


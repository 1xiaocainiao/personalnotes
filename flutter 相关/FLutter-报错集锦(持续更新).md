网络请求偶尔出现 connection closed before full header was received dart
后台修改http2配置

无法打开“iproxy”，因为无法验证开发者。
设置，安全与隐私，看是否有iproxy允许的提示，点击仍然允许

使用融云插件rongcloud-im-flutter-sdk, 执行了 pod repo update, 因为是新电脑，环境是重新配置的，导致了融云的版本不一致，pod install一直失败，详见[[rongcloud-im-flutter-sdk](https://github.com/rongcloud/rongcloud-im-flutter-sdk)
](https://github.com/rongcloud/rongcloud-im-flutter-sdk/issues/142)，后来通过明确指定融云版本解决rongcloud_im_plugin: 4.0.4
注意 rongcloud_im_plugin: 4.0.3 只明确指定版本， rongcloud_im_plugin: ^4.0.3 和 用 rongcloud_im_plugin: any 一样，默认加载的最新版本

使用flutter_ffmpeg时，千万要注意如下图的顺序,否则会出现写奇怪的问题
![image.png](https://upload-images.jianshu.io/upload_images/167849-e5b88488284b9e2e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

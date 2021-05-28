[vscode-flutter-i18n-json](https://github.com/esskar/vscode-flutter-i18n-json)

添加依赖
dependencies:
  flutter:
    sdk: flutter
  flutter_localizations:
    sdk: flutter

按照教程安装好插件后: 打开cmd+shift+p
1.Flutter I18n Json: Initialize, 初始化后会创建以下文件
i18n/<default-locale>.json
lib/generated/i18n.dart
i18nconfig.json
2.Flutter I18n Json: Add locale, 添加要支持的语言，例如 输入 zh-CN
3.在i18n目录下生成的json文件添加国际化的键值对 key = value, 然后必须执行Flutter I18n Json: Create automagic translations from default locale命令，才会在i18n.dart文件生成将要使用的国际化代码，如添加键值对后，执行命令生成![WX20190930-103715.png](https://upload-images.jianshu.io/upload_images/167849-b47ec80423365e6a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
4.使用：除了按照官方教程添加代码外，格外注意，需要在设置localizationsDelegates的地方，额外添加
```
localizationsDelegates: [i18n,
GlobalMaterialLocalizations.delegate,
GlobalWidgetsLocalizations.delegate,
GlobalCupertinoLocalizations.delegate],
```
避免使用有问题，我自己使用时刚开始没添加下面三个，fultter报错了, 如图![WX20190930-104523.png](https://upload-images.jianshu.io/upload_images/167849-e6cd8060614b6422.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

5.iOS使用还需要在Runner工程的info.plist添加
```
<key>CFBundleLocalizations</key>
  <array>
    <string>en</string>
    <string>es</string>
    <string>ru</string>
  </array>
```
，以及如图所示![WX20190930-104319.png](https://upload-images.jianshu.io/upload_images/167849-88007618caed235b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



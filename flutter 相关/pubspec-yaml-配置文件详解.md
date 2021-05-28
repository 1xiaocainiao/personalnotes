最近发现指定版本有不明白的地方，找了个资料看下 [原文链接](https://www.cnblogs.com/mengqd/p/13928830.html)

pubspec.yaml 是 Flutter 项目的配置文件，类似于 Android 中的 Gradle 配置文件，下面我们就看看 pubspec.yaml 中各个属性的配置。

创建一个新的项目（Flutter Application），pubspec.yaml 位于根目录，如图：

![image](https://upload-images.jianshu.io/upload_images/167849-3f6429a79afd7b03.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

项目中默认配置，去掉注释部分，剩下如下：

```
name: flutter_app
description: A new Flutter application.

publish_to: 'none' 

version: 1.0.0+1

environment:
  sdk: ">=2.7.0 <3.0.0"

dependencies:
  flutter:
    sdk: flutter

  cupertino_icons: ^1.0.0

dev_dependencies:
  flutter_test:
    sdk: flutter

flutter:
  uses-material-design: true

```

下面我们一个一个的详细介绍下。

### name

此属性表示包名（package name），此属性是非常重要的，引入其他文件时需要使用此包名：

```
import 'package:flutter_app/home_page.dart';

```

如果你修改包名为 ，那么相应的引入也需要修改:

```
import 'package:flutter_app_demo/home_page.dart';

```

如果你创建了一个 Flutter 插件并发布到 [pub.dev](https://pub.dev/)，那么此属性将会作为标题显示，同时其他人引用也需要使用此属性。

![image](https://upload-images.jianshu.io/upload_images/167849-adbcf8a79e41e0d1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### description

**description** 属性是一个**可选**配置属性，是对当前项目的介绍。如果作为插件发布到 pub.dev 上，此值显示在如下位置：

![image](https://upload-images.jianshu.io/upload_images/167849-1162da3eba4bea3e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### version

此属性应用程序的版本和内部版本号，格式为 **x.x.x+x**，例如：**1.0.0+1**，这个版本号称为 **语义版本号（semantic versioning ）**，semantic versioning 相关知识请[参考此处](https://semver.org/spec/v2.0.0-rc.1.html)。

版本号 **+** 前面到部分，叫做 **version number**，由 2 个小点隔开，后面的部分叫做 **build number**。

在 Android 中 version number 对应 **versionName**，build number 对应 **versionCode**，在 android/build.gradle 下有相关配置，

![image](https://upload-images.jianshu.io/upload_images/167849-431f2b684c50495e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

早期的版本 build.gradle 中 versionName 和 versionCode 是直接写死的数字，如下：

![image](https://upload-images.jianshu.io/upload_images/167849-4aae60f1ca8a6f7f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

此时修改版本号只能通过修改 build.gradle 。而现在可以直接通过 pubspec.yaml 进行修改。

如果是插件，那么用户可以通过此版本号指定使用哪个版本，

```
path_provider: ^1.6.22

```

版本的指定有多种形式：

#### 不指定或者 any

```
path_provider:

path_provider: any

```

此种格式默认加载 **最新的版本**，但强烈不推荐使用此方式，因为版本的变化会导致接口发生变化，项目出现编译异常。

#### x.y.z

明确指定版本

```
path_provider: 1.6.22

```

指定依赖的版本。

#### <=x.y.z 或者<x.y.z

小于或者小于等于此版本的包

```
path_provider: <=1.6.22

path_provider: <1.6.22

```

#### >=a.b.c <x.y.z

指定版本的区间

```
path_provider: '>=1.0.0 <1.6.22'

```

#### ^x.y.z

此方式为最常见的方式，也是**推荐**的方式。

此方式表示大版本不变，小版本使用最新的版本，例如`^1.6.22 相当于`'>=1.6.22 <2.0.0'`

```
path_provider: ^1.6.22

```

### author homepage issue_tracker repository

这四种属性在 Flutter Application 项目中默认是没有的，正常项目中也无需这几个属性，当我们开发插件并发布到 pub 时需要这几个属性。

当我们创建一个插件时，默认配置：

![image](https://upload-images.jianshu.io/upload_images/167849-88728905df18b3d0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

issue_tracker 和 repository 我们可以手动创建。这四个属性说明：

*   author：作者，填写自己的署名
*   homepage：主页。
*   issue_tracker：issue，一般写当前插件源代码的Github issue 地址。
*   repository：一般写当前插件源代码的Github地址。

这些属性会显示在 pub.dev 主页上：

![image](https://upload-images.jianshu.io/upload_images/167849-17affb05a6fb03c6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### Environment

Environment 属性下添加 **Flutter** 和 **Dart** 版本控制。

```
environment:
  sdk: ">=2.7.0 <3.0.0"

```

上面的版本规定此应用或库只能在高于或等于2.7.0，低于3.0.0的Dart SDK版本上运行。

我们也可以手动添加 Flutter 版本：

```
environment:
  sdk: ">=2.7.0 <3.0.0"
  flutter: "1.22.0"

```

也可以通过此属性使用实验性质的版本：

```
environment:
  sdk: ">=2.11.0-213.0.dev <2.12.0"

```

### dependencies 和 dev_dependencies

dependencies 和 dev_dependencies 下包含应用程序所依赖的包，dependencies 和 dev_dependencies 就像其名字一样，dependencies 下的所有依赖会编译到项目中，而 dev_dependencies 仅仅是运行期间的包，比如自动生成代码的库。

我们可以通过四种方式依赖其包：

*   依赖 pub.dev 上的第三方库
*   依赖本地库
*   依赖 **git repository**
*   依赖我们自己的 **pub仓库**

#### 依赖 pub.dev 上的第三方库

依赖 pub.dev 上的第三方库是最常用的一种方式

```
dependencies:
  path_provider: ^1.6.22

```

#### 依赖本地库

如果你在本地创建了一个模块，依赖本地的库：

```
dependencies:
  flutter_package:
    path: ../flutter_package

```

#### 依赖 git repository

依赖 Github 上的一个插件：

```
dependencies:
  bloc:
    git:
      url: https://github.com/felangel/bloc.git
      ref: bloc_fixes_issue_110
      path: packages/bloc

```

*   url：github 地址
*   ref：表示git引用，可以是 **commit hash, tag** 或者 **branch**
*   path：如果 git 仓库中有多个软件包，则可以使用此属性指定软件包

#### 依赖我们自己的 pub 仓库。

一般大公司都会搭建自己的 pub 仓库，引用自己仓库的方式：

```
dependencies:
  bloc: 
    hosted:
      name: bloc
      url: http://your-package-server.com
    version: ^6.0.0

```

### 依赖覆盖

想象如下场景：项目依赖一个库（比如 path_provider）的版本为 **1.6.22**，而另一个依赖库也依赖这个 path_provider， 但版本为 **0.5.0**，那么我最终到底依赖哪个版本，此时执行 **flutter pub get** 则会出现如下错误：

```
Running "flutter pub get" in flutter_app...                     

Because every version of flutter_plugin from path depends on path_provider ^0.5.0 and flutter_app depends on path_provider ^1.6.22, flutter_plugin from path is forbidden.
So, because flutter_app depends on flutter_plugin from path, version solving failed.
pub get failed (1; So, because flutter_app depends on flutter_plugin from path, version solving failed.)
Process finished with exit code 1

```

![image](https://upload-images.jianshu.io/upload_images/167849-d858451b6da87dd8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

此时要解决这个冲突，可以添加 **dependency_overrides**：

```
dependency_overrides:
  path_provider: ^1.6.22

```

添加此属性后，所有 **path_provider** 插件都会使用同一个最新版本，使用此字段执行 **flutter pub get** 则会出现如下警告：

```
/Users/mengqingdong/project/flutter/bin/flutter --no-color pub get
Running "flutter pub get" in flutter_app...                     

Warning: You are using these overridden dependencies:
! path_provider 1.6.22
Running "flutter pub get" in flutter_app...                         0.5s
Process finished with exit code 0

```

![image](https://upload-images.jianshu.io/upload_images/167849-014978e77734ba13.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### Flutter

Flutter 下面的配置都是 Flutter 的相关配置。

#### uses-material-design

```
flutter:
  uses-material-design: true

```

确保您的应用程序中包含Material Icons字体，以便您可以使用material Icons类中的图标。

#### assets

assets 是对当前资源的配置，比如 图片、字体等。

配置本地图片，使用**Image.asset()** 加载。

```
assets:
  - images/a_dot_burr.jpeg
  - images/a_dot_ham.jpeg

```

配置字体：

```
fonts:
  - family: Schyler
    fonts:
      - asset: fonts/Schyler-Regular.ttf
      - asset: fonts/Schyler-Italic.ttf
        style: italic
  - family: Trajan Pro
    fonts:
      - asset: fonts/TrajanPro.ttf
      - asset: fonts/TrajanPro_Bold.ttf
        weight: 700

```

#### plugin

plugin 配置只存在与插件项目中，package 和 pluginClass 一般是不需要修改的，

```
flutter:
  plugin:
    platforms:
      android:
        package: com.flutter.app_market
        pluginClass: AppMarketPlugin
      ios:
        pluginClass: AppMarketPlugin

```

此配置正常情况下不需要修改，当需要添加新平台适配时，直接添加：

```
flutter:
  plugin:
    platforms:
      android:
        package: com.flutter.app_market
        pluginClass: AppMarketPlugin
      ios:
        pluginClass: AppMarketPlugin
      macos:
        default_package: app_market_macos
      web:
        default_package: app_market_web

```

**pubspec.yaml** 包含应用程序和依赖的软件包，规定Dart和Flutter SDK的版本约束，管理依赖关系并设置Flutter特定的配置。更详细的信息可以转到[pubspec的官方文档查看](https://dart.dev/tools/pub/pubspec)。

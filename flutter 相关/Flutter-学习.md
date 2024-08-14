vscode 使用

![image.png](https://upload-images.jianshu.io/upload_images/167849-c1bd112848b07a0f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


去除垂直标尺(即代码边的线)，文件--》首选项--》设置--》--》搜索“editor.rulers”。将"editor.rulers": [80]  数字删除即可

flutter vscode 插件

Bracket Pair Colorizer 2

vscode-flutter-i18n-json

Awesome flutter sinppets

Image preview

vscode 快捷键

commond + 鼠标左键，跳转到函数

ctrl + - 返回前一个函数

ctrl + shift + - 返回后一个函数位置

flutter devices 终端获取设备id

flutter run -d 设备id 启动控制台

flutter 引用插件方式

pubspec.yaml 文件

//引用 github
```

permission_handler:

    git:

        url: [https://github.com/gongjiehong/permission_handler.git](https://github.com/gongjiehong/permission_handler.git)

flutter_video_compress:

   git:

       url: https://github.com/rurico/flutter_video_compress.git

       ref: noRegift //指定分支

//引用本地

camera:

    path: plugins/camera-0.5.8+2
```

在工程目录下新建文件夹plugins,将需要的插件复制到该文件夹下，并在配置文件添加如上引用即可

![image.png](https://upload-images.jianshu.io/upload_images/167849-037d82f44dd933bf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![image.png](https://upload-images.jianshu.io/upload_images/167849-7d0580a3f661766c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


环境配置

vim ~/.bash_profile

export PATH=/Users/xxf/Documents/flutter/bin:$PATH

export PUB_HOSTED_URL=https://pub.flutter-io.cn

export FLUTTER_STORAGE_BASE_URL=[https://storage.flutter-io.cn](https://storage.flutter-io.cn/)

source ~/.bash_profile

zshrc环境 需要添加

source ~/.bash_profile

source ~/.scripts/zsh-syntax-highlighting/zsh-syntax-highlighting.plugin.zsh // 高亮
zsh-autosuggestions.zsh //历史命令补全

eval "$(thefuck --alias)" //thefuck

setopt no_nomatch

升级Flutter版本

将Flutter SDK下载解压，再将原来flutter 路径 .pub-cache(该文件夹为隐藏文件，需要打开隐藏)  下 的git，hosted文件夹都复制到新的Flutter sdk 下面，注意路径和老的一样，完工

flutter 环境配置.zip
1.3 KB](https://app.yinxiang.com/shard/s51/res/0d2c1346-7ef7-4226-bd42-2489c9880d34/flutter%20%E7%8E%AF%E5%A2%83%E9%85%8D%E7%BD%AE.zip)

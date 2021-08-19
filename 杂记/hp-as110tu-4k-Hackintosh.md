基于opencore 0.6.6

去掉开机日志
config.plist
Misc/Debug/Target 改为 0 即可取出开机日志
默认 67 记录开机日志

因为开启了intel 无线网卡，导致App Store不能登录下载软件，关于本机，wifi 里可以看到![image.png](https://upload-images.jianshu.io/upload_images/167849-486cf7f8d599909f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)，这里如果不是en0，可以按以下方法试试，

打开苹果系统盘根目录下的--> Library (资源库)--> Preferences --> SystemConfiguration 并删除 "NetworkInterfaces.plist"文件，重启电脑，打开设置，网络查看当前连接的网络后面是否如图![image.png](https://upload-images.jianshu.io/upload_images/167849-be2997b5aacccbba.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)，再去登录App Store试试吧，说不定有惊喜哦


最近重新安装了mac catalina 升级big sur的时候，点击安装，完成自动重新启动系统就崩溃，进入了锁屏界面，通过控制台查看日志发现崩溃信息中有coredisplay,我的笔记本是4k的，显示器只能输出40hz，在启动参数中添加了-igfxmpc参数，可以60hz，随后去掉-igfxmpc参数，就成功升级了bir sur，升级完成后在添加了-igfxmpc参数，完成60hz

添加启动项
在使用 BOOTICE 或者 EasyUEFI 添加启动项时需要注意，OpenCore 的启动项应为 \EFI\BOOT\BOOTx64.efi 而不是 \EFI\OC\OpenCore.efi

重建缓存命令
```
sudo kextcache -i /
```
今天用到usb2.0的u盘，插上后发现没有反应，所以定制了USB，可以正常读取2.0的u盘了，特别注意加入USBPorts.kext时，如图红色区域，和别的kext是有区别的，否则可能会有一些莫名其妙的问题
![image.png](https://upload-images.jianshu.io/upload_images/167849-3f05cdd76acaaed7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)






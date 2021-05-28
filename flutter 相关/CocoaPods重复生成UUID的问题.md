今天用pod install的时候出现警告[!] [Xcodeproj] Generated duplicate UUIDs: 占满整个终端,搜索得到结果
[CocoaPods重复生成UUID的问题](http://yangzq007.com/2018/05/28/CocoaPods%E9%87%8D%E5%A4%8D%E7%94%9F%E6%88%90UUID%E7%9A%84%E9%97%AE%E9%A2%98/)
使用第一个没对，参考了增加第二种方法，终于对了
```
//建议放在文件开始或者source之后    
install! 'cocoapods', :deterministic_uuids => false
```
我的是Flutter项目，版本1.17.5，添加位置如图
![WX20200831-141148.png](https://upload-images.jianshu.io/upload_images/167849-3b230731c80d9eee.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

1.20.2,直接添加到末尾即可，如图
![image.png](https://upload-images.jianshu.io/upload_images/167849-153888287f7fba9b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

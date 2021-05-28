[官方文档](https://developer.apple.com/documentation/appstorereceipts/verifyreceipt)

一定要注意验证有两个环境，测试环境用sandbox,

使用postman 测试验证凭据,
![image.png](https://upload-images.jianshu.io/upload_images/167849-97e660fa1168e82d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
如上图，一定要注意这里的参数拼接是json格式，
```
{"receipt-data":"凭证", "password":"App Store connect sharesecret"}
```
拼接好后就可以测试了

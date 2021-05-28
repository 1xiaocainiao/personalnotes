Xcode11.7
所用[资料图片连接](https://koenig-media.raywenderlich.com/uploads/2018/06/CreateMLMaterials.zip)
打开Xcode->Open Developer Tool->CreateML
选择如图
![image.png](https://upload-images.jianshu.io/upload_images/167849-ae0133c7e74678bf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
该文件夹包含需要训练的两个文件夹模型
或者File->New Project->Image Classifier,新建
选择好上图的文件夹点击Train,开始训练模型.
完成后，点击Testing,选择如图
![image.png](https://upload-images.jianshu.io/upload_images/167849-fb9de6dd52130c8e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
开始测试模型
要导出模型，右键MyImageClassifier.mlproj文件，显示包内容，Models文件夹下的MyImageClassifier 1.mlmodel文件就是训练好的模型

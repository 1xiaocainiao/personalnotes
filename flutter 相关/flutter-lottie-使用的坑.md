使用lottie时，UI给的动画资源文件如图
![image.png](https://upload-images.jianshu.io/upload_images/167849-c472288185ace5bd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
选中这两个文件，右键压缩出来的zip文件才能被lottie使用，如果是新建文件夹，将两个文件放入并压缩的，会导致找不到图片路径，代码始终读取不到图片资源

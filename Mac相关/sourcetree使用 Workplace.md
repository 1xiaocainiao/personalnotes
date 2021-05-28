sourcetree使用 Workplace
分支新建，代码不在master下修改，在新建的分支下，修改代码，push到服务器，然后切换回master，并且选中master，然后右键要合并的分支，选择合并到master，在push到服务器

添加子模块，
[image.png](https://upload-images.jianshu.io/upload_images/167849-a2803cfd0be2bef2.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/png)
[image.png](https://upload-images.jianshu.io/upload_images/167849-28419915bbbddd13.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/png)
[image.png](https://upload-images.jianshu.io/upload_images/167849-cc949832fd77e564.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/png)




如上面的图片顺序，添加子模块时，注意最后一张图第一步为子模块 git 远程路径，第二步为本地文件路径，千万不要弄错了

关于Workplace依赖，可先 git clone url（即需要用到的第三方库） 到自己工程目录下，再重复添加子模块

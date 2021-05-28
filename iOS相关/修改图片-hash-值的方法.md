

使用 [ImageMagick](http://www.imagemagick.org/) 对 png 图片做轻量压缩，及不损失图片质量，又可改变图片文件 hash 值。方法：

1.  安装 ImageMagick，`brew install imagemagick`
2.  压缩工程目录下所有 png 文件，`find . -iname "*.png" -exec echo {} \; -exec convert {} {} \;`

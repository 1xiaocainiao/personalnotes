最近做项目时，有个朋友圈类似的界面，发现多张图片时，内存暴增了400M左右，debug发现可能是图片过多造成的，查找图片内存优化发现[此文](https://www.jianshu.com/p/5f844bc7cf51), 于是将  cached_network_image: 2.5.0
升级到2.5.0版本，设置memCacheWidth后内存瞬间降了200+M, 特此记录.

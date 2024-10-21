## Xcode12 新建项目 记录


Xcode 12 新建项目多了SceneDelegate，如果不开发iPadOS多窗口，可以直接删除此文件

1、删除掉info.plist中Application Scene Manifest选项，同时，文件SceneDelegate可删除可不删；

2、AppDelegate.m中SceneDelegate的两个方法相关代码注释掉；

3、AppDelegate中添加属性var window: UIWindow?

didFinishLaunchingWithOptions 中添加如下代码

```jsx
window = UIWindow(frame: UIScreen.main.bounds) window?.backgroundColor = UIColor.white window?.makeKeyAndVisible() let vc = ViewController() window?.rootViewController = vc
```

## 关于新建pch文件

1.  打开你的 Xcode 工程. 在Supporting Files目录下,使用 Command + N 新建一个文件选择 other 下面的 PCH File，PCH 文件名格式建议为 工程名-Prefix.pch，比如：NSLogDemo-Prefix.pch
    
2.  在工程的 Build Settings 里搜索找到 Prefix Header 选项，然后给这个选项配置路径为：项目名称/PCH 文件名，比如：NSLogDemo/NSLogDemo-Prefix.pch
    
3.  将 Precompile Prefix Header 为 YES，预编译后的 PCH 文件会被缓存起来，可以提高编译速度
    
      
    
    ![](https://upload-images.jianshu.io/upload_images/167849-32861b4e1f7f0c7a.png?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)
    
    image.png
    

注意在设置pch文件路径时，使用

```bash
${SRCROOT}/一般为项目名称/Support Files/项目名-Prefix.pch
```

最好不要设置绝对路径，绝对路径别人可能跑步起来

${SRCROOT}[相关文章链接](https://www.jianshu.com/p/53664726d813)  
[新建pch以及NSLog出处](https://links.jianshu.com/go?to=https%3A%2F%2Fxiaovv.me%2F2017%2F05%2F13%2FOC%2520%25E5%2592%258C%2520Swift%2520%25E8%2587%25AA%25E5%25AE%259A%25E4%25B9%2589%25E6%2589%2593%25E5%258D%25B0%25E8%25BE%2593%25E5%2587%25BA%2F)

注意新版Xcode控制台会显示一些无用的log信息，我们一般会用  
Product -> Scheme -> Edit Scheme -> Run -> Arguments -> Environment Variables  
增加 "OS\_ACTIVITY\_MODE" 值为 "disable"，关闭这些无用信息，我这里出现使用这个变量后无法正常打印NSLog信息，所以暂时取消了这个环境变量

/\*\*

-   完美解决Xcode NSLog打印不全的宏 亲测目前支持到9.0版 [解决Xcode NSLog打印不全的宏](https://www.jianshu.com/p/4ceb35fce4ab)

\*/

```cpp
#ifdef DEBUG //#define NSLog(format, ...) printf("class: <%p %s:(%d) > method: %s \n%s\n", self, [[[NSString stringWithUTF8String:__FILE__] lastPathComponent] UTF8String], __LINE__, __PRETTY_FUNCTION__, [[NSString stringWithFormat:(format), ##__VA_ARGS__] UTF8String] ) #define NSLog(...) printf("%f %s\n",[[NSDate date]timeIntervalSince1970],[[NSString stringWithFormat:__VA_ARGS__]UTF8String]); #else #define NSLog(format, ...) #endif
```

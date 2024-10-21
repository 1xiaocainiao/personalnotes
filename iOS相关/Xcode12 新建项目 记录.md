## Xcode12 新建项目 记录

[![](https://upload.jianshu.io/users/upload_avatars/167849/fa5a695cbdb1?imageMogr2/auto-orient/strip|imageView2/1/w/96/h/96/format/webp)](https://www.jianshu.com/u/6e4dacffd230)

0.7092021.07.22 11:36:06字数 455阅读 529

[编辑文章](https://www.jianshu.com/writer#/notebooks/345846/notes/90702708)

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

最后编辑于

：2022.10.18 09:32:21

更多精彩内容，就在简书APP

![](https://upload.jianshu.io/images/js-qrc.png)

"小礼物走一走，来简书关注我"

还没有人赞赏，支持一下

[![  ](https://upload.jianshu.io/users/upload_avatars/167849/fa5a695cbdb1?imageMogr2/auto-orient/strip|imageView2/1/w/100/h/100/format/webp)](https://www.jianshu.com/u/6e4dacffd230)

-   序言：七十年代末，一起剥皮案震惊了整个滨河市，随后出现的几起案子，更是在滨河造成了极大的恐慌，老刑警刘岩，带你破解...
    
    [![](https://upload.jianshu.io/users/upload_avatars/15878160/783c64db-45e5-48d7-82e4-95736f50533e.jpg?imageMogr2/auto-orient/strip|imageView2/1/w/48/h/48/format/webp)沈念sama](https://www.jianshu.com/u/dcd395522934)阅读 199,519评论 5赞 468
    
-   序言：滨河连续发生了三起死亡事件，死亡现场离奇诡异，居然都是意外死亡，警方通过查阅死者的电脑和手机，发现死者居然都...
    
-   文/潘晓璐 我一进店门，熙熙楼的掌柜王于贵愁眉苦脸地迎上来，“玉大人，你说我怎么就摊上这事。” “怎么了？”我有些...
    
-   文/不坏的土叔 我叫张陵，是天一观的道长。 经常有香客问我，道长，这世上最难降的妖魔是什么？ 我笑而不...
    
-   正文 为了忘掉前任，我火速办了婚礼，结果婚礼上，老公的妹妹穿的比我还像新娘。我一直安慰自己，他们只是感情好，可当我...
    
    [![](https://upload.jianshu.io/users/upload_avatars/4790772/388e473c-fe2f-40e0-9301-e357ae8f1b41.jpeg?imageMogr2/auto-orient/strip|imageView2/1/w/48/h/48/format/webp)茶点故事](https://www.jianshu.com/u/0f438ff0a55f)阅读 62,646评论 5赞 359
    
-   文/花漫 我一把揭开白布。 她就那样静静地躺着，像睡着了一般。 火红的嫁衣衬着肌肤如雪。 梳的纹丝不乱的头发上，一...
    
-   那天，我揣着相机与录音，去河边找鬼。 笑死，一个胖子当着我的面吹牛，可吹牛的内容都是我干的。 我是一名探鬼主播，决...
    
-   文/苍兰香墨 我猛地睁开眼，长吁一口气：“原来是场噩梦啊……” “哼！你这毒妇竟也来了？” 一声冷哼从身侧响起，我...
    
-   序言：老挝万荣一对情侣失踪，失踪者是张志新（化名）和其女友刘颖，没想到半个月后，有当地人在树林里发现了一具尸体，经...
    
-   正文 独居荒郊野岭守林人离奇死亡，尸身上长有42处带血的脓包…… 初始之章·张勋 以下内容为张勋视角 年9月15日...
    
    [![](https://upload.jianshu.io/users/upload_avatars/4790772/388e473c-fe2f-40e0-9301-e357ae8f1b41.jpeg?imageMogr2/auto-orient/strip|imageView2/1/w/48/h/48/format/webp)茶点故事](https://www.jianshu.com/u/0f438ff0a55f)阅读 35,268评论 2赞 317
    
-   正文 我和宋清朗相恋三年，在试婚纱的时候发现自己被绿了。 大学时的朋友给我发了我未婚夫和他白月光在一起吃饭的照片。...
    
    [![](https://upload.jianshu.io/users/upload_avatars/4790772/388e473c-fe2f-40e0-9301-e357ae8f1b41.jpeg?imageMogr2/auto-orient/strip|imageView2/1/w/48/h/48/format/webp)茶点故事](https://www.jianshu.com/u/0f438ff0a55f)阅读 37,299评论 1赞 329
    
-   序言：一个原本活蹦乱跳的男人离奇死亡，死状恐怖，灵堂内的尸体忽然破棺而出，到底是诈尸还是另有隐情，我是刑警宁泽，带...
    
-   正文 年R本政府宣布，位于F岛的核电站，受9级特大地震影响，放射性物质发生泄漏。R本人自食恶果不足惜，却给世界环境...
    
    [![](https://upload.jianshu.io/users/upload_avatars/4790772/388e473c-fe2f-40e0-9301-e357ae8f1b41.jpeg?imageMogr2/auto-orient/strip|imageView2/1/w/48/h/48/format/webp)茶点故事](https://www.jianshu.com/u/0f438ff0a55f)阅读 38,591评论 3赞 303
    
-   文/蒙蒙 一、第九天 我趴在偏房一处隐蔽的房顶上张望。 院中可真热闹，春花似锦、人声如沸。这庄子的主人今日做“春日...
    
-   文/苍兰香墨 我抬头看了看天上的太阳。三九已至，却和暖如春，着一层夹袄步出监牢的瞬间，已是汗流浃背。 一阵脚步声响...
    
-   我被黑心中介骗来泰国打工， 没想到刚下飞机就差点儿被人妖公主榨干…… 1. 我叫王不留，地道东北人。 一个月前我还...
    
-   正文 我出身青楼，却偏偏与公主长得像，于是被迫代替她去往敌国和亲。 传闻我的和亲对象是个残疾皇子，可洞房花烛夜当晚...
    
    [![](https://upload.jianshu.io/users/upload_avatars/4790772/388e473c-fe2f-40e0-9301-e357ae8f1b41.jpeg?imageMogr2/auto-orient/strip|imageView2/1/w/48/h/48/format/webp)茶点故事](https://www.jianshu.com/u/0f438ff0a55f)阅读 41,871评论 2赞 341
    

### 被以下专题收入，发现更多相似内容

投稿管理
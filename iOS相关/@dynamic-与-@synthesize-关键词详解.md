@dynamic 与 @synthesize 关键词详解
http://www.learn-cocos2d.com/2011/10/complete-list-objectivec-20-compiler-directives 详细

今天开发的过程中，第一次自己遇到需要使用

@dynamic

关键词的场景，之前@dynamic只在NSManagedObject的子类中遇到过，因为NSManagedObject的子类是由CoreData直接生成的，其中对应参数(@property)的setter和getter方法也是由CoreData直接生成，并且不展现给你。

Setter & Getter

首先介绍一下什么是setter和getter方法：

由名字也大致能猜出

getter方法是当你的程序某处读取一个参数A的时候，会调用的方法，它会返回当前A的值

setter方法是当你的程序某处给参数A赋值的时候，会调用的方法，把新值赋值给变量A

接下来，我们看一个标准的setter&&getter方法

@interfaceSample()@property(nonatomic,strong,readwrite)NSObject*sampleObject;@end@implementationSample@synthesizesampleObject = _sampleObject;//getter- (NSObject*)sampleObject{return_sampleObject;}//setter- (void)setSampleObject:(NSObject*)sampleObject{    _sampleObject = sampleObject;}@end

以上就是一个比较标准的setter以及getter方法

其中用到了我们要讲的一个关键词

@synthesize

synthesize中文意思为‘合成’，在编译的过程中，编译器会帮你自动生成getter和setter方法，也就是说，上述代码中，把

-(NSObject*)sampleObject-(void)setSampleObject:(NSObject*)sampleObject

两个函数的实现删除掉也是没有关系的。因为@synthesize语法糖会让编译器帮助你生成getter和setter方法

而现在的编译器（XCode6），即使你不写@synthesize，它同样会自动帮你生成getter和setter方法，但是具体是从哪个版本开始的我还没有查到。

而语法糖@synthesize的写法也很有深意

@synthesizesampleObject = _sampleObject;

可以看出sampleObject是我们的参数名称,而_sampleObject呢？

_sampleObject的下划线只是一种常用的命名规范，因为当你不写@synthesize的时候，编译器自动为你生成getter和setter方法中，你可以直接通过_xxx的形式来调用getter方法。你当然可以使用其他名字。

@dynamic

于是就到了今天主要要讲的@dynamic关键词。之前也说到了，这个关键词用的不多，最常见的地方还是在CoreData的NSManagedObject中会看见。

@dynamic A相当于告诉编译器：“参数A的getter和setter方法并不在此处，而在其他地方实现了或者生成了，当你程序运行的时候你就知道了，所以别警告我了”这样程序在运行的时候，对应参数的getter和setter方法就会在其他地方去寻找，比如父类。

举一个例子吧

父类

@interfacefather()@property(nonatomic,strong,readwrite)NSObject*sampleObject;...@synthesizesampleObject = _sampleObject;@end

子类

@interfacechild: father@property(nonatomic, strong, readwrite) NSObject *sampleObject;...@dynamicsampleObject;@end

这样的话，如果你在子类中调用sampleObject，则会调用父类的getter方法。

何时用到

比如类遵守一个delegate时，delegate中的参数在父类的初始化方法中就赋值了，而子类的没有自己的初始化方法的时候，子类中的此参数就可以设为@dynamic，即和父类共用一个参数

如果有什么错误，欢迎指出！

转载自 http://suree.org/2015/09/01/Dynamic-Synthesize/

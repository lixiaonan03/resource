# IOS初学的一些整理(OC 相关的)
### !!!oc的基础语法和介绍
1、https://github.com/qinjx/30min_guides/blob/master/ios.md

### 官方文档
1、开发者中文文档 https://developer.apple.com/cn/documentation/



## 代理和协议相关：
  代理就是委托模式 协议就是接口
  定义协议在调用的类.h  中(注意要用弱引用)   类似安卓在adapter 中创建一个条目点击监听并生成一个监听listner对象
  比如：
```  IOS
@interface ImageViewDemoVC ()
@property(nonatomic,strong) CircleImageView *circleImageView;
@end

@interface BBTSplashVC : UIViewController
@property(nonatomic,weak) id <BBTSplashVCDelegate> splashVCDelegate;
@end
```

  调用者在 .m 中 (注意判断这个类是否实现)   类似安卓在adapter 中判断这个监听是否被set(不为空)了 并调用listner.某个方法
```  IOS
if ([self.splashVCDelegate respondsToSelector:@selector(userDidTouchedSplashVCwithUri:)]) {
   [self.splashVCDelegate userDidTouchedSplashVCwithUri:self.uri];
}
```
  实现在另个继承这个协议的类中 (IOS只有通过类实现 没有同过匿名内部类创建的方式) 类似于安卓在 activity创建adapter时 给这个adapter 设置一个匿名内部类listner对象


##  block对象（注意使用弱引用）  多用在类似java匿名内部类实现中

  block 对象类似java中的Runable对象  block对于外部变量，默认是只读属性 要使用外部变量(加入这个) __block int a;
  block定义    返回值类型 (^block变量名) （参数列表）=^(参数列表){}；
  block的调用  block变量名(实参)


## 多线程
OGC 同步执行和异步执行 串行队列和并行队列的
概念解释 https://juejin.cn/post/6844903566398717960

同步执行：同步添加任务到指定的队列中，在添加的任务执行结束之前，会一直等待，直到队列里面的任务完成之后再继续执行。
        只能在当前线程中执行任务，不具备开启新线程的能力。

异步执行：异步添加任务到指定的队列中，它不会做任何等待，可以继续执行任务。
        可以在新的线程中执行任务，具备开启新线程的能力。

串行队列：每次只有一个任务被执行。让任务一个接着一个地执行。（只开启一个线程，一个任务执行完毕后，再执行下一个任务）

并行队列：可以让多个任务并发（同时）执行。（可以开启多个线程，并且同时执行任务）

使用：1、先创建一个队列 2、将任务追加到任务的等待队列中，然后系统就会根据任务类型执行任务（同步执行或异步执行）。


练习:https://blog.csdn.net/u014600626/article/details/90265061

NSOperation与 NSOperationQueue 是苹果提供的一套面向对象的基于 GCD 封装的多线程解决方案。
https://www.jianshu.com/p/d8caf596d5d0

## 变量修饰符
https://www.jianshu.com/p/64866e2d5394

copy与strong类似。不同之处是strong的复制是多个指针指向同一个地址，而copy的复制每次会在内存中拷贝一份对象，指针指向不同地址。copy一般用在修饰有可变对应类型的不可变对象上，如NSString, NSArray, NSDictionary。

## UI属性的
1. 基础UI组件
+ 1、UILable   https://www.jianshu.com/p/3b95e8f649a5
+ 2、UIButton  https://www.jianshu.com/p/0d0d394d0f2c

2. 动画
动画学习  1、(序列帧动画) 2、UIView动画 3、核心动画的
https://www.jianshu.com/p/94f047efee6d

## 第三方jar包管理 (类似安卓的 build gradle文件的)
刚开始创建的项目是没有这个 build文件的 生成处理步骤
+ 1、在项目根目录中创建  Podfile 文件
+ 2、在项目中编辑
```  IOS
 //项目最低兼容的IOS版本
 platform :ios, '8.0'
 // ocDemo 更换为项目名称
 target 'ocDemo' do
  //引入的第三方包
  pod 'Masonry', '1.1.0'
 end
```
+ 3、在项目的根目录下 命令行执行 pod install
+ 4、执行成功之后 项目根目录下会出现  项目名.xcworkspace  的文件(原来只有一个 .xcodeproj)   点击这个文件打开工程

## 常用的项目框架
+ 1、[约束布局框架的Masonry](https://github.com/SnapKit/Masonry)
+ 2、[JSON和model之间的转换的](https://github.com/CoderMJLee/MJExtension)

有点类似fastJson 但是注意：因为oc中的array没法指定类型，所以当一个模型(也就是类)中个array数组，并且其中array中的类型不是基础类型的时候，就需要实现方法  mj_ objectClassInArray  告诉系统这个array中是啥对象 （写在.m）中就行
```  IOS
+ (NSDictionary *)mj_ objectClassInArray{
  //statuses 就是Json中对应的key    Status 就是对应的那个类的
  return @{ @"statuses" : @"Status", @"ads" : @"Ad" };
}
```
+ 3、[网络库使用的AFNetworking](https://github.com/AFNetworking/AFNetworking)
+ 4、[图片加载库的SDWebImage](https://github.com/SDWebImage/SDWebImage)
+ 5、[简化文件处理的FCFileManager](https://github.com/fabiocaccamo/FCFileManager)
+ 6、[处理键盘弹出对界面影响的问题IQKeyboardManager](https://github.com/hackiftekhar/IQKeyboardManager)
+ 7、[第三方刷新框架MJRefresh](https://github.com/CoderMJLee/MJRefresh)
+ 8、

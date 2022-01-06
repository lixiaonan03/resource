# 自己平常整理的一些资源链接和思路

## [面试学习相关的链接](/面试学习/study.md)

## Android整体知识

* [Android官方培训课程中文版](https://github.com/kesenhoo/android-training-course-in-chinese)
* [Github上比较火的开源项目集合](https://github.com/open-android/Android)（有链接和视频）
* [强大易用的安卓工具类库AndroidUtilCode](https://github.com/Blankj/AndroidUtilCode) （可从里面找一些工具类）

* [Android校招面试指南](https://github.com/LRH1993/android_interview) （常看看）
* [leetcode 图形化解释](https://github.com/MisterBooo/LeetCodeAnimation)(刷算法必备)

* [分类 Android 开源大全AndroidLibs](https://github.com/XXApple/AndroidLibs) （可从里面找一些资源）
* [小知识点根据字母排序Android-Tips](https://github.com/tangqi92/Android-Tips)

* [国内 Android 设备 / ROM 兼容性问题反馈与跟踪](https://github.com/android-in-china/Compatibility)

## 框架搭建
* [可配置化的整合了主流框架的MVPArms框架](https://github.com/JessYanCoding/MVPArms) （和<a href="#auto">AutoSize适配</a>框架的作者是同一个）

* [基于谷歌最新AAC架构，MVVM设计模式的一套快速开发库MVVMHabit](https://github.com/goldze/MVVMHabit)
  #### Rx思想系列
* [Rx学习RxJava2Examples](https://github.com/nanchen2251/RxJava2Examples)
  #### 组件化
* [阿里的组件化路由ARouter](https://github.com/alibaba/ARouter)
  #### 适配框架
* [今日头条的适配框架<a name="auto">AndroidAutoSize</a>](https://github.com/JessYanCoding/AndroidAutoSize)
  #### 图片处理
* [图片压缩Luban框架](https://github.com/Curzibn/Luban)
  #### 后台任务处理
* [印象笔记的后台任务android-job](https://github.com/evernote/android-job)
  #### 版本更新
* [APP版本更新的框架AppUpdate](https://github.com/WVector/AppUpdate) （已停止更新 可参考另一）
* [参考AppUpdate实现的XUpdate](https://github.com/xuexiangjys/XUpdate) （上一个已停止更新可参考这个）

* [链接调用的更新框架CheckVersionLib](https://github.com/AlexLiuSheng/CheckVersionLib) （这个相比前2个使用简单）
  #### webview处理
* [对webview封装的一个好的库](https://github.com/Justson/AgentWeb)
  #### 热更新
* [腾讯热更新tinker](https://github.com/Tencent/tinker)

## 网络模块

* [基于RxJava2+Retrofit2的网络请求框架RxEasyHttp](https://github.com/zhou-you/RxEasyHttp)

## 图片加载模块

* [扩展glide框架支持webp格式gif的库](https://github.com/zjupure/GlideWebpDecoder)


## UI模块

* [牛逼的下拉刷新框架SmartRefreshLayout](https://github.com/scwang90/SmartRefreshLayout) （目前下拉刷新用这个就行，如果需要国家化可直接添加value）

* [腾讯出的QMUI_Android整合框架](https://github.com/Tencent/QMUI_Android) （里面有些UI可参考）

* [新用户引导层的库NewbieGuide](https://github.com/huburt-Hu/NewbieGuide) （做应用是第一次进入做引导指引）

* [滑动选择框架AndroidPicker](https://github.com/gzu-liyujiang/AndroidPicker) （集成是根据需求集成、注意存储权限）

* [轮播图框架MZBannerView](https://github.com/pinguo-zhouwei/MZBannerView)

  #### 通知栏
* [通知栏使用NotifyUtil](https://github.com/wenmingvs/NotifyUtil)
  #### 图片处理
* [大图慢慢自己移动的框框KenBurnsView](https://github.com/flavioarfaria/KenBurnsView) （闪屏页可以使用，参考soul应用的闪屏页）
  #### 照相机使用
* [google官方的照相机使用demo](https://github.com/google/cameraview)
* [仿微信照相机的实现](https://github.com/CJT2325/CameraView)
* [老外写的自定义照相、摄像实现](https://github.com/natario1/CameraView)（目前项目使用的这个，有相关的api文档可参考使用）
  #### 状态栏
* [处理状态栏和输入法弹框的ImmersionBar](https://github.com/gyf-dev/ImmersionBar) （star数比较多 可参考学习）
* [一款方便的设置状态栏和导航栏的各种效果的框架](https://github.com/Zackratos/UltimateBarX)

  #### 自定义view
* [背景水波纹效果MultiWaveHeader](https://github.com/scwang90/MultiWaveHeader)
* [任意位置悬浮的按钮FloatWindow](https://github.com/yhaolpz/FloatWindow)
     列表
* [RecyclerView实现顶部悬浮效果](https://github.com/Gavin-ZYX/StickyDecoration)
     键盘
* [自定义安全键盘CustomizeKeyboard](https://github.com/StomHong/CustomizeKeyboard)
     日历相关
* [支持自定义效果的日历](https://github.com/huanghaibin-dev/CalendarView) (star数最多，可自定义效果)
* [仿小米日历](https://github.com/xiaojianglaile/Calendar)
    手势密码
* [仿支付宝手势密码解锁LockPattern](https://github.com/sym900728/LockPattern)
    刻度尺和图表总结
* [报表统计的MPAndroidChart](https://github.com/PhilJay/MPAndroidChart)
* [自定义尺子收集demo](https://github.com/dalong982242260/AndroidRuler)

  #### 网络错误页面加载或loading加载
* [根据stat状态区分不同的](https://github.com/Zhao-Yan-Yan/MultiStatePage)
* [自定义修改底层View的 可学习的](https://github.com/nukc/StateView)



## IO存储模块

* [微信出的高性能 key-value 存储组件MMKV](https://github.com/Tencent/MMKV)

## 性能监控模块

* [微信的性能监控框架Matrix ](https://github.com/Tencent/matrix)

* [滴滴的研发助手框架DoraemonKit ](https://github.com/didi/DoraemonKit)(开发中可使用这个)

* [360的性能监控框架ArgusAPM](https://github.com/Qihoo360/ArgusAPM)

* [崩溃实时显示的SpiderMan](https://github.com/simplepeng/SpiderMan)

* [轻量级自动化埋点方案](https://github.com/luojilab/DDAutoTracker) （待验证效果可以参考AOP面向切面思想）

* [微信的资源混淆方案](https://github.com/shwenzhang/AndResGuard)

## 其他模块

* [好用的一个loggat框架](https://github.com/orhanobut/logger)
* [可以查看SDK中隐藏类的一种方式](https://github.com/anggrayudi/android-hidden-api)


## 联系方式
* QQ: 472379153
* 微信: lxn1551309

  ![lxn1551309](/img/weixin.jpeg)

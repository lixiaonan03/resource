## 关于flutter_boost的集成使用
集成文档地址(https://github.com/alibaba/flutter_boost)

使用文档(https://github.com/alibaba/flutter_boost/blob/master/README_CN.md)


##### 1、新建或引入flutter module 项目

新建：在项目同级的目录下创建flutter moule (注意是项目同级的目录下 有可能flutter项目和android项目不是一个仓库)
  命令：
  ```
  flutter create -t module 项目名字
  ```
已有项目:如果是从已有仓库down的项目,则使用命令生成编译文件和依赖文件

第一步:打开项目目录
  ```
cd /Users/lixiaonan/Documents/workspace-android/bonbonwork0821/wanwu_flutter/
  ```

第二步:命令生成编译文件和依赖文件
  ```
flutter pub get
  ```

##### 2、把flutter项目依赖到android项目中
做法在 setting.gradle结尾处添加如下代码，注意flutter_module路径要与创建的模块相对路径对应（路劲不要写错）
  ```
setBinding(new Binding([gradle: this]))
evaluate(new File(
        settingsDir.parentFile,
        '/flutter_module/.android/include_flutter.groovy'
))
  ```

##### 3、在flutter项目中引入flutterBoost  框架(注意版本号的区别)

  ```
flutter_boost:
  git:
    url: 'https://github.com/alibaba/flutter_boost.git'
    ref: 'v1.12.13-hotfixes’
 ```
之后同步flutter的包引入

##### 4、在android的项目app中引入flutter lib工程
先引入flutter module工程（注意不要改名字）
  ```
implementation project(':flutter’)
  ```
再用gradle同步项目之后再引入flutter_boost
  ```
implementation project(':flutter_boost')
  ```
##### 5、处理android 配置文件的
```  xml
<activity
       android:name="com.idlefish.flutterboost.containers.BoostFlutterActivity"
       android:theme="@style/Theme.AppCompat"
       android:configChanges="orientation|keyboardHidden|keyboard|screenSize|locale|layoutDirection|fontScale|screenLayout|density"
       android:hardwareAccelerated="true"
       android:windowSoftInputMode="adjustResize" >
       <meta-data android:name="io.flutter.embedding.android.SplashScreenDrawable" android:resource="@drawable/page_loading"/>
</activity>


<meta-data android:name="flutterEmbedding"
           android:value="2"> </meta-data>
```
##### 6、application中初始化配置
```  Java
//flutter 加入的
FlutterMain.startInitialization(this);
initFlutterBoost();

/**
     * 初始化flutter 控件的
     */
    private void initFlutterBoost() {
        INativeRouter router = new INativeRouter() {
            @Override
            public void openContainer(Context context, String url, Map<String, Object> urlParams, int requestCode, Map<String, Object> exts) {
                //跳转的一些url处理
                String assembleUrl = Utils.assembleUrl(url, urlParams);
                PageRouter.openPageByUrl(context, assembleUrl, urlParams);
            }
        };
        FlutterBoost.BoostLifecycleListener boostLifecycleListener = new FlutterBoost.BoostLifecycleListener() {
            @Override
            public void onEngineCreated() {
                BoostPluginRegistry boostPluginRegistry = new BoostPluginRegistry(FlutterBoost.instance().engineProvider());
                //注册一些插件的
            }

            @Override
            public void onPluginsRegistered() {

            }

            @Override
            public void onEngineDestroy() {

            }

        };
        //
        // AndroidManifest.xml 中必须要添加 flutterEmbedding 版本设置
        //
        //   <meta-data android:name="flutterEmbedding"
        //               android:value="2">
        //    </meta-data>
        // GeneratedPluginRegistrant 会自动生成 新的插件方式　
        //
        //
        Platform platform = new FlutterBoost
                .ConfigBuilder(this, router)
                .isDebug(true)
                .whenEngineStart(FlutterBoost.ConfigBuilder.ANY_ACTIVITY_CREATED)
                .renderMode(FlutterView.RenderMode.texture)
                .lifecycleListener(boostLifecycleListener)
                .build();
        FlutterBoost.instance().init(platform);
    }
```

##### 7、参考demo的路由处理的

```  Java
public class PageRouter {
    public final static Map<String, String> pageName = new HashMap<String, String>() {{
        put("second", "second");
        put("tab", "tab");
        put("sample://flutterPage", "flutterPage");
    }};

    public static final String NATIVE_PAGE_URL = "exampleViewController";
    public static final String FLUTTER_PAGE_URL = "sample://flutterPage";
    public static final String FLUTTER_FRAGMENT_PAGE_URL = "sample://flutterFragmentPage";

    public static boolean openPageByUrl(Context context, String url, Map params) {
        return openPageByUrl(context, url, params, 0);
    }

    public static boolean openPageByUrl(Context context, String url, Map params, int requestCode) {
        String path = url.split("\\?")[0];
        try {
            if (pageName.containsKey(path)) {
                Intent intent = BoostFlutterActivity.withNewEngine().url(pageName.get(path)).params(params)
                        .backgroundMode(BoostFlutterActivity.BackgroundMode.opaque).build(context);
                if (context instanceof Activity) {
                    Activity activity = (Activity) context;
                    activity.startActivityForResult(intent, requestCode);
                } else {
                    context.startActivity(intent);
                }
                return true;
            } else if (url.startsWith(FLUTTER_FRAGMENT_PAGE_URL)) {
                context.startActivity(new Intent(context, FlutterFragmentPageActivity.class));
                return true;
            } else if (url.startsWith(NATIVE_PAGE_URL)) {
                context.startActivity(new Intent(context, NativePageActivity.class));
                return true;
            }

            return false;

        } catch (Throwable t) {
            return false;
        }
    }
}

```

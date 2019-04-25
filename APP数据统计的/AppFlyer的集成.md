## 关于AppFlyer的集成使用
集成文档地址(https://support.appsflyer.com/hc/zh-cn)

Android集成步骤

1、在工程项目build文件中加入
  ``` xml
    repositories {
      mavenCentral()
    }
  ```
  在项目中builde 文件中加入
  ``` xml
   dependencies {
   implementation 'com.appsflyer:af-android-sdk:4+@aar'

   //如果需要支持 Google Play Install referrer API,必须添加,使用此 API 可提高归因的准确性，能有效预防安装作弊等现象。
   implementation 'com.android.installreferrer:installreferrer:1.0'
   }

  ```
2、添加权限和广播接受器

``` xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<!-- Optional : -->
<uses-permission android:name="android.permission.READ_PHONE_STATE" />


  <receiver
           android:name="com.appsflyer.SingleInstallBroadcastReceiver"
           android:exported="true">
           <intent-filter>
               <action android:name="com.android.vending.INSTALL_REFERRER"/>
           </intent-filter>
   </receiver>
```
3、SDK初始化

   在 onCreate() 中完成初始化
   ``` Java
   AppsFlyerConversionListener conversionDataListener = new AppsFlyerConversionListener() {
         @Override
         public void onInstallConversionDataLoaded(Map<String, String> map) {
             if (map.containsKey("media_source")) {
                 //这个值是安装渠道来源 用这个可以处理一些业务逻辑
                 String mediaSource = map.get("media_source");
             }
         }
         @Override
         public void onInstallConversionFailure(String s) {
         }
         @Override
         public void onAppOpenAttribution(Map<String, String> map) {
         }
         @Override
         public void onAttributionFailure(String s) {
         }
     };
     AppsFlyerLib.getInstance().init("自己的appflyerKey值（统一账号底下的key值是相同的）", conversionDataListener,
             getApplicationContext());
     AppsFlyerLib.getInstance().startTracking(this);

   ```
4、应用内事件的统计（可选功能）
  统计一些应用内事件点击的次数
  ``` Java
   Map<String, Object> eventValue = new HashMap<>();
   eventValue.put("pid",mPid);//加的一些参数
   AppsFlyerLib.getInstance().trackEvent(getApplicationContext(), "事件名称", eventValue);
  ```

5、混淆处理
   ``` xml
     -keep class com.appsflyer.** { *; }
   ```

6、如果需要写死渠道来源  [官方文档地址](https://support.appsflyer.com/hc/en-us/articles/207032166-Configuring-and-Testing-Pre-Installs-Campaigns-for-Android#Setup)
   ```xml
   <meta-data android:name="AF_PRE_INSTALL_NAME" android:value="daichao_int"/>
   ```
   其中 value 值填写死的广告平台pid(一般都是 _int 结尾)

### 广告平台的账号申请


 [对接文档地址](https://www.evernote.com/shard/s374/client/snv?noteGuid=3c272532-5916-46b7-8a1a-ca29af83b8f9&noteKey=4e6efceebd6c751b&sn=https%3A%2F%2Fwww.evernote.com%2Fshard%2Fs374%2Fsh%2F3c272532-5916-46b7-8a1a-ca29af83b8f9%2F4e6efceebd6c751b&title=AppsFlyer%25E5%25B9%25BF%25E5%2591%258A%25E5%25B9%25B3%25E5%258F%25B0%25E8%25B4%25A6%25E5%258F%25B7%25E6%25B3%25A8%25E5%2586%258C%25E5%258F%258A%25E5%259F%25BA%25E6%259C%25AC%25E4%25BD%25BF%25E7%2594%25A8%25E6%258C%2587%25E5%258D%2597)

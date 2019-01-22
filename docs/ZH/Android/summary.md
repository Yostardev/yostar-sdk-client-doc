## 概述

AiriSDK主要用来向第三方应用程序提供方便快捷的、适合海外地区玩家使用的登陆及支付服务。本文主要描述SDK相关接口的使用方法，供使用原生Android进行开发的应用程序提供商直接接入使用。

## 阅读对象
本文档面向具有一定Android开发基础的开发与管理人员。

## SDK集成

在您的项目中，打开 ```your_app | Gradle Scripts | build.gradle (Project)``` 并添加以下存储库到 ```buildscript { repositories {}}``` 部分，以便从Maven 中央存储库下载 SDK：

```gradle
maven {
    url 'http://123.206.215.231/repository/maven-releases/'
}
```

在您的项目中，打开 ```your_app | Gradle Scripts | build.gradle (Module: app)``` 并添加以下一段执行语句至 ```dependencies{}``` 部分

```gradle
implementation 'com.airisdk.sdkcall:airisdk:2.1.0'
```

构建项目。

## 编辑您的资源和清单

### Assets资源

AiriSDK的环境资源和日志开关等参数都是由```assets/AiriSDKConf.properties```文件中的参数控制，请开发者设置一下参数：

参数值请联系悠星商务进行获取。

| 参数名称 | 参数说明 | 是否必须 |
| ------ | ------ | ------ |
| AIRISDK_URL | 分配的AiriSDK服务器访问地址 | 是 |
| AIRISDK_PAYSTOREID | 游戏支持的支付方式，默认为googleplay | 是 |
| AIRISDK_SHOWDEBUGLOG | AiriSDK日志打印，默认为false，不打印 | 是 |
| AIRISDK_NEWDEVICE | 是否将当前机器当作全新的机器使用，默认为false | 是 |

### AndroidManifeset配置

#### 客服系统

AiriSDK集成了Helpshift作为客服管理工具，所以在Package Explorer中，打开安卓项目的AndroidManifest.xml。在<application>元素中添加以下 meta-data 标签，配置对应的Helpshift参数。

获取参数值请咨询悠星商务人员。

```xml
<meta-data android:name="helpshift_apiKey" android:value="xxxxxxx" />
<meta-data android:name="helpshift_demain" android:value="xxxxx" />
<meta-data android:name="helpshift_appId" android:value="xxxxxxxxxxx" />
```

### AU支付权限

AiriSDK也集成了AU支付渠道，如果您的游戏有AU支付的需求，请在AndroidManifeset.xml文件中添加以下权限：

```xml
<uses-permission android:name="com.kddi.market.permission.USE_ALML" />
```


### res资源配置

AiriSDK集成了firebase的部分功能，需要在```res/values/google_service_strings.xml```中配置firebase服务参数。

获取参数值请咨询悠星商务人员。

```xml
<string name="default_web_client_id">***</string>
<string name="fcm_fallback_notification_channel_label">****</string>
<string name="firebase_database_url">*****</string>
<string name="gcm_defaultSenderId">*****</string>
<string name="google_api_key">******</string>
<string name="google_app_id">******</string>
<string name="google_crash_reporting_api_key">******</string>
<string name="google_storage_bucket">*****</string>
<string name="project_id">*****</string>
```

## 接口设计说明

#### demo工程源码目录

https://github.com/Yostardev/yostar-sdk-android

接入过程您可以查看demo工程作为参考。

### 初始化接口

以下所有接口必须在初始化完成后调用。

#### 调用API
```java
void initSDK(Activity activity, AiriSDKConnect.InitResultCallback callback)
```
#### 调用实例
```java
 AiriSDKInstance.getInstance().initSDK(MainActivity.this,new AiriSDKConnect.InitResultCallback() {
            @Override
            public void onSuccess(boolean isVirtual) {
                MainActivity.setResultTv("初始化成功 - 是否为模拟器:" + isVirtual) ;
            }

            @Override
            public void onFail(ErrorEntity entity) {
                MainActivity.setResultTv("初始化失败" ) ;
            }
        });
```
#### 接口参数说明

| 参数名称 | 参数说明 | 是否必须 |
| ------ | ------ | ------ |
| Activity | 程序上下文 | 是 |
| AiriSDKConnect.InitResultCallback | 初始化结果回调 | 是 |

#### 回调参数说明

| 参数名称 | 参数说明 |
| ------ | ------ | 
| isVirtual | 当前机器是否为模拟器 |
| ErrorEntity | 错误日志类，entity.CODE()为错误码，错误详情请查看错误码表 |

### 设备号获取

#### 调用API

```java
String SDKGetDeviceID()
```
#### 调用实例
```java
AiriSDKInstance.getInstance().SDKGetDeviceID()
```

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
                MainActivity.setResultTv("Initialization was successful. Is it an emulator:" + isVirtual) ;
            }

            @Override
            public void onFail(ErrorEntity entity) {
                MainActivity.setResultTv("Initialization failed." ) ;
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

### 打开客服界面

#### 调用API
```java
void SDKOpenHelpShift()
```
#### 调用实例
```java
AiriSDKInstance.getInstance().SDKOpenHelpShift();
```
### 快速登陆

#### 调用API
```java
void SDKQuickLogin(AiriSDKConnect.LoginResultCallback callback)
```
#### 调用实例
```java
AiriSDKConnect.LoginResultCallback loginResultCallback = new AiriSDKConnect.LoginResultCallback() {
            @Override
            public void onSuccess(AiriLoginEntity entity) {
                MainActivity.showSettingLayout();
                MainActivity.setResultTv("Login successfully.");
                if (entity.isCanBindGuest()){ //Whether the landing account can be bound to the local tourist account.
                    AlertDialog.Builder builder = new AlertDialog.Builder(AiriSDK.instance);
                    builder.setTitle("Prompt:");
                    builder.setMessage("Whether to bind?");
                    builder.setIcon(R.mipmap.ic_launcher_round);
                    builder.setCancelable(true);
                    builder.setPositiveButton("YES", new DialogInterface.OnClickListener() {
                        @Override
                        public void onClick(DialogInterface dialog, int which) {
                            //Call SDKNewAccountLink interface
                        }
                    });
                    builder.setNegativeButton("NO", new DialogInterface.OnClickListener() {
                        @Override
                        public void onClick(DialogInterface dialog, int which) {
                            dialog.dismiss();
                        }
                    });
                    AlertDialog dialog = builder.create();
                    dialog.show();
                }

            }

            @Override
            public void onFail(ErrorEntity entity) {
                MainActivity.setResultTv("Login failed:" + entity.toString());
            }
        } ;
AiriSDKInstance.getInstance().SDKQuickLogin(loginResultCallback);
```
#### 接口参数说明

| 参数名称 | 参数说明 | 是否必须 |
| ------ | ------ | ------ |
| AiriSDKConnect.LoginResultCallback | 登陆结果回调 | 是 |

### 回调参数说明

| 参数名称 | 参数说明 |
| ------ | ------ | 
| ErrorEntity | 错误日志类，entity.CODE()为错误码，错误详情请查看错误码表 |
| AiriLoginEntity.accessToken | 登陆成功的AccessToken，作为验证账号的凭证 |
| AiriLoginEntity.twitter_username | 当前账号绑定的Twitter账户的用户名，没有绑定为"" |
| AiriLoginEntity.facebook_username | 当前账号绑定的Facebook账户的用户名，没有绑定为"" |
| AiriLoginEntity.yostar_username | 当前账号绑定的Yostar账户的用户名，没有绑定为"" |
| AiriLoginEntity.isCanBindGuest | 当前账号是否可以绑定当前机器保存的游客账号，为true时调用SDKNewAccountLink接口 |
| AiriLoginEntity.airiUID | 当前账号的uid,作为账户唯一标识使用 |
| AiriLoginEntity.virtual | 当前机器是否为虚拟机，为true时，说明当前机器为虚拟机 |

### 渠道登陆

#### 调用API

```java
void SDKLogin(Platform platform,String params1,String params2,boolean isCreateNew,AiriSDKConnect.LoginResultCallback callback)
```
#### 调用实例

```java
 AiriSDKInstance.getInstance().SDKLink(platform,params1,params2,loginResultCallback);
```

#### 接口参数说明

| 参数名称 | 参数说明 | 是否必须 |
| ------ | ------ | ------ |
| Platform | 登陆平台参数，登陆渠道选择有DEVICE,TRANSCODE,YOSTAR,FACEBOOK,TWITTER | 是 |
| params1 | 登陆需要参数1，当Platform的值为Platform.TRANSCODE时，parms1代表继承码。当Platform的值为Platform.YOSTAR时，params1为邮箱账号 | 否 |
| params2 | 登陆需要参数2，当Platform的值为Platform.TRANSCODE时，parms2代表继承码对应的UID。当Platform的值为Platform.YOSTAR时，params2为邮箱收到的验证码 | 否 |
| isCreateNew | 是否强制创建新的账号 | 是 |
| AiriSDKConnect.LoginResultCallback | 登陆结果回调 | 是 |

#### Platform参数说明

| 参数名称 | 参数说明 |
| ------ | ------ | 
| Platform.DEVICE | 游客渠道 |
| Platform.TRANSCODE | 继承码渠道 |
| Platform.TWITTER | Twitter渠道 |
| Platform.FACEBOOK | Facebook渠道 |
| Platform.YOSTAR | Yostar渠道 |
| Platform.GOOGLE | Google支付渠道 |
| Platform.AU | AU支付渠道 |

### 获取继承码

#### 调用API
```java
void SDKTranscodeReq(AiriSDKConnect.TranscodeResultCallback callback)
```
#### 调用实例
```java
AiriSDKInstance.getInstance().SDKTranscodeReq(new AiriSDKConnect.TranscodeResultCallback() {
            @Override
            public void onSuccess(String transcode, String transUid) {
                MainActivity.setResultTv("Get the transcode successfully:"+transcode + ",Corresponding UID：" + transUid) ;
            }

            @Override
            public void onFail(ErrorEntity error) {
                MainActivity.setResultTv("Get the transcode failed："+error.toString()) ;
            }
        });
```
#### 接口参数说明
| 参数名称 | 参数说明 | 是否必须 |
| ------ | ------ | ------ |
| AiriSDKConnect.TranscodeResultCallback | 获取继承码结果回调 | 是 |

#### 回调参数说明
| 参数名称 | 参数说明 |
| ------ | ------ |
| transcode | 继承码 |
| transUid | 继承码对应的UID |

### 渠道绑定

#### 调用API
```java
void SDKLink(Platform platfrom,String params1,String params2,AiriSDKConnect.LinkResultCallback callback)
```
#### 调用实例
```java
AiriSDKInstance.getInstance().SDKLink(platform,params1,params2,new AiriSDKConnect.LinkResultCallback() {
            @Override
            public void onSuccess(Platform platform, String socailName) {
                MainActivity.setResultTv("Binding success:" + platform.name() + ",Corresponding user name：" + socailName ) ;
            }

            @Override
            public void onFail(ErrorEntity error) {
                MainActivity.setResultTv("Binding failed："+error.toString()) ;
            }
        });
```
#### 接口参数说明

| 参数名称 | 参数说明 | 是否必须 |
| ------ | ------ | ------ |
| Platform | 绑定使用的平台标识，渠道绑定参数标识可选择YOSTAR,FACEBOOK,TWITTER | 是 |
| params1 | 绑定需要参数1，当Platform的值为Platform.YOSTAR时，params1为邮箱账号 | 否 |
| params2 | 绑定需要参数2，当Platform的值为Platform.YOSTAR时，params2为邮箱收到的验证码 | 否 |
| AiriSDKConnect.LinkResultCallback | 绑定结果回调 | 是 |

#### 回调结果参数
| 参数名称 | 参数说明 |
| ------ | ------ |
| Platform | 绑定的渠道标识 |
| socailName | 绑定渠道对应的用户名 |

### 覆盖绑定

#### 调用API
```java
void SDKNewAccountLink(AiriSDKConnect.ReLinkResultCallback callback)
```
#### 调用实例
```java
AiriSDKInstance.getInstance().SDKNewAccountLink(new AiriSDKConnect.ReLinkResultCallback() {
            @Override
            public void onSuccess(Platform platform, String socailName, String accessToken) {
                MainActivity.setResultTv("Binding tourists successfully:" + platform.name() + ",Corresponding user name：" + socailName + ",Updated AccessToken:" +accessToken ) ;
            }

            @Override
            public void onFail(ErrorEntity error) {
                MainActivity.setResultTv("Binding tourists failed："+error.toString()) ;
            }
        }) ;
```
#### 接口参数说明
| 参数名称 | 参数说明 | 是否必须 |
| ------ | ------ | ------ |
| AiriSDKConnect.ReLinkResultCallback | 覆盖绑定结果回调 | 是 |

#### 回调结果参数说明
| 参数名称 | 参数说明 |
| ------ | ------ |
| Platform | 绑定的渠道标识 |
| socailName | 绑定渠道对应的用户名 |
| accessToken | 登陆时获取的accessToken过期，变成此accessToken |

### 解除绑定
#### 调用API
```java
void SDKUnlink(Platform platform,AiriSDKConnect.UnLinkResultCallback callback)
```
#### 调用实例
```java
AiriSDKInstance.getInstance().SDKUnlink(platform,new AiriSDKConnect.UnLinkResultCallback() {
            @Override
            public void onSuccess(Platform platform, String socailName) {
                MainActivity.setResultTv("Unbind successfully:" + platform.name() + ",Corresponding user name：" + socailName ) ;
            }

            @Override
            public void onFail(ErrorEntity error) {
                MainActivity.setResultTv("Unbind successfully failed："+error.toString()) ;
            }
        } );
```
#### 接口参数说明
| 参数名称 | 参数说明 | 是否必须 |
| ------ | ------ | ------ |
| platform | 解除绑定渠道标识,解除绑定可选择标识TWITTER,FACEBOOK | 是 |
| AiriSDKConnect.UnLinkResultCallback | 解除绑定结果回调 | 是 |

#### 回调结果参数
| 参数名称 | 参数说明 |
| ------ | ------ |
| Platform | 解除绑定的渠道标识 |
| socailName | 绑定渠道对应的用户名 |

### 生日设置(其他可选,日本必接)

#### 调用API
```java
void SDKSetBirth(String birthDay,AiriSDKConnect.BirthSetResultCallback callback)
```
#### 调用实例
```java
AiriSDKInstance.getInstance().SDKSetBirth(birthDay,new AiriSDKConnect.BirthSetResultCallback() {
            @Override
            public void onSuccess() {
                MainActivity.setResultTv("Birthday setting is successful") ;
            }

            @Override
            public void onFail(ErrorEntity error) {
                MainActivity.setResultTv("Birthday setting failed："+error.toString()) ;
            }
        });
```
#### 接口参数说明
| 参数名称 | 参数说明 | 是否必须 |
| ------ | ------ | ------ |
| birthDay | 生日日期，日期格式为yyyyMMdd | 是 |
| AiriSDKConnect.BirthSetResultCallback | 设置生日结果回调 | 是 |

### 统计事件上传

#### 调用API
```java
void SDKUserEventUpload(String eventName,String eventJson)
```
#### 调用实例
```java
Map<String,String> map = new HashMap<>() ;
map.put("params1","test1") ;
map.put("params2","test2") ;
JSONObject json = new JSONObject(map);
AiriSDKInstance.getInstance().SDKUserEventUpload("role_levelup",json.toString());
```
#### 接口参数详情
| 参数名称 | 参数说明 | 是否必须 |
| ------ | ------ | ------ |
| eventName | 事件名称，要与AiriSDK后台添加的相对应 | 是 |
| eventJson | 事件详情，为JSON格式的字符串参数 | 是 |

### 支付接口
#### 调用API
```java
void SDKPurchase(Platform platform,String productId,String serverTag,String extraData,AiriSDKConnect.PurchaseResultCallback callback)
```
#### 调用实例
```java
AiriSDKInstance.getInstance().SDKPurchase(platform,productId,serverTag,extraData,new AiriSDKConnect.PurchaseResultCallback() {
            @Override
            public void onResult(String orderId, String extraData, ErrorEntity entity) {
                if (entity.CODE() == 0){
                    MainActivity.setResultTv("支付成功 - 订单ID:" + orderId + ", 附加参数：" + extraData );
                }else{
                    MainActivity.setResultTv("支付失败："+entity.toString()) ;
                }
            }
        });
```
#### 接口参数详情
| 参数名称 | 参数说明 | 是否必须 |
| ------ | ------ | ------ |
| platform | 支付渠道标识，支付时可以选择GOOGLE、AU， | 是 |
| productId | 商品ID，要与支付渠道后台和AiriSDK后台配置的相符合 | 是 |
| serverTag | 服务器标识，默认为production | 是 |
| extraData | 附加参数，在支付结果回调时原样返回 | 是 |
| AiriSDKConnect.PurchaseResultCallback | 支付结果回调 | 是 |

#### 回调结果参数说明
| 参数名称 | 参数说明 | 
| ------ | ------ | 
| orderId | AiriSDK订单号 |
| extraData | 附加参数，由支付时传入 |
| ErrorEntity | 支付结果信息，entity.CODE()==0时支付成功，其他情况为失败 |


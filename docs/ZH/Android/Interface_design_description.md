本SDK的主入口类为AiriSDK，以下方法皆从该类中调用。

#### demo工程源码目录

<!--[https://github.com/Yostardev/yostar-sdk-android](https://github.com/Yostardev/yostar-sdk-android)-->

接入过程您可以查看demo工程作为参考。






### 1.设置全局回调

+ 调用API

```java
void setSdkInfoCallback(AiriSDKConnect.SDKInfoCallback sdkInfoCallback)
```

+ 调用实例

```java

AiriSDK.getInstance().setSdkInfoCallback(new AiriSDKConnect.SDKInfoCallback() {
  
            @Override 
            public void onSuccess(String message) {
              
              // message字段可转化为json对象；
              // 所有异步接口调用后，调用结果都会在该函数返回；
              // METHOD 字段用于区分来自哪个接口的调用；
            }
        });
```


### 2.初始化

以下所有接口必须在初始化完成后调用。

+ 调用API

```java
void SDKInit( String sdk_url,  String payStoreId,  boolean isShowDebugLog,  boolean isNewDevice)
```

+ 调用实例

```java
AiriSDK.SDKInit("https://xxxxx.arknights.com", "googleplay", false, false);
```

+ 接口参数说明

| 参数名称             | 参数说明      | 备注 |
|:-------------------|:------------|:--------|
| sdk_url            | SDK服务器地址| 无      |
|  payStoreId         | 支付渠道 |  google支付:googleplay、oneStore支付: onestore、亚马逊支付:amazon、三星支付:samsung   |
| isShowDebugLog      | 是否显示log日志| 无      |
| isNewDevice         | 游戏卸载重装后，游客登录时,账号是否需要重新生成| 若入参false,游客账号会和设备号绑定，卸载重装后，可重登老账号   |


+ 回调参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| R_VIRTUAL | Int | 是否是模拟器 1：模拟器 0：真机 |
| R_CODE | ResultCode（枚举） | 错误码 : 0成功，其它见后面统一错误码表 |
| R_MSG | string | 错误信息，辅助用 |
| ISCACHE | Int | 是否存在登陆缓存，存在1，不存在0 |
| LOGIN_PLATFORM | LoginPlatform（枚举） | 缓存登陆的平台 |
| LOGIN_UID | string | 缓存的UID |
| LOGIN_NAME | string | 缓存的名称 |
| IS_POPUP_AGREEMENT | Int | 是否需要弹出公告栏，1：需要 ，0：不需要 |
| METHOD | string | OnInitNotify |

### 2.获取设备号

+ 调用API

```java
String SDKGetDeviceID()
```

+ 调用实例

```java
AiriSDK.SDKGetDeviceID()
```

### 3.打开客服界面

+ 调用API

```java
void ShowAiHelpFAQs(String sdkVersion,String serverId,String roleUid, String roleName,String roleCreateTime,int purchase,String tags)
```

+ 调用实例

```java
JsonArray tagArray = new JsonArray();
tagArray.add("tag1");
tagArray.add("vip1");
AiriSDK.ShowAiHelpFAQs("2.1.42","serverID 1","playerUid_271","playerName_271","2020-08-24",1000,tagArray.toString());
```

+ 接口参数说明

| 参数名称             | 参数说明      | 备注 |
|:-------------------|:------------|:--------|
| sdkVersion            | sdk版本号|        |
| serverId         | 角色所在服务器Id |  未登录可传""|
| roleUid      | 角色ID| 未登录可传""|
| roleName         |  角色名称 |未登录可传""|
| roleCreateTime     | 角色创建时间|未登录可传""|
| purchase            | 角色累计消费|未登录可传0|
| tags            | 标签数组|未登录可传空数组|


### 4.快速登陆

+ 调用API

```java
void QuickLogin()
```

+ 调用实例

```java
AiriSDK.QuickLogin();
```


+ 回调参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| R_CODE | string | 错误码 : 0成功，其它见后面统一错误码表 |
| R_MSG | string | 错误信息，辅助用 |
| ACCESS_TOKEN | string | SDK登陆成功之后返回ACCESS_TOKEN，用于游戏服务器验证使用 |
| UID | string | SDK登陆成功之后返回UID，用于游戏服务器验证使用 |
| LOGIN_PLATFORM | LoginPlatform（枚举） | 当前游戏登陆平台，枚举Airisdk.LoginPlatform |
| BIRTH | string | 生日信息（仅在日本地区有效，没有设置生日信息的不可以支付） |
| FACEBOOK_NAME | string | FB登陆或绑定的FB名称 |
| TWITTER_NAME | string | TW登陆或绑定的TW名称 |
| GOOGLE_EMAIL | string | Google登陆或绑定的Google邮箱 |
| SDK_NAME | string | 悠星账号登陆的名称 |
| ISCAN_BIND_GUEST | int | 是否可以绑定游客账号(0不可以绑定, 非0可以绑定)，发生在用新FB、TW、悠星账号登陆时，同时检测到相同设备上一次登陆过游客账号。则可以调用API NewAccountLink() 进行绑定，也可不绑定。 |
| R_DELETETIME | string | 时间单位(单位：毫秒),最终确定删除此账号的时间，在这个时间之前，账号都是可以恢复的 |
| ISNEW | int | 是否为新账号，1：是新账号，0：不是新账号 |
| MIGRATIONCODE | string | 继承码，账号没有继承码或者继承码过期时，参数为空 |
| AMAZON_NAME | string | 用于标识是否绑定亚马逊账号 |
| METHOD | string | OnLoginNotify |




### 5.请求邮箱验证码

在使用Yostar账号系统登陆，绑定之前，需要用户手动输入邮箱，并调用此接口获取邮箱验证码.

+ 调用API

```java
void SDKVerificationCodeReq(String accountEmail)
```

+ 调用实例

```java
AiriSDK.SDKVerificationCodeReq("email_address@host.com");
```

+ 接口参数说明

| 参数名称                              | 参数说明            | 是否必须 |
|:-------------------------------------|:------------------|:--------|
| accountEmail                         | Yostar账户系统的邮箱 | 是      |


+ 回调参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| R_CODE | string | 错误码 : 0成功，其它见后面统一错误码表 |
| R_MSG | string | 错误信息，辅助用 |
| METHOD | string | OnVerificationCodeNotify |


### 6.渠道登陆

+ 调用API

```java
void SDKLogin( int platFromCode,  String params1,  String parmas2,  boolean isCreateNew)
```

+ 调用实例

```java
AiriSDK.SDKLogin(AiriSDKCommon.LOGINPLATFORM_YOSTAR, "xxx@host.com", "btdf3gb", false);
```

+ 接口参数说明

| 参数名称                            | 参数说明                                                                                                                         | 是否必须 |
|:-----------------------------------|:-------------------------------------------------------------------------------------------------------------------------------|:--------|
| platform                           | 登陆平台参数，登陆渠道选择有DEVICE,TRANSCODE,YOSTAR,FACEBOOK,TWITTER,Google_Email,Google_Play,Amazon                                                         | 是      |
| params1                            | 登陆需要参数1，当Platform的值为Platform.TRANSCODE时，parms1代表继承码。当Platform的值为Platform.YOSTAR时，params1为邮箱账号               | 否      |
| params2                            | 登陆需要参数2，当Platform的值为Platform.TRANSCODE时，parms2代表继承码对应的UID。当Platform的值为Platform.YOSTAR时，params2为邮箱收到的验证码 | 否      |
| isCreateNew                        | 默认入参 false                                                                                                               | 是      |                                                                                                                  | 是      |

+ Platform参数说明

| 参数名称             | 参数说明           |
|:--------------------|:-----------------|
| AiriSDKCommon.DEVICE     | 游客渠道          |
| AiriSDKCommon.TRANSCODE  | 继承码渠道         |
| AiriSDKCommon.TWITTER    | Twitter渠道      |
| AiriSDKCommon.FACEBOOK   | Facebook渠道     |
| AiriSDKCommon.YOSTAR     | Yostar渠道       |
| AiriSDKCommon.GOOGLE_EMAIL     | Google邮箱渠道 |
| AiriSDKCommon.GOOGLE_GAME_PLAY | GooglePlay渠道 |
| AiriSDKCommon.AMAZON         | 亚马逊渠道        |


+ 回调参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| R_CODE | string | 错误码 : 0成功，其它见后面统一错误码表 |
| R_MSG | string | 错误信息，辅助用 |
| ACCESS_TOKEN | string | SDK登陆成功之后返回ACCESS_TOKEN，用于游戏服务器验证使用 |
| UID | string | SDK登陆成功之后返回UID，用于游戏服务器验证使用 |
| LOGIN_PLATFORM | LoginPlatform（枚举） | 当前游戏登陆平台，枚举Airisdk.LoginPlatform |
| BIRTH | string | 生日信息（仅在日本地区有效，没有设置生日信息的不可以支付） |
| FACEBOOK_NAME | string | FB登陆或绑定的FB名称 |
| TWITTER_NAME | string | TW登陆或绑定的TW名称 |
| GOOGLE_EMAIL | string | Google登陆或绑定的Google邮箱 |
| SDK_NAME | string | 悠星账号登陆的名称 |
| ISCAN_BIND_GUEST | int | 是否可以绑定游客账号(0不可以绑定, 非0可以绑定)，发生在用新FB、TW、悠星账号登陆时，同时检测到相同设备上一次登陆过游客账号。则可以调用API NewAccountLink() 进行绑定，也可不绑定。 |
| R_DELETETIME | string | 时间单位(单位：毫秒),最终确定删除此账号的时间，在这个时间之前，账号都是可以恢复的 |
| ISNEW | int | 是否为新账号，1：是新账号，0：不是新账号 |
| MIGRATIONCODE | string | 继承码，账号没有继承码或者继承码过期时，参数为空 |
| AMAZON_NAME | string | 用于标识是否绑定亚马逊账号 |
| METHOD | string | OnLoginNotify |




### 7.发行继承码

+ 调用API

```java
void SDKTranscodeReq()
```

+ 调用实例

```java
 AiriSDK.SDKTranscodeReq()
```

+ 回调Event参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| R_CODE | string | 错误码 : 0成功，其它见后面统一错误码表 |
| R_MSG | string | 错误信息，辅助用 |
| MIGRATIONCODE | string | 继承码 |
| UID | string | SDK UID |
| METHOD | string | OnMigrationCodeNotify |

### 8.渠道绑定

+ 调用API

```java
public static void SDKLink(int platfrom, String params1, String params2)
```

+ 调用实例

```java
AiriSDK.SDKLink(AiriSDKCommon.LOGINPLATFORM_FACEBOOK, "", "");
```

+ 接口参数说明

| 参数名称                           | 参数说明                                                                      | 是否必须 |
|:----------------------------------|:----------------------------------------------------------------------------|:--------|
| platfrom                          | 绑定使用的平台标识，渠道绑定参数标识可选择YOSTAR,FACEBOOK,TWITTER,Google,GOOGLEPLAY | 是      |
| params1                           | 绑定需要参数1，当Platform的值为Platform.YOSTAR时，params1为邮箱账号                | 否      |
| params2                           | 绑定需要参数2，当Platform的值为Platform.YOSTAR时，params2为邮箱收到的验证码         | 否      |

+ 回调结果参数

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| R_CODE | string | 错误码 : 0成功，其它见后面统一错误码表 |
| R_MSG | string | 错误信息，辅助用 |
| ACCESS_TOKEN | string | 绑定成功之后返回ACCESS_TOKEN |
| LOGIN_PLATFORM | int | 当前游戏绑定平台，枚举Airisdk.LoginPlatform |
| SOCAIL_NAME | string | 当前游戏绑定平台用户名称 |
| METHOD | string | OnLinkNotify |


### 9.覆盖绑定

+ 调用API

```java
void SDKNewAccountLink()
```

+ 调用实例

```java
AiriSDK.SDKNewAccountLink()
```

+ 回调结果参数

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| R_CODE | string | 错误码 : 0成功，其它见后面统一错误码表 |
| R_MSG | string | 错误信息，辅助用 |
| ACCESS_TOKEN | string | 绑定成功之后返回ACCESS_TOKEN |
| LOGIN_PLATFORM | int | 当前游戏绑定平台，枚举Airisdk.LoginPlatform |
| SOCAIL_NAME | string | 当前游戏绑定平台用户名称 |
| METHOD | string | OnLinkNotify |


### 10.解除绑定

+ 调用API

```java
 void SDKUnLink(int platfrom, String params1, String params2)
```

+ 调用实例

```java
 AiriSDK.SDKUnLink(AiriSDKCommon.LOGINPLATFORM_YOSTAR, "xxx@host.com", "fdsgt4");
```

+ 接口参数说明

| 参数名称                             | 参数说明                                                          | 是否必须 |
|:------------------------------------|:----------------------------------------------------------------|:-------|
| platfrom                           | 解除绑定渠道标识,解除绑定可选择标识TWITTER,FACEBOOK,Google,GOOGLEPLAY | 是      |
| params1                            | 解绑需要参数1，当Platform的值为Platform.TRANSCODE时，parms1代表继承码。当Platform的值为Platform.YOSTAR时，params1为邮箱账号               | 否      |
| params2                            | 解绑需要参数2，当Platform的值为Platform.TRANSCODE时，parms2代表继承码对应的UID。当Platform的值为Platform.YOSTAR时，params2为邮箱收到的验证码 | 否      |


+ 回调Event参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| R_CODE | string | 错误码 : 0成功，其它见后面统一错误码表 |
| R_MSG | string | 错误信息，辅助用 |
| LOGIN_PLATFORM | LoginPlatform（枚举） | 当前游戏绑定平台，枚举Airisdk.LoginPlatform |
| SOCAIL_NAME | string | 当前游戏绑定平台用户名称 |
| METHOD | string | OnUnLinkNotify |

### 11.生日设置(可选,日本必接)

+ 调用API

```java
void SDKSetBirth(String birth)
```

+ 调用实例

```java
AiriSDK.SDKSetBirth(birthDay);
```

+ 接口参数说明

| 参数名称                               | 参数说明                   | 是否必须 |
|:--------------------------------------|:-------------------------|:--------|
| birthDay                              | 生日日期，日期格式为yyyyMMdd | 是      |


+ 回调Event参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| R_CODE | string | 错误码 : 0成功，其它见后面统一错误码表 |
| R_MSG | string | 错误信息，辅助用 |
| BIRTH | string | 生日，格式“yyyymmdd”，如“19901212”（必要） |
| METHOD | string | OnSetBrithNotify |

### 12.统计事件上传

+ 调用API

```java
void SDKUserEventUpload(String eventName,String eventJson)
```

+ 调用实例

```java
Map<String,String> map = new HashMap<>() ;
map.put("params1","test1") ;
map.put("params2","test2") ;
JSONObject json = new JSONObject(map);
AiriSDKInstance.getInstance().SDKUserEventUpload("role_levelup",json.toString());
```

+ 接口参数详情

| 参数名称   | 参数说明                          | 是否必须 |
|:----------|:--------------------------------|:--------|
| eventName | 事件名称，要与AiriSDK后台添加的相对应 | 是      |
| eventJson | 事件详情，为JSON格式的字符串参数     | 是     |

### 13.支付接口

+ 调用API

```java
void SDKBuy(String productId, String serverTag, String extraData);
```

+ 调用实例

```java
AiriSDK.SDKBuy(purchasItem.getProductID(), "audit", "testxxxxxxx2020||");
```

+ 接口参数详情

| 参数名称                               | 参数说明                                    | 是否必须 |
|:--------------------------------------|:------------------------------------------|:--------|
| productId                             | 商品ID，要与支付渠道后台和AiriSDK后台配置的相符合 | 是      |
| serverTag                             | 服务器标识；提审服:audit、预发布服:preAudit、正式服:production | 是      |
| extraData                             | 附加参数，在支付结果回调时原样返回               | 是      |


+ 回调结果参数说明

| 参数名称     | 参数说明                                           |
|:------------|:-------------------------------------------------|
| ORDERID     | AiriSDK订单号                                      |
| EXTRADATA   | 附加参数，由支付时传入                                |
| R_CODE | 错误码 : 0成功，其它见后面统一错误码表 |
| R_MSG | 错误信息，辅助用 |
| METHOD      | OnBuyNotify |


### 14.系统分享(可选)

+ 调用API

```java
void SystemShare(String strShareText, String imagePath)
```

+ 调用实例

```java
AiriSDK.SystemShare("123455", "img file path");
```

+ 接口参数说明

| 参数名称                            | 参数说明                                                    | 是否必须 |
|:-----------------------------------|:----------------------------------------------------------|:--------|
| shareText                          | 分享图片时带的文字内容，可能无效                                | 是      |
| imagePath                          | 分享图片的存储路径                                            | 是      |


+ 回调Event参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| R_CODE | string | 错误码 : 0成功，其它见后面统一错误码表 |
| R_MSG | string | 错误信息，辅助用 |
| METHOD   | string | OnSystemShareNotify |






### 15. void onResume()

Adjust统计需要游戏需要在Launcher Activity的onResume方法中调用此接口

+ 调用API

```java
void SDKOnResume() ;
```

+ 调用实例

```java
AiriSDK.SDKOnResume();
```

### 16. void onPause()

Adjust统计需要游戏需要在Launcher Activity的onPause方法中调用此接口

+ 调用API

```java
void SDKOnPause();
```

+ 调用实例

```java
AiriSDK.SDKOnPause();
```


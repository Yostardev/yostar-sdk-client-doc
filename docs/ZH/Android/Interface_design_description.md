
本SDK的主入口类为AiriSDKInstance，以下方法皆从该类中调用。

#### demo工程源码目录

[https://github.com/Yostardev/yostar-sdk-android](https://github.com/Yostardev/yostar-sdk-android)

接入过程您可以查看demo工程作为参考。

### 1.初始化

以下所有接口必须在初始化完成后调用。

+ 调用API
```java
void initSDK(Activity activity, AiriSDKConnect.InitResultCallback callback)
```
+ 调用实例
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
+ 接口参数说明

| 参数名称 | 参数说明 | 是否必须 |
| ------ | ------ | ------ |
| Activity | 程序上下文 | 是 |
| AiriSDKConnect.InitResultCallback | 初始化结果回调 | 是 |

+ 回调参数说明

| 参数名称 | 参数说明 |
| ------ | ------ | 
| isVirtual | 当前机器是否为模拟器 |
| ErrorEntity | 错误日志类，entity.CODE()为错误码，错误详情请查看错误码表 |

### 2.获取设备号

+ 调用API

```java
String SDKGetDeviceID()
```
+ 调用实例
```java
AiriSDKInstance.getInstance().SDKGetDeviceID()
```

### 3.打开客服界面

+ 调用API
```java
void SDKOpenHelpShift()
```
+ 调用实例
```java
AiriSDKInstance.getInstance().SDKOpenHelpShift();
```
### 4.快速登陆

+ 调用API
```java
void SDKQuickLogin(AiriSDKConnect.LoginResultCallback callback)
```
+ 调用实例
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
+ 接口参数说明

| 参数名称 | 参数说明 | 是否必须 |
| ------ | ------ | ------ |
| AiriSDKConnect.LoginResultCallback | 登陆结果回调 | 是 |

+ 回调参数说明

| 参数名称 | 参数说明 |
| ------ | ------ | 
| ErrorEntity | 错误日志类，entity.CODE()为错误码，错误详情请查看错误码表 |
| AiriLoginEntity.accessToken | 登陆成功的AccessToken，作为验证账号的凭证 |
| AiriLoginEntity.twitter_username | 当前账号绑定的Twitter账户的用户名，没有绑定为"" |
| AiriLoginEntity.facebook_username | 当前账号绑定的Facebook账户的用户名，没有绑定为"" |
| AiriLoginEntity.yostar_username | 当前账号绑定的Yostar账户的用户名，没有绑定为"" |
| AiriLoginEntity.google_username | 当前账号绑定的Google账户的用户名，没有绑定为"" |
| AiriLoginEntity.isCanBindGuest | 当前账号是否可以绑定当前机器保存的游客账号，为true时调用SDKNewAccountLink接口 |
| AiriLoginEntity.airiUID | 当前账号的uid,作为账户唯一标识使用 |
| AiriLoginEntity.virtual | 当前机器是否为虚拟机，为true时，说明当前机器为虚拟机 |

### 5.请求邮箱验证码

在使用Yostar账号系统登陆，绑定之前，需要用户手动输入邮箱，并调用此接口获取邮箱验证码.

+ 调用API
```java
void SDKVerificationCodeReq(String accountEmail,AiriSDKConnect.CodeReqResultCallback callback)
```
+ 调用实例
```java
AiriSDKInstance.getInstance().SDKVerificationCodeReq(accountEmail, new AiriSDKConnect.CodeReqResultCallback() {
            @Override
            public void onSuccess() {
                MainActivity.setResultTv("Get the verification code successfully.") ;
            }

            @Override
            public void onFail(ErrorEntity entity) {
                MainActivity.setResultTv("Failed to get verification code："+entity.toString()) ;
            }
        });
```
+ 接口参数说明

| 参数名称 | 参数说明 | 是否必须 |
| ------ | ------ | ------ |
| accountEmail | Yostar账户系统的邮箱 | 是 |
| AiriSDKConnect.CodeReqResultCallback | 邮箱验证码回调 | 是 |


### 6.渠道登陆

+ 调用API

```java
void SDKLogin(Platform platform,String params1,String params2,boolean isCreateNew,AiriSDKConnect.LoginResultCallback callback)
```
+ 调用实例

```java
 AiriSDKInstance.getInstance().SDKLink(platform,params1,params2,loginResultCallback);
```

+ 接口参数说明

| 参数名称 | 参数说明 | 是否必须 |
| ------ | ------ | ------ |
| Platform | 登陆平台参数，登陆渠道选择有DEVICE,TRANSCODE,YOSTAR,FACEBOOK,TWITTER,Google | 是 |
| params1 | 登陆需要参数1，当Platform的值为Platform.TRANSCODE时，parms1代表继承码。当Platform的值为Platform.YOSTAR时，params1为邮箱账号 | 否 |
| params2 | 登陆需要参数2，当Platform的值为Platform.TRANSCODE时，parms2代表继承码对应的UID。当Platform的值为Platform.YOSTAR时，params2为邮箱收到的验证码 | 否 |
| isCreateNew | 是否强制创建新的账号 | 是 |
| AiriSDKConnect.LoginResultCallback | 登陆结果回调 | 是 |

+ Platform参数说明

| 参数名称 | 参数说明 |
| ------ | ------ | 
| Platform.DEVICE | 游客渠道 |
| Platform.TRANSCODE | 继承码渠道 |
| Platform.TWITTER | Twitter渠道 |
| Platform.FACEBOOK | Facebook渠道 |
| Platform.YOSTAR | Yostar渠道 |
| Platform.GOOGLE | Google支付登陆渠道 |
| Platform.AU | AU支付渠道 |

### 7.发行继承码

+ 调用API
```java
void SDKTranscodeReq(AiriSDKConnect.TranscodeResultCallback callback)
```
+ 调用实例
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
+ 接口参数说明

| 参数名称 | 参数说明 | 是否必须 |
| ------ | ------ | ------ |
| AiriSDKConnect.TranscodeResultCallback | 获取继承码结果回调 | 是 |

+ 回调参数说明

| 参数名称 | 参数说明 |
| ------ | ------ |
| transcode | 继承码 |
| transUid | 继承码对应的UID |

### 8.渠道绑定

+ 调用API
```java
void SDKLink(Platform platfrom,String params1,String params2,AiriSDKConnect.LinkResultCallback callback)
```
+ 调用实例
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
+ 接口参数说明

| 参数名称 | 参数说明 | 是否必须 |
| ------ | ------ | ------ |
| Platform | 绑定使用的平台标识，渠道绑定参数标识可选择YOSTAR,FACEBOOK,TWITTER,Google | 是 |
| params1 | 绑定需要参数1，当Platform的值为Platform.YOSTAR时，params1为邮箱账号 | 否 |
| params2 | 绑定需要参数2，当Platform的值为Platform.YOSTAR时，params2为邮箱收到的验证码 | 否 |
| AiriSDKConnect.LinkResultCallback | 绑定结果回调 | 是 |

+ 回调结果参数

| 参数名称 | 参数说明 |
| ------ | ------ |
| Platform | 绑定的渠道标识 |
| socailName | 绑定渠道对应的用户名 |

### 9.覆盖绑定

+ 调用API
```java
void SDKNewAccountLink(AiriSDKConnect.ReLinkResultCallback callback)
```
+ 调用实例
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
+ 接口参数说明

| 参数名称 | 参数说明 | 是否必须 |
| ------ | ------ | ------ |
| AiriSDKConnect.ReLinkResultCallback | 覆盖绑定结果回调 | 是 |

+ 回调结果参数说明

| 参数名称 | 参数说明 |
| ------ | ------ |
| Platform | 绑定的渠道标识 |
| socailName | 绑定渠道对应的用户名 |
| accessToken | 登陆时获取的accessToken过期，变成此accessToken |

### 10.解除绑定
+ 调用API
```java
void SDKUnlink(Platform platform,AiriSDKConnect.UnLinkResultCallback callback)
```
+ 调用实例
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
+ 接口参数说明

| 参数名称 | 参数说明 | 是否必须 |
| ------ | ------ | ------ |
| platform | 解除绑定渠道标识,解除绑定可选择标识TWITTER,FACEBOOK,Google | 是 |
| AiriSDKConnect.UnLinkResultCallback | 解除绑定结果回调 | 是 |

+ 回调结果参数

| 参数名称 | 参数说明 |
| ------ | ------ |
| Platform | 解除绑定的渠道标识 |
| socailName | 绑定渠道对应的用户名 |

### 11.生日设置(可选,日本必接)

+ 调用API
```java
void SDKSetBirth(String birthDay,AiriSDKConnect.BirthSetResultCallback callback)
```
+ 调用实例
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
+ 接口参数说明

| 参数名称 | 参数说明 | 是否必须 |
| ------ | ------ | ------ |
| birthDay | 生日日期，日期格式为yyyyMMdd | 是 |
| AiriSDKConnect.BirthSetResultCallback | 设置生日结果回调 | 是 |

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

| 参数名称 | 参数说明 | 是否必须 |
| ------ | ------ | ------ |
| eventName | 事件名称，要与AiriSDK后台添加的相对应 | 是 |
| eventJson | 事件详情，为JSON格式的字符串参数 | 是 |

### 13.支付接口
+ 调用API
```java
void SDKPurchase(Platform platform,String productId,String serverTag,String extraData,AiriSDKConnect.PurchaseResultCallback callback)
```
+ 调用实例
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
+ 接口参数详情

| 参数名称 | 参数说明 | 是否必须 |
| ------ | ------ | ------ |
| platform | 支付渠道标识，支付时可以选择GOOGLE、AU， | 是 |
| productId | 商品ID，要与支付渠道后台和AiriSDK后台配置的相符合 | 是 |
| serverTag | 服务器标识，默认为production | 是 |
| extraData | 附加参数，在支付结果回调时原样返回 | 是 |
| AiriSDKConnect.PurchaseResultCallback | 支付结果回调 | 是 |

+ 回调结果参数说明

| 参数名称 | 参数说明 | 
| ------ | ------ | 
| orderId | AiriSDK订单号 |
| extraData | 附加参数，由支付时传入 |
| ErrorEntity | 支付结果信息，entity.CODE()==0时支付成功，其他情况为失败 |

### 14.系统分享(可选)

+ 调用API
```java
void SDKSystemShare(String shareText,Bitmap bitmap,AiriSDKConnect.ShareResultCallback callback)
```
+ 调用实例
```java
AiriSDKInstance.getInstance().SDKSystemShare("测试图片-截图",activityShot(MainActivity.this),new AiriSDKConnect.ShareResultCallback() {
            @Override
            public void onSuccess() {
                MainActivity.setResultTv("System-level sharing on the Android side, there is no share result callback, so except for special cases, the default is success.");
            }

            @Override
            public void onFail(ErrorEntity entity) {
                MainActivity.setResultTv("Android share failed：" + entity.MESSAGE());
            }
        });
```
+ 接口参数说明

| 参数名称 | 参数说明 | 是否必须 |
| ------ | ------ | ------ |
| shareText | 分享图片时带的文字内容，可能无效 | 是 |
| bitmap | 图片Bitmap | 是 |
| AiriSDKConnect.ShareResultCallback | 分享结果回调(默认为成功，除了特殊情况，例如：图片没获取等情况返回失败) | 是 |

### 15.注销

调用注销功能会清除所有SDK缓存，请CP谨慎调用。
调用注销功能后，如果需要再次使用SDK功能请重新初始化SDK。

+ 调用API
```java
void SDKLogout(AiriSDKConnect.LogoutCallback callback)
```
+ 调用实例
```java
AiriSDKInstance.getInstance().SDKLogout(new AiriSDKConnect.LogoutCallback() {
            @Override
            public void onSuccess() {
                MainActivity.setResultTv("Logout successful, please re-initialize the sdk." ) ;
            }

            @Override
            public void onFail(ErrorEntity entity) {
                MainActivity.setResultTv("Logout failed："+entity.toString()) ;
            }
        });
```

### 16. void onResume()

游戏需要在Launcher Activity和Main Activity的onResume方法中调用此接口

+ 调用API
```java
void SDKOnResume() ;
```
+ 调用实例
```java
AiriSDKInstance.getInstance().SDKOnResume()
```
### 17. void onPause()

游戏需要在Launcher Activity和Main Activity的onPause方法中调用此接口

+ 调用API
```java
void SDKOnPause() ;
```
+ 调用实例
```java
AiriSDKInstance.getInstance().SDKOnPause()
```

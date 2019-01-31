
As the main class of this SDK, AiriSDKInstance is where you call API from for all the methods mentioned below.

#### DEMO PROJECT SOURCE CODE DIRECTORY

[https://github.com/Yostardev/yostar-sdk-android](https://github.com/Yostardev/yostar-sdk-android)

Please use the demo project as a reference during the process of building your SDK.

### 1.Initialization

All of the following API can only be called after a successful initialization.

+ Call API
```java
void initSDK(Activity activity, AiriSDKConnect.InitResultCallback callback)
```
+ Call API Example
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
+ API Parameter Details

| Parameter| Description | Necessity |
| ------ | ------ | ------ |
| Activity | Program context | YES |
| AiriSDKConnect.InitResultCallback | Initialization result | YES |

+ Callback Parameter Details

| Parameter | Description |
| ------ | ------ |
| isVirtual | Identify whether the current device is an emulator. |
| ErrorEntity | Error log, more details can be found in error_code_document with the given entity.CODE() |

### 2.Obtain Device Number

+ Call API

```java
String SDKGetDeviceID()
```
+ Call API Example
```java
AiriSDKInstance.getInstance().SDKGetDeviceID()
```

### 3.Open Customer Support Interface

+ Call API
```java
void SDKOpenHelpShift()
```
+ Call API Example
```java
AiriSDKInstance.getInstance().SDKOpenHelpShift();
```
### 4.Fast Login

+ Call API
```java
void SDKQuickLogin(AiriSDKConnect.LoginResultCallback callback)
```
+ Call API Example
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
+ API Parameter Details

| Parameter | Description | Necessity |
| ------ | ------ | ------ |
| AiriSDKConnect.LoginResultCallback | Login result Callback | YES |

+ Callback Parameter Details

| Parameter | Description |
| ------ | ------ |
| ErrorEntity | Error log, more details can be found in error_code_document with the given entity.CODE() |
| AiriLoginEntity.accessToken | An AccessToken for successful login, used to verify accounts |
| AiriLoginEntity.twitter_username | The username of Twitter account, "" means the account is not bound to Twitter yet |
| AiriLoginEntity.facebook_username | The username of Facebook account, "" means the account is not bound to Twitter yet |
| AiriLoginEntity.yostar_username | The username of Yostar account, "" means the account is not bound to Twitter yet |
| AiriLoginEntity.isCanBindGuest | Identify whether the current account is bound with the guest account currently saved in the device. If "ture", call API from "SDKNewAccountLink" |
| AiriLoginEntity.airiUID | The UID of current account, used as an unique identification of this account |
| AiriLoginEntity.virtual | Identify whether the current device is an emulator, "true" means it is an emulator |

### 5.Request an Email Verification code

Before users can login Yostar accounts, they are requested to input their email address manually, and then this API is used for Email Verification.

+ Call API
```java
void SDKVerificationCodeReq(String accountEmail,AiriSDKConnect.CodeReqResultCallback callback)
```
+ Call API Example
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
+ API Parameter Details

| Parameter | Description | Necessity |
| ------ | ------ | ------ |
| accountEmail | The email address linked to Yostar account | YES |
| AiriSDKConnect.CodeReqResultCallback | Email verification code callback | YES |


### 6.Login through Platforms

+ Call API

```java
void SDKLogin(Platform platform,String params1,String params2,boolean isCreateNew,AiriSDKConnect.LoginResultCallback callback)
```
+ Call API Example

```java
 AiriSDKInstance.getInstance().SDKLink(platform,params1,params2,loginResultCallback);
```

+ API Parameter Details

| Parameter | Description | Necessity |
| ------ | ------ | ------ |
| Platform | Platform parameter, platform includes DEVICE,TRANSCODE,YOSTAR,FACEBOOK,TWITTER | YES |
| params1 |The first parameter required for login. When Platform.TRANSCODE, params1 serves as the Device Transfer code; When Platform.YOSTAR, params1 serves as the email account | NO |
| params2 | The second parameter required for login. When Platform.TRANSCODE, params2 serves as the UID that pairs with the Device Transfer code; When Platform.YOSTAR, params2 serves as the verification code sent to the email | NO |
| isCreateNew | Whether to force a new account being created | YES |
| AiriSDKConnect.LoginResultCallback | Login result | YES |

+ Platform Parameter Details

| Parameter | Description |
| ------ | ------ |
| Platform.DEVICE | Guest (login without any platform) |
| Platform.TRANSCODE | Device Transfer Code |
| Platform.TWITTER | Twitter |
| Platform.FACEBOOK | Facebook |
| Platform.YOSTAR | Yostar |
| Platform.GOOGLE | Google Play payment method |
| Platform.AU | AU payment method |

### 7.Generate Device Transfer Code

+ Call API
```java
void SDKTranscodeReq(AiriSDKConnect.TranscodeResultCallback callback)
```
+ Call API Example
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
+ API Parameter Details

| Parameter | Description | Necessity |
| ------ | ------ | ------ |
| AiriSDKConnect.TranscodeResultCallback | Device Transfer Code generation result | YES |

+ Callback Parameter Details

| Parameter | Description |
| ------ | ------ |
| transcode | Device Transfer Code |
| transUid | The UID that pairs with the Device Transfer code |

### 8.Binding Account with Platforms

+ Call API
```java
void SDKLink(Platform platfrom,String params1,String params2,AiriSDKConnect.LinkResultCallback callback)
```
+ Call API Example
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
+ API Parameter Details

| Parameter | Description | Necessity |
| ------ | ------ | ------ |
| Platform | Account binding parameter, used to determine platforms which include YOSTAR,FACEBOOK,TWITTER | YES |
| params1 | When Platform.YOSTAR, params1 serves as the email account | NO |
| params2 | When Platform.YOSTAR, params2 serves as the verification code sent to the email | NO |
| AiriSDKConnect.LinkResultCallback | Account binding result | YES |

+ Callback Parameter Details

| Parameter | Description |
| ------ | ------ |
| Platform | Platform that is bound to the user account |
| socailName | Username in that platform |

### 9.Account Binding Overwriting

+ Call API
```java
void SDKNewAccountLink(AiriSDKConnect.ReLinkResultCallback callback)
```
+ Call API Example
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
+ API Parameter Details

| Parameter | Description | Necessity |
| ------ | ------ | ------ |
| AiriSDKConnect.ReLinkResultCallback | Overwrite account binding result | YES |

+ Callback Parameter Details

| Parameter | Description |
| ------ | ------ |
| Platform | Platform that is bound to the user account |
| socailName | Username in that platform |
| accessToken | After account binding overwriting, the old accessToken becomes invalid and is replaced by this new accessToken |

### 10.Account Unbinding
+ Call API
```java
void SDKUnlink(Platform platform,AiriSDKConnect.UnLinkResultCallback callback)
```
+ Call API Example
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
+ API Parameter Details

| Parameter | Description | Necessity |
| ------ | ------ | ------ |
| platform | Account unbinding parameter, can choose between FACEBOOK and TWITTER | YES |
| AiriSDKConnect.UnLinkResultCallback | Account unbinding result | YES |

+ Callback Parameter Details

| Parameter | Description |
| ------ | ------ |
| Platform | Platform that the user account was unbound from |
| socailName | Username in that platform |

### 11.Birthday Setting (optionable, excpet for users from Japan)

+ Call API
```java
void SDKSetBirth(String birthDay,AiriSDKConnect.BirthSetResultCallback callback)
```
+ Call API Example
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
+ API Parameter Details

| Parameter | Description | Necessity |
| ------ | ------ | ------ |
| birthDay | User's birthday, the format is yyyymmdd | YES |
| AiriSDKConnect.BirthSetResultCallback | Birthday result | YES |

### 12.Event Upload

+ Call API
```java
void SDKUserEventUpload(String eventName,String eventJson)
```
+ Call API Example
```java
Map<String,String> map = new HashMap<>() ;
map.put("params1","test1") ;
map.put("params2","test2") ;
JSONObject json = new JSONObject(map);
AiriSDKInstance.getInstance().SDKUserEventUpload("role_levelup",json.toString());
```
+ API Parameter Details

| Parameter | Description | Necessity |
| ------ | ------ | ------ |
| eventName | Event name, must match with the one added in AiriSDK server | YES |
| eventJson | Event details, must be formatted as a json file | YES |

### 13.Payment API
+ Call API
```java
void SDKPurchase(Platform platform,String productId,String serverTag,String extraData,AiriSDKConnect.PurchaseResultCallback callback)
```
+ Call API Example
```java
AiriSDKInstance.getInstance().SDKPurchase(platform,productId,serverTag,extraData,new AiriSDKConnect.PurchaseResultCallback() {
            @Override
            public void onResult(String orderId, String extraData, ErrorEntity entity) {
                if (entity.CODE() == 0){
                    MainActivity.setResultTv("Payment Successful - OrderId:" + orderId + ", ExtraData：" + extraData );
                }else{
                    MainActivity.setResultTv("Payment Failed:"+entity.toString()) ;
                }
            }
        });
```
+ API Parameter Details

| Parameter | Description | Necessity |
| ------ | ------ | ------ |
| platform | Identify the payment method, can choose between Google and AU | YES |
| productId | Item Id, must match with the one from payment platform and the one from AiriSDK server | YES |
| serverTag | Server tag, the default is false "production" | YES |
| extraData | A string used to verify the purchase. It was sent when a purchase starts, and then callback to verify if it is the same string | YES |
| AiriSDKConnect.PurchaseResultCallback | Purchase result | YES |

+ Callback Parameter Details

| Parameter | Description |
| ------ | ------ |
| orderId | AiriSDK order id |
| extraData | A string used to verify the purchase. It was sent when a purchase starts, and then callback to verify if it is the same string |
| ErrorEntity | Purchase result, the payment is successful only when entity.CODE()==0, otherwise the payment is failed |

### 14.Sharing System (optional)

+ Call API
```java
void SDKSystemShare(String shareText,Bitmap bitmap,AiriSDKConnect.ShareResultCallback callback)
```
+ Call API Example
```java
AiriSDKInstance.getInstance().SDKSystemShare("Test Image - Screenshot",activityShot(MainActivity.this),new AiriSDKConnect.ShareResultCallback() {
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
+ API Parameter Details

| Parameter | Description | Necessity |
| ------ | ------ | ------ |
| shareText | Test which is going to be shared, might be invalid | YES |
| bitmap | Image which is going to be shared, must be formatted as Bitmap | YES |
| AiriSDKConnect.ShareResultCallback | Sharing result (the default is "onSuccess", except for special circumstances, for instance: the image is not retrieved) | YES |

### 15.Cancellation

Calling the Cancellation function will result a SDK cache clearing, please use it with great caution.
After a Cancellation, you have to perform a SDK initialization before using it again.

+ Call API
```java
void SDKLogout(AiriSDKConnect.LogoutCallback callback)
```
+ Call API Example
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

Your game requires to call this API through onResume method in Launcher Activity and Main Activity.

+ Call API
```java
void SDKOnResume() ;
```
+ Call API Example
```java
AiriSDKInstance.getInstance().SDKOnResume()
```
### 17. void onPause()

Your game requires to call this API through onPause method in Launcher Activity and Main Activity.

+ Call API
```java
void SDKOnPause() ;
```
+ Call API Example
```java
AiriSDKInstance.getInstance().SDKOnPause()
```

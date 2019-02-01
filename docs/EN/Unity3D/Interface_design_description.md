
### 1、Initialization

Initialization only has to be done once, and it is a necessity for calling any API. The result is shown in Callback EVENT.

 + Call API:
 ```csharp
 public void Init()
 ```
 + Call API Example:
```csharp
using Airisdk;
AiriSDK.Instance.Init();
```
 + Callback Event
```csharp
AirisdkEvent.Instance.InitEvent
```
 + Callback Event Type:
```csharp
InitRet
```
+ Callback Parameter Details

| Parameter | Type | Description |
| ------ | ------ | ------ |
| R_VIRTUAL | Int | Identify whether the current device is an emulator. 1: Emulator; 0: Mobile |
| R_CODE | ResultCode (Enumeration) | Status code, 0 means success; If an error occurs, please check error_code_document for more details. |
| R_MSG | string | Error message |

### 2、Server Shift

Called when Unity program is shifting between client and server.

+ Call API:

```csharp
public void OnResume()
```
```csharp
public void OnPause()
```
+ Call API Example:
```csharp
using Airisdk;
private void OnApplicationPause(bool isPause)
{
  //Need to determine that SDK INIT is successful before it can be called
  if (isPause)
  {
    AiriSDK.Instance.OnPause();
  }
  else
  {
    AiriSDK.Instance.OnResume();
  }
}
```

### 3、Guest Login

Login the game with device number, no assurance provided to user account.

+ Call API:
```csharp
public void LoginWithDevice()
```
+ Call API Example:
```csharp
using Airisdk;
AiriSDK.Instance.LoginWithDevice();
```
+ Callback Event:
```csharp
AirisdkEvent.Instance.LoginEvent (More detailed description can be found in a later section)
```

### 4、Fast Login

Login with the most recent account that has been logged in on the device. If no previous account has been used, then login as a guest. Please note: The guest account information will be cleared upon resetting the mobile to factory settings and/or clearing local account data cache.

+ Call API:
```csharp
public void QuickLogin()
```
+ Call API Example:
```csharp
using Airisdk;
AiriSDK.Instance.QuickLogin();
```
+ Callback Event:
```csharp
AirisdkEvent.Instance.LoginEvent
```

### 5、Facebook Login

Use a Facebook account to login the game, if it is the first time logging in with a Facebook account, create a SDK ID automatically.

+ Call API:
```csharp
public void LoginWithFB()
```
+ Call API Example:
```csharp
using Airisdk;
AiriSDK.Instance.LoginWithFB();
```
+ Callback Event:
```csharp
AirisdkEvent.Instance.LoginEvent
```

### 6、Twitter Login

Use a Twitter account to login the game, if it is the first time logging in with a Twitter account, create a SDK ID automatically.

+ Call API:
```csharp
public void LoginWithTW()
```
+ Call API Example:
```csharp
using Airisdk;
AiriSDK.Instance.LoginWithTW();
```
+ Callback Event:
```csharp
AirisdkEvent.Instance.LoginEvent
```

### 7、Device Transfer Code Login

Logging in with a Device Transfer code. Device Transfer code acquisition needs an independent API being called (it is explained in the next section). Call function return value ResultCode which is only used to verify the the parameter, the final validity is determined by the callback result of LoginEvent (More detailed description can be found in a later section).

+ Call API:
```csharp
ResultCode void LoginWithTranscode(string strTranscode, string strUid)
```
+ Call API Example：
```csharp
using Airisdk;
ResultCode rc = AiriSDK.Instance.LoginWithTranscode(strcode, struid);
If(rc == ResultCode.OK){
    //todo suc
  } else {
  //todo failed
}
```
+ Callback Event:
```csharp
AirisdkEvent.Instance.LoginEvent
```

+ API Parameter Details

| Parameter | Type | Description |
| ------ | ------ | ------ |
| strTranscode | string | The Device Transfer code (necessary) |
| strUid | string | SDK UID（necessary） |


### 8、Device Transfer Code Acquisition

After logging in the game, call this API to acquire the Device Transfer code and UID of the current account. If the current account is not bound with any third-party platform (Facebook, Twitter, and Yostar), then it is possible to recover this account with a Device Transfer code.

+ Call API:
```csharp
public void TranscodeRequest()
```
+ Call API Example:
```csharp
using Airisdk;
AiriSDK.Instance.TranscodeRequest();
```
+ Callback Event:
```csharp
AirisdkEvent.Instance.TranscodeEvent
```
+ Callback Event Type:
```csharp
TranscodeRet
```
+ Callback Parameter Details

| Parameter | Type | Description |
| ------ | ------ | ------ |
| R_CODE | string | Status code, 0 means success; If an error occurs, please check error_code_document for more details |
| R_MSG | string | Error message |
| TRANSCODE | string | The Device Transfer Code |
| UID | string | SDK UID |

+ Callback Event Example

```csharp
using Airisdk.Event;
AirisdkEvent.Instance.TranscodeEvent += OnTranscodeRespone;
private void OnTranscodeRespone(TranscodeRet ret) {
  //to do
}
```

### 9、Login Callback Event

This event is called no matter which login method is used, including logging in through Yostar account system (which is introduced in the next section).

+ Callback Event:
```csharp
AirisdkEvent.Instance.LoginEvent
```
+ Callback Event Type:
```csharp
LoginRet
```
+ Callback Parameter Details

| Parameter | Type | Description |
| ------ | ------ | ------ |
| R_CODE | string | Status code, 0 means success; If an error occurs, please check error_code_document for more details |
| R_MSG | string | Error message |
| ACCESS_TOKEN | string | ACCESS_TOKEN is returned after logging in the SDK， it is used to verify with the game server |
| UID | string | UID is returned after logging in the SDK， it is used to verify with the game server |
| LOGIN_PLATFORM | LoginPlatform（Enumeration） | Platform that the current game logged in through, enumerate Airisdk.LoginPlatform |
| BIRTH | string | Birthday Information (It is a necessity for player from Japan, otherwise their payments will be denied) |
| FACEBOOK_NAME | string | Facebook account name |
| TWITTER_NAME | string | Twitter account name |
| SDK_NAME | string | Yostar account name |
| ISCAN_BIND_GUEST | int | Identify whether a Guest account can be bound with a third-party platform account (0: No; Anything else than 0: Yes). It happens when a Guest account, which logged in the last time on this device, is detected, when logging in with a new Facebook, Twitter or Yostar account. It is possible to call API NewAccountLink() to bind the Guest account. |

+ Callback Event Example：
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.LoginEvent+= OnLoginRespone;
private void OnLoginRespone(LoginRet ret) {
  //to do
}
```

### 10、Yostar Account Registration

Upon the completion of registering Yostar account, the account is logged in automatically, the same Callback event as the one we use for login is used here. Call function return value ResultCode which is only used to verify the the parameter, the final validity is determined by the callback result of LoginEvent (More detailed description can be found in a later section).

+ Call API:
```csharp
ResultCode void SDKRegistLogin(string strEmail, string strEmailDoubleCheck, string strVerificationCode)
```
+ Call API Example：
```csharp
using Airisdk;
ResultCode rc = AiriSDK.Instance.SDKRegistLogin(strEmail, strEmailDoubleCheck, strVerificationCode);
If(rc == ResultCode.OK){
  //todo suc
} else {
  //todo failed
}
```

+ Callback Event：

```csharp
The same as the Callback Event in section 9
```
+ API Parameter Details

| Parameter | Type | Description |
| ------ | ------ | ------ |
| strEmail | string | Email address (necessary) |
| strEmailDoubleCheck | string | Double check the email address (necessary) |
| strVerificationCode | string | Verification code sent to the email (necessary) |

### 11、Yostar Account Login

Upon the logging in the Yostar account, the same Callback event as the one we use for login is used here. Call function return value ResultCode which is only used to verify the the parameter, the final validity is determined by the callback result of LoginEvent (More detailed description can be found in a later section).

+ Call API:
```csharp
ResultCode void LoginWithSDKAccount(string strEmail, string strVerificationCode)
```

+ Call API Example：
```csharp
using Airisdk;
ResultCode rc = AiriSDK.Instance.LoginWithSDKAccount(strEmail, strVerificationCode);
If(rc == ResultCode.OK){
  //todo suc
} else {
  //todo failed
}
```

+ Callback Event：

```
The same as the Callback Event in section 9
```

+ API Parameter Details

| Parameter | Type | Description |
| ------ | ------ | ------ |
| strEmail | string | Email address (necessary) |
| strVerificationCode | string | Verification code sent to the email (necessary) |

### 12、Yostar Account Verification Code

This API is called when Yostar account system is requesting a verification code. The verification code then will be sent to the email address. The callback API only returns error code.

+ Call API:
```csharp
ResultCode void VerificationCodeReq(string strEmail)
```
+ Call API Example:
```csharp
using Airisdk;
ResultCode rc = AiriSDK.Instance.VerificationCodeReq(strEmail);
If(rc == ResultCode.OK){
  //todo suc
} else {
  //todo failed
}
```
+ Callback Event:
```csharp
AirisdkEvent.Instance.VerificationCodeEvent
```
+ Callback Event Type:
```csharp
VerificationCodeRet
```
+ Callback Event Example:
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.VerificationCodeEvent += OnVerificationCodeRespone;
private void OnVerificationCodeRespone(VerificationCodeRet ret){
  //to do
}
```
+ API Parameter Details

| Parameter | Type | Description |
| ------ | ------ | ------ |
| strEmail | string | Email address (necessary) |

+ Callback Parameter Details

| Parameter | Type | Description |
| ------ | ------ | ------ |
| R_CODE | string | Status code, 0 means success; If an error occurs, please check error_code_document for more details |
| R_MSG | string | Error message |

### 13、Facebook and Twitter Account Binding

Call function return value ResultCode which is only used to verify the the parameter, the final validity is determined by the callback result of LoginEvent (More detailed description can be found in a later section).

Please note: Account binding overwriting is not valid. If the Facebook/Twitter account is already bound, unbind it first.

Please note: Can only be called after logging in the SDK

+ Call API:

```csharp
ResultCode void LinkSocial(LoginPlatform platform)
```
+ Call API Example：
```csharp
using Airisdk;
ResultCode rc = AiriSDK.Instance.LinkSocial(LoginPlatform.FACEBOOK);
If(rc == ResultCode.OK){
  //todo suc
 } else {
  //todo failed
 }
```
+ Callback Event:
```csharp
AirisdkEvent.Instance.LinkEvent
```
+ API Parameter Details

| Parameter | Type | Description |
| ------ | ------ | ------ |
| platform | LoginPlatform（Enumeration） | Platform (necessary) |

### 14、Yostar Account Binding (with an existing Yostar account)

Call function return value ResultCode which is only used to verify the the parameter, the final validity is determined by the callback result of LoginEvent (More detailed description can be found in a later section).

Please note: Yostar account cannot be overwritten nor be unbound.

Please note: Can only be called after logging in the SDK.

Please note: A Yostar account can be bound to many games, if one account is already bound with game A, then in game B it would be regarded was an existing Yostar account.

+ Call API:
```csharp
ResultCode void LinkSocial(LoginPlatform platform, string strEmail, string strVerificationCode)
```
+ Call API Example:
```csharp
using Airisdk;
ResultCode rc = AiriSDK.Instance.LinkSocial(LoginPlatform.YOSTAR, strEmail, strVerificationCode);
If(rc == ResultCode.OK){
  //todo suc
 } else {
  //todo failed
 }
```
+ Callback Event:
```csharp
AirisdkEvent.Instance.LinkEvent
```

+ API Parameter Details

| Parameter | Type | Description |
| ------ | ------ | ------ |
| platform | LoginPlatform（Enumeration） | Platform (necessary) |
| strEmail | string | Email address (necessary) |
| strVerificationCode | string | Verification (necessary) |


### 15、Yostar Account Binding (with a new account)

Call function return value ResultCode which is only used to verify the the parameter, the final validity is determined by the callback result of LoginEvent (More detailed description can be found in a later section).

Please note: Yostar account cannot be overwritten nor be unbound.

Please note: Can only be called after logging in the SDK.

Please note: This API is called when registering and binding Yostar account in game.

+ Call API:
```csharp
ResultCode void SDKRegsitLink(string strEmail, string strEmailDoubleCheck, string strVerificationCode)
```
+ Call API Example:
```csharp
using Airisdk;
ResultCode rc = AiriSDK.Instance.SDKRegsitLink(strEmail, strEmailDoubleCheck,strVerificationCode);
If(rc == ResultCode.OK){
  //todo suc
} else {
  //todo failed
}
```
+ Callback Event:
```csharp
AirisdkEvent.Instance.LinkEvent
```
+ API Parameter Details

| Parameter | Type | Description |
| ------ | ------ | ------ |
| strEmail | string | Email address (necessary) |
| strEmailDoubleCheck | string | Double check the email address (necessary) |
| strVerificationCode | string | Verification code sent to the email (necessary) |


### 16、Special Account Binding

Call function without return, the final validity is determined by the callback result of LoginEvent (More detailed description can be found in a later section).

Please note: Can only be called after logging in the SDK.

Please note: Can only be called when login Callback event “ISCAN_BIND_GUEST != 0”.

Please note: More detailed description can be found in section 9.

+ Call API:
```csharp
public void NewAccountLink()
```
+ Call API Example:
```csharp
using Airisdk;
AiriSDK.Instance.NewAccountLink();
```
+ Callback Event:
```csharp
AirisdkEvent.Instance.LinkEvent
```

### 17、Account Binding Callback Event

+ Callback Event:
```csharp
	AirisdkEvent.Instance.LinkEvent
 ```
+ Callback Event Type:
```csharp
LinkRet
```
+ Callback Event Example:
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.LinkEvent+= OnLinkRespone;
private void OnLinkRespone(LinkRet ret) {
  //to do
}
```
+ Callback Parameter Details

| Parameter | Type | Description |
| ------ | ------ | ------ |
| R_CODE | string | Status code, 0 means success; If an error occurs, please check error_code_document for more details |
| R_MSG | string | Error message |
| ACCESS_TOKEN | string | Return ACCESS_TOKEN upon successful account binding |
| LOGIN_PLATFORM | LoginPlatform（Enumeration） | Platform that the current game bound with, enumerate Airisdk.LoginPlatform |
| SOCAIL_NAME | string | User name of the platform that bound to the game |

### 18、Account Unbinding System

Call function return value ResultCode which is only used to verify the the parameter, the final validity is determined by the callback result of LoginEvent (More detailed description can be found in a later section).

Please note: Account binding overwriting is not valid. If the Facebook/Twitter account is already bound, unbind it first.

Please note: Can only be called after logging in the SDK.

Please note: Only works with Facebook and Twitter accounts.

+ Call API:
```csharp
ResultCode void UnLinkSocial(LoginPlatform platform)
```
+ Call API Example:
```csharp
using Airisdk;
AiriSDK.Instance.UnLinkSocial(LoginPlatform.FACEBOOK);
```
+ API Parameter Details

| Parameter | Type | Description |
| ------ | ------ | ------ |
| platform | LoginPlatform（Enumeration） | Platform (necessary) |

### 19、Account Unbinding Callback Event

+ Callback Event:
```csharp
AirisdkEvent.Instance.UnLinkEvent
```
+ Callback Event Type:
```csharp
UnLinkRet
```
+ Callback Event Example：
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.UnLinkEvent+= OnUnLinkRespone;
private void OnUnLinkRespone(UnLinkRet ret) {
	//to do
}
```
+ Callback Parameter Details

| Parameter | Type | Description |
| ------ | ------ | ------ |
| R_CODE | string | Status code, 0 means success; If an error occurs, please check error_code_document for more details |
| R_MSG | string | Error message |
| LOGIN_PLATFORM | LoginPlatform（Enumeration） | Platform that the current game bound with, enumerate Airisdk.LoginPlatform |
| SOCAIL_NAME | string | User name of the platform that bound to the game |

### 20、Testing on PC

Since most of the functions involve the original APIs on mobile, the testing on PC only contain the following:
+ SDK initialization：
```csharp
public void Init()
```
+ Fast Login：
```csharp
public void QuickLogin()
```
+ Guest Login：
```csharp
public void LoginWithDevice()
```
+ Device Transfer Code Login：	
```csharp
ResultCode void LoginWithTranscode(string strTranscode, string strUid)
```

### 21、Birthday Setting

Call this API to set user birthday. Japanese user's monthly payment limit is related with each user age.

+ Call API:
```csharp
public ResultCode SetBirth(string strBirth)
```
+ Call API Example：
```csharp
using Airisdk;
AiriSDK.Instance.SetBirth(“19901212”);
```
+ Callback Event：
```csharp
AirisdkEvent.Instance.BirthSetEvent
```
+ Callback Event Type：
```csharp
BirthSetRet
```
+ Callback Event Example：
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.BirthSetEvent+= OnBirthSetRespone;
private void OnBirthSetRespone(BirthSetRet ret) {
	//to do
}
```
+ API Parameter Details

| Parameter | Type | Description |
| ------ | ------ | ------ |
| strBirth | string | Birthday, keep the format as "yyyymmdd", for instance "19901212" (necessary) |

+ Callback Parameter Details

| Parameter | Type | Description |
| ------ | ------ | ------ |
| R_CODE | string | Status code, 0 means success; If an error occurs, please check error_code_document for more details |
| R_MSG | string | Error message |

### 22、Local Account Data Cache Clearing

Call this API to clear account data cache on the device.

Please note: Clearing the account data cache also clears the latest login information saved in Fast Login. Please re-login through Facebook, Twitter, or Yostar.

Please note: Use this function with great caution, and after confirm it with the player.

Please note: If the player doesn't have a Device Transfer Code, nor has he/she bound the account to Facebook/Twitter/Yostar, the account could be permanently lost after an account data cache clearing.

+ Call API:
```csharp
public void ClearAccountInfo()
```
+ Call API Example:
```csharp
using Airisdk;
AiriSDK.Instance.ClearAccountInfo();
```
+ Callback Event:
```csharp
AirisdkEvent.Instance.ClearAccountEvent
```
+ Callback Event Type:
```csharp
ClearAccountInfoRet
```
+ Callback Event Example:
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.ClearAccountEvent+= OnClearAccountRespone;
private void OnClearAccountRespone(ClearAccountInfoRet ret) {
	//to do
}
```
### 23、Upload User Data (Data Statistics)

These APIs allow some user activities being uploaded to SDK server.

+ Call API:
```csharp
public void UserEventUpload(string strEventName, Dictionary<string, string> strCallbackParameter = null)
```
+ Call API Example：
```csharp
using Airisdk;
Dictionary<string, string> dicParam = new Dictionary<string, string>();
dicParam.Add("test1", "test1");
dicParam.Add("test2", "test2");
AiriSDK.Instance.UserEventUpload(m_inputEventName.text, dicParam);
```
+ Callback Event：
```
Empty
```
+ API Parameter Details

| Parameter | Type | Description |
| ------ | ------ | ------ |
| strEventName | string | Activity name (provided by operation team) (necessary) |
| strCallbackParameter | Dictionary<string, string> | Callback parameter (provided by operation team) (unnecessary) |

### 24、Image Sharing

This API allows users to share customizable Texture2D through original iOS/Android sharing method. The image data is obtained through a parameter named "texture".

+ Call API:
```csharp
public void SystemShare(string strShareText, Texture2D texShare = null)
```
+ Call API Example：
```csharp
using Airisdk;
Texture2D screenShot = GetScreeShot()；
AiriSDK.Instance.SystemShare("test share", screenShot)；
```
+ Callback Event：
```csharp
AirisdkEvent.Instance.SystemShareEvent
```
+ Callback Event Parameter：
```csharp
SystemShareRet
```
+ Callback Event Example：
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.SystemShareEvent += OnSystemShareRespone;
private void OnSystemShareRespone(SystemShareRet ret) {
	//to do
}
```
+ API Parameter Details

| Parameter | Type | Description |
| ------ | ------ | ------ |
| strShareText | string | Test which is going to be shared (necessary) |
| texShare  | Texture2D | Image which is going to be shared (unnecessary) |

+ Callback Parameter Details

| Parameter | Type | Description |
| ------ | ------ | ------ |
| R_CODE | string | Status code, 0 means success; If an error occurs, please check error_code_document for more details |
| R_MSG | string | Error message |

### 25、App Store Ratings

This function allows users to rate for the App without leaving the App.

Please note: This function can only be used 3 times per user per year, thus it is advised to promote this function to players at the right time.

+ Call API:
```csharp
public string RequestStoreReview()
```
+ Call API Example：
```csharp
using Airisdk;
AiriSDK.Instance.RequestStoreReview();
```

### 26、Third-party customer support addon - HelpShift

This function opens the third-party customer support addon, HelpShift, where players can find the FAQ of the game and/or connect the customer service directly.

+ Call API:
```csharp
public string OpenHelpShift()
```
+ Call API Example：
```csharp
using Airisdk;
AiriSDK.Instance.OpenHelpShift();
```

### 27、Item Purchase

This function starts item purchasing. Item information is saved in AiriSDK server, please use "YostarSDKServerAPI" as a guidance. Call function return value ResultCode which is only used to verify the the parameter, the final validity is determined by the callback result of LoginEvent (More detailed description can be found in a later section).

+ Call API:
```csharp
ResultCode void Buy(string strProductId, BuyServerTag eServerTag, string strExtraData)
```

+ Call API Example：
```csharp
using Airisdk;
AiriSDK.Instance.Buy(“productid”, BuyServerTag.preAudit, “ExtraData”);
```

+ Callback Event:
```csharp
AirisdkEvent.Instance.BuyEvent
```
+ Callback Event Type：
```csharp
BuyRet
```

+ Callback Event Example：
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.BuyEvent += OnBuyRespone;
private void OnBuyRespone(BuyRet ret) {
	//to do
}
```
+ API Parameter Details

| Parameter | Type | Description |
| ------ | ------ | ------ |
| strProductId | string | Item ID, can be acquired from operation team, it is uploaded and saved in AiriSDK server (necessary) |
| eServerTag  | BuyServerTag(Enumeration) | Server Enumeration (Review server, test server, and official server) (necessary) Payment related server tag. This tag determines the URL given by the server when a payment request is being sent |
| strExtraData  | string | A string used to verify the purchase. It was sent when a purchase starts, and then callback to verify if it is the same string |

+ Callback Parameter Details

| Parameter | Type | Description |
| ------ | ------ | ------ |
| R_CODE | string | Status code, 0 means success; If an error occurs, please check error_code_document for more details |
| R_MSG | string | Error message |
| EXTRADATA | string | A string used to verify the purchase. It was sent when a purchase starts, and then callback to verify if it is the same string |
| ORDERID | string | Order ID, if the purchase request is initiated correctly, this string should be the same as the order ID on AiriSDK |

### 28、Data Acquisition

| Status | Description |
| ------ | ------ |
| AiriSDK.Instance.GetDeviceID() | Acquire user device ID |
| AiriSdkData.Instance.AiriSDK_VERSION | SDK version |


### 29、Error Code Document

[Error Code Document](https://github.com/Yostardev/yostarsdk/blob/master/docs/EN/errorcode.md)

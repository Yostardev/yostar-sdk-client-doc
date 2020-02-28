### 1、Guest Login

There's no security guarantee using the device number to log in.

+ Calling API:		
```csharp
public void LoginWithDevice()
```
+ Examples of API Call:
```csharp
using Airisdk;
AiriSDK.Instance.LoginWithDevice();
```
+ Callback Event:	
```csharp
AirisdkEvent.Instance.LoginEvent ((Further explained in later part of the documentation))
```

### 2、Quick login

Quick log in with the account that has logged into the game recently. If you do not have the account, you will log in with guest account. Note: The recent login information will be cleared if the phone has gone through the factory reset or the local account cache has been cleared.

+ Calling API:		
```csharp
public void QuickLogin()
```
+ Examples of API Call: 
```csharp
using Airisdk;
AiriSDK.Instance.QuickLogin();
```
+ Callback Event:
```csharp
AirisdkEvent.Instance.LoginEvent
```

### 3、Login with Facebook

Log into the game with Facebook account. The SDK ID will be automatically created if it is the first time login with Facebook account.

+ Calling API:		
```csharp
public void LoginWithFB()
```
+ Examples of API Call:
```csharp
using Airisdk;
AiriSDK.Instance.LoginWithFB();
```
+ Callback Event:
```csharp
AirisdkEvent.Instance.LoginEvent
```

### 4、Login with Gamil

Log into the game with Google account. The SDK ID will be automatically created if it is the first time login with Google account.

+ Calling API:		
```csharp
public void LoginWithGoogle()
```
+ Examples of API Call:
```csharp
using Airisdk;
AiriSDK.Instance.LoginWithGoogle();
```
+ Callback Event:
```csharp
AirisdkEvent.Instance.LoginEvent
```

### 5、Login with Google Play Game Services

Log into the game with Google account. The SDK ID will be automatically created if it is the first time login with Google Play Game Services.

+ Calling API:		
```csharp
public void LoginWithGooglePlay()
```
+ Examples of API Call:
```csharp
using Airisdk;
AiriSDK.Instance.LoginWithGooglePlay();
```
+ Callback Event:
```csharp
AirisdkEvent.Instance.LoginEvent
```

### 6、Sign in with apple

Log into the game with Apple account. The SDK ID will be automatically created if it is the first time login with Apple account.

+ Calling API:		
```csharp
public void LoginWithApple()
```
+ Examples of API Call:
```csharp
using Airisdk;
AiriSDK.Instance.LoginWithApple();
```
+ Callback Event:
```csharp
AirisdkEvent.Instance.LoginEvent
```

### 7、Login with Twitter

Log into the game with Twitter account. The SDK ID will be automatically created if it is the first time login with Twitter account.

Calling API:		
```csharp
public void LoginWithTW()
```
Examples of API Call: 
```csharp
using Airisdk;
AiriSDK.Instance.LoginWithTW();
```
Callback Event:	
```csharp
AirisdkEvent.Instance.LoginEvent 
```

### 8、Login with Inheritance Code 

Log into the game with inheritance code. The independent API should be called to obtain the inheritance code information, which is explained below. The return value of the function, ResultCode (further explained in later part of the documentation) is only used to verify the parameters. Whether it succeeds should be judged based on the return value of LoginEvent.

+ Calling API: 		
```csharp
ResultCode void LoginWithMigrationCode(string strTranscode, string strUid)
```
+ Examples of API Call： 
```csharp
using Airisdk;
ResultCode rc = AiriSDK.Instance.LoginWithMigrationCode(strcode, struid);
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

+ Interface Parameter Description

| Parameter Name | Parameter Type | Parameter Description |
| ------ | ------ | ------ |
| strTranscode | string | Inheritance Code (required) |
| strUid | string | SDK UID(required) |


### 9、Obtain Inheritance Code

After logging into the game, the inheritance code and UID couldl be obtained by calling this API. If the game account is not bound to any third-party account, it could be recovered by login with inheritance code when changing login device.

+ Calling API: 
```csharp
public void MigrationCodeRequest()
```
+ Examples of API Call:
```csharp
using Airisdk;
AiriSDK.Instance.MigrationCodeRequest();
```
+ Callback Event:			
```csharp
AirisdkEvent.Instance.MigrationCodeEvent
```
+ Callback Event Type:	
```csharp
MigrationCodeRet
```
+ Callback Event Parameter Description

| Parameter Name | Parameter Type | Parameter Description |
| ------ | ------ | ------ |
| R_CODE | string | Error code: 0 success. See Error Code Table for other error codes. |
| R_MSG | string | Error message, auxiliary |
| MIGRATIONCODE | string | Inheritance Code  |
| UID | string | SDK UID |

+ Examples of Callback Event

```csharp
using Airisdk.Event;
AirisdkEvent.Instance.MigrationCodeEvent += OnMigrationRespone;
private void OnMigrationRespone(MigrationCodeRet ret) {  
  //to do  
} 
```

### 10、Login Unified Callback EVENT

No matter which of the above login methods is used, including login with Yostar account which will be mentioned below, the callback event is always ```AirisdkEvent.Instance.LoginEvent``.

+ Callback Event:			
```csharp
AirisdkEvent.Instance.LoginEvent
```
+ Callback Event Type:	
```csharp
LoginRet
```
+ Callback Event Parameter Description

| Parameter Name | Parameter Type | Parameter Description |
| ------ | ------ | ------ |
| R_CODE | string | Error code: 0 success. See Error Code Table for other error codes. |
| R_MSG | string | Error message, auxiliary |
| ACCESS_TOKEN | string | Return ACCESS_TOKEN for game server authentication after the SDK login succeeds. |
| UID | string | Return UID for game server authentication after the SDK login succeeds. |
| LOGIN_PLATFORM | LoginPlatform | Current game login platform, enumerating ```Airisdk.LoginPlatform```. |
| BIRTH | string | Birthday information (only valid in Japan, unable to make payment without birthday information) |
| FACEBOOK_NAME | string | FB Login or Bound FB Name |
| TWITTER_NAME | string | TW Login or Bound TW Name |
| GOOGLE_EMAIL | string | Google Login or Bound Google Account |
| SDK_NAME | string | Yostar Account Name |
| ISCAN_BIND_GUEST | int | Whether the guest account can be bound (0 cannot be bound, non-0 can be bound). When logging in with a new FB, TW or Yostar account and it is detected that user has previously logged in with a guest account on the device, the API NewAccountLink() could be called to bind. |
| R_DELETETIME | string | Time unit (unit: millisecond). The time of actually deleting the account. The account could be recovered before it. |
| ISNEW | int | Whether it is a new account, 1: it is a new account, 0: it is not a new account |
| MIGRATIONCODE | string | Inheritance code. If the account does not have an inheritance code or the inheritance code expires, the parameter is empty. |

+ Examples of Callback Event：
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.LoginEvent+= OnLoginRespone;
private void OnLoginRespone(LoginRet ret) {  
  //to do  
} 
```

### 11、Yostar Account Login

Log into the game with Yostar account. The return value of the function, ResultCode (further explained in later part of the documentation) is only used to verify the parameters. Whether it succeeds should be judged based on the return value of LoginEvent.

+ Calling API: 	
```csharp
ResultCode void LoginWithSDK(string strEmail, string strVerificationCode)
```

+ Examples of API Call： 
```csharp
using Airisdk;
ResultCode rc = AiriSDK.Instance.LoginWithSDK(strEmail, strVerificationCode);
If(rc == ResultCode.OK){ 
  //todo suc 
} else { 
  //todo failed 
}
```

+ Callback Event：	

```
AirisdkEvent.Instance.LoginEvent
```

+ Interface Parameter Description

| Parameter Name | Parameter Type | Parameter Description |
| ------ | ------ | ------ |
| strEmail | string | Email Address (required) |
| strVerificationCode | string | Verification Code Sent To Email(required) |

### 12、Obtain Yostar Account Verification Code

The verification code request of the Yostar account system calls the API, and the verification code will be sent to the email address passed to the API. All callback interfaces will not contain the verification code, only ERRCODE.

+ Calling API: 	
```csharp
ResultCode void VerificationCodeReq(string strEmail)
```
+ Examples of API Call:
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
+ Examples of Callback Event:
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.VerificationCodeEvent += OnVerificationCodeRespone;
private void OnVerificationCodeRespone(VerificationCodeRet ret){ 
  //to do 
} 
```
+ Interface Parameter Description

| Parameter Name | Parameter Type | Parameter Description |
| ------ | ------ | ------ |
| strEmail | string | Email Address(required) |

+ Callback EventParameter Description

| Parameter Name | Parameter Type | Parameter Description |
| ------ | ------ | ------ |
| R_CODE | string | Error code: 0 success. See Error Code Table for other error codes. |
| R_MSG | string | Error message, auxiliary |


### 13、Obtain the current SDK login information

+ Calling API：

```csharp
public string SDKGetUID();
public string SDKGetAccessToken();
```

+ Examples of API Call：

```csharp
string Sdk_Uid = AiriSDK.Instance.SDKGetUID();
string Sdk_AccessToken = AiriSDK.Instance.SDKGetAccessToken();
```

+ Interface Description：

The ```SDKGetUID``` interface is used to obtain the current SDK UID. The ```SDKGetAccessToken``` interface is used to obtain the currently cached SDK AccessToken,. The AccessToken is used by the game to verify the login


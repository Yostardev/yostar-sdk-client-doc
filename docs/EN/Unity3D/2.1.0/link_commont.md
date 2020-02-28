
### 1、Account Binding System

The return value of the function, ResultCode (further explained in later part of the documentation) is only used to verify the parameters. Whether it succeeds should be judged based on the return value of LinkEvent.

Note: Cannot overwrite the binding. If the FB and TW accounts are already bound, you will need to unbind them first.

Note: Can only be called after successful login.

+ Calling API: 	

```csharp
ResultCode void LinkSocial(LoginPlatform platform)
```
+ Examples of API Call： 
```csharp
using Airisdk;
ResultCode rc = AiriSDK.Instance.LinkSocial(LoginPlatform.FACEBOOK);
If(rc == ResultCode.OK){ 
  //todo suc 
 } else { 
  //todo failed 
 }
```
+ Callback EVENT:	
```csharp
AirisdkEvent.Instance.LinkEvent
```
+ Interface Parameter Description

| Parameter Name | Parameter Type | Parameter Description |
| ------ | ------ | ------ |
| platform | LoginPlatform | Platform Type（required） |

### 2、Yostar Account Binding

The return value of the function, ResultCode (further explained in later part of the documentation) is only used to verify the parameters. Whether it succeeds should be judged based on the return value of LinkEvent.

Note: Can only be called after successful login.

Note: Yostar account could be bound to accounts of different games. For example, a Yostar account registered in Game A is an existing account for Game B.

+ Calling API: 	
```csharp
ResultCode void LinkSocial(LoginPlatform platform, string strEmail, string strVerificationCode)
```
+ Examples of API Call:
```csharp
using Airisdk;
ResultCode rc = AiriSDK.Instance.LinkSocial(LoginPlatform.YOSTAR, strEmail, strVerificationCode);
If(rc == ResultCode.OK){ 
  //todo suc 
 } else { 
  //todo failed 
 }
```
+ Callback EVENT:	
```csharp
AirisdkEvent.Instance.LinkEvent（Further explained in later part of the documentation）
```

+ Interface Parameter Description

| Parameter Name | Parameter Type | Parameter Description |
| ------ | ------ | ------ |
| platform | LoginPlatform（enumerate） | Platform Type（required） |
| strEmail | string | Email Address（required） |
| strVerificationCode | string | Verification Code Sent To Email （required） |

### 3、Special Binding

API Description: The function has no return value. Whether it succeeds should be judged based on the return value of LinkEvent. Further explained in later part of the documentation.

Note: Can only be called after successful login.

Note: Can only be called if it returns the data field "ISCAN_BIND_GUEST! = 0" when logging in.

Note: For detailed explanation, please refer to the description of ```"Login Unified Callback Event"```.

+ Calling API: 	
```csharp
public void NewAccountLink()
```
+ Examples of API Call:
```csharp
using Airisdk;
AiriSDK.Instance.NewAccountLink();
```
+ Callback EVENT:	
```csharp
AirisdkEvent.Instance.LinkEvent（Further explained in later part of the documentation）
```

### 4、Binding Unified Callback EVENT

+ Callback EVENT:		
```csharp
AirisdkEvent.Instance.LinkEvent
```
+ CCallback Event Type:	
```csharp
LinkRet
```
+ Examples of Callback Event:
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.LinkEvent+= OnLinkRespone;
private void OnLinkRespone(LinkRet ret) {  
  //to do  
} 
```
+ Callback EVENTParameter Description

| Parameter Name | Parameter Type | Parameter Description |
| ------ | ------ | ------ |
| R_CODE | string | Error code: 0 success. See Error Code Table for other error codes. |
| R_MSG | string |Error message, auxiliary |
| ACCESS_TOKEN | string | Returns ACCESS_TOKEN after successful binding |
| LOGIN_PLATFORM | LoginPlatform（enumerate） | Bound platform of the currentt game, enumerating Airisdk.LoginPlatform |
| SOCAIL_NAME | string | Username of the bound platform of the currentt game |

### 5、Account Unbundling System

API Description: The return value of the function, ResultCode (further explained in later part of the documentation) is only used to verify the parameters. Whether it succeeds should be judged based on the return value of UnLinkEvent.

Note: Cannot overwrite the binding. If the FB and TW accounts are already bound, you will need to unbind them first.

Note: Can only be called after successful login.


+ Calling API: 	
```csharp
ResultCode void UnlinkSocial(LoginPlatform platform)
```
+ Examples of API Call:
```csharp
using Airisdk;
AiriSDK.Instance.UnlinkSocial(LoginPlatform.FACEBOOK);
```
+ Interface Parameter Description

| Parameter Name | Parameter Type | Parameter Description |
| ------ | ------ | ------ |
| platform | LoginPlatform（enumerate） | Platform Type（required） |

### 6、Yostar Account Unbinding

+ Calling API: 	
```csharp
ResultCode void UnlinkSocial(LoginPlatform platform, string strEmail, string strVerificationCode)
```
+ Examples of API Call:
```csharp
using Airisdk;
ResultCode rc = AiriSDK.Instance.UnlinkSocial(LoginPlatform.YOSTAR, strEmail, strVerificationCode);
If(rc == ResultCode.OK){ 
  //todo suc 
 } else { 
  //todo failed 
 }
```
+ Callback EVENT:	
```csharp
AirisdkEvent.Instance.UnLinkEvent（Further explained in later part of the documentation）
```

+ Interface Parameter Description

| Parameter Name | Parameter Type | Parameter Description |
| ------ | ------ | ------ |
| platform | LoginPlatform（enumerate） | Platform Type（required） |
| strEmail | string | Email Address（required） |
| strVerificationCode | string | Verification Code Sent To Email （required） |

### 7、Unbinding Callback EVENT

+ Callback EVENT:			
```csharp
AirisdkEvent.Instance.UnLinkEvent
```
+ Callback Event Type:	
```csharp
UnLinkRet
```
+ Examples of Callback Event：
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.UnLinkEvent+= OnUnLinkRespone;
private void OnUnLinkRespone(UnLinkRet ret) {  
	//to do  
} 
```
+ Callback EVENTParameter Description

| Parameter Name | Parameter Type | Parameter Description |
| ------ | ------ | ------ |
| R_CODE | string | Error code: 0 success. See Error Code Table for other error codes. |
| R_MSG | string |Error message, auxiliary |
| LOGIN_PLATFORM | LoginPlatform（enumerate） | Bound platform of the currentt game, enumerating Airisdk.LoginPlatform |
| SOCAIL_NAME | string | Username of the bound platform of the currentt game |

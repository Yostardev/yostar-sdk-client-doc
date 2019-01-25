
### 1、初始化

初始化只需要调用一次。在调用其它的任何API前，必须执行初始化。初始化结果会在回调EVENT中给出。

 + 调用API:		
 ```csharp
 public void Init()
 ```
 + 调用示例:
```csharp
using Airisdk;
AiriSDK.Instance.Init();
```
 + 回调EVENT		
```csharp
AirisdkEvent.Instance.InitEvent
```
 + 回调Event类型:
```csharp
InitRet
```
+ 回调参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| R_VIRTUAL | Int | 是否是模拟器 1：模拟器 0：真机 |
| R_CODE | ResultCode（枚举） | 错误码 : 0成功，其它见后面统一错误码表 |
| R_MSG | string | 错误信息，辅助用 |

### 2、后台切换

在unity程序前后台切换时调用。

+ 调用API:		

```csharp
public void OnResume()
```
```csharp
public void OnPause()
```
+ 调用示例:
```csharp
using Airisdk;
private void OnApplicationPause(bool isPause)
{
  //这里需要判断SDK INIT成功之后才可以调用
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

### 游客登陆

使用设备号登陆游戏，账号无保障。

+ 调用API:		
```csharp
public void LoginWithDevice()
```
+ 调用示例:
```csharp
using Airisdk;
AiriSDK.Instance.LoginWithDevice();
```
+ 回调Event:	
```csharp
AirisdkEvent.Instance.LoginEvent (后续文章详细介绍)
```

### 快速登陆

使用最近一次登陆过游戏的账号快速登陆，若没有最近一次账号，则默认使用游客登陆。注：手机重装或本地账号缓存清除，最近登陆信息清空。

+ 调用API:		
```csharp
public void QuickLogin()
```
+ 调用示例: 
```csharp
using Airisdk;
AiriSDK.Instance.LoginWithDevice();
```
+ 回调Event:
```csharp
AirisdkEvent.Instance.LoginEvent
```

### Facebook登陆

使用facebook账号登陆游戏，若第一次使用facebook账号登陆，会自动创建SDK ID。

+ 调用API:		
```csharp
public void LoginWithFB()
```
+ 调用示例:
```csharp
using Airisdk;
AiriSDK.Instance.LoginWithFB();
```
+ 回调Event:
```csharp
AirisdkEvent.Instance.LoginEvent
```

### Twitter登陆

使用twitter账号登陆游戏，若第一次使用twitter账号登陆，会自动创建SDK ID。

调用API:		
```csharp
public void LoginWithTW()
```
调用示例: 
```csharp
using Airisdk;
AiriSDK.Instance.LoginWithTW();
```
回调Event:	
```csharp
AirisdkEvent.Instance.LoginEvent 
```

### 继承码登陆

使用继承码登陆游戏，继承码信息获取需要调用独立API获取，下面解释。调用函数返回值ResultCode（后续文章专门介绍）仅用来验证参数合法性，实际成功与否需要根据LoginEvent的返回数据进行判断。

+ 调用API: 		
```csharp
ResultCode void LoginWithTranscode(string strTranscode, string strUid)
```
+ 调用示例： 
```csharp
using Airisdk;
ResultCode rc = AiriSDK.Instance.LoginWithTranscode(strcode, struid);
If(rc == ResultCode.OK){ 
    //todo suc 
  } else { 
  //todo failed 
}
```
+ 回调Event:	
```csharp
AirisdkEvent.Instance.LoginEvent
```

+ 接口参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| strTranscode | string | 继承码（必要） |
| strUid | string | SDK UID（必要） |


### 继承码获取

在登陆游戏后，调用该API可以获取到当前账号的继承码和UID信息，当在未绑定第三方账号时，更换设备等可以通过继承码登陆找回之前账号。

+ 调用API: 
```csharp
public void TranscodeRequest()
```
+ 调用示例:
```csharp
using Airisdk;
AiriSDK.Instance.TranscodeRequest();
```
+ 回调Event:			
```csharp
AirisdkEvent.Instance.TranscodeEvent
```
+ 回调Event类型:	
```csharp
TranscodeRet
```
+ 回调Event参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| R_CODE | string | 错误码 : 0成功，其它见后面统一错误码表 |
| R_MSG | string | 错误信息，辅助用 |
| TRANSCODE | string | 继承码 |
| UID | string | SDK UID |

+ 回调Event 示例

```csharp
using Airisdk.Event;
AirisdkEvent.Instance.TranscodeEvent += OnTranscodeRespone;
private void OnTranscodeRespone(TranscodeRet ret) {  
  //to do  
} 
```

### 登陆统一回调EVENT

不管用以上哪一种登陆方式，回调事件都是这个。包括下文即将提到的悠星账号系统，同为AirisdkEvent.Instance.LoginEvent

+ 回调Event:			
```csharp
AirisdkEvent.Instance.LoginEvent
```
+ 回调Event类型:	
```csharp
LoginRet
```
+ 回调Event参数说明

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
| SDK_NAME | string | 悠星账号登陆的名称 |
| ISCAN_BIND_GUEST | int | 是否可以绑定游客账号(0不可以绑定, 非0可以绑定)，发生在用新FB、TW、悠星账号登陆时，同时检测到相同设备上一次登陆过游客账号。则可以调用API NewAccountLink() 进行绑定，也可不绑定。 |

+ 回调Event 示例：
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.LoginEvent+= OnLoginRespone;
private void OnLoginRespone(LoginRet ret) {  
  //to do  
} 
```

### 悠星账号注册

悠星账号注册成功后会自动登陆，所以这里的回调EVENT还是登陆回调。调用函数返回值ResultCode（后续文章专门介绍）仅用来验证参数合法性，实际成功与否需要根据LoginEvent的返回数据进行判断。不得在游戏内调用此接口。

+ 调用API: 	
```csharp
ResultCode void SDKRegistLogin(string strEmail, string strEmailDoubleCheck, string strVerificationCode)
```
+ 调用示例： 
```csharp
using Airisdk;
ResultCode rc = AiriSDK.Instance.SDKRegistLogin(strEmail, strEmailDoubleCheck, strVerificationCode);
If(rc == ResultCode.OK){ 
  //todo suc 
} else { 
  //todo failed 
}
```

+ 回调Event：	

```csharp
同上一章节登陆回调Event
```
+ 接口参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| strEmail | string | 邮箱地址（必要） |
| strEmailDoubleCheck | string | 邮箱地址二次检查（必要） |
| strVerificationCode | string | 发给邮箱的验证码（必要） |

### 悠星账号登陆

悠星账号登陆成功后，回调EVENT还是登陆回调。调用函数返回值ResultCode（后续文章专门介绍）仅用来验证参数合法性，实际成功与否需要根据LoginEvent的返回数据进行判断。

+ 调用API: 	
```csharp
ResultCode void LoginWithSDKAccount(string strEmail, string strVerificationCode)
```

+ 调用示例： 
```csharp
using Airisdk;
ResultCode rc = AiriSDK.Instance.LoginWithSDKAccount(strEmail, strVerificationCode);
If(rc == ResultCode.OK){ 
  //todo suc 
} else { 
  //todo failed 
}
```

+ 回调Event：	

```
同上一章节登陆回调Event
```

+ 接口参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| strEmail | string | 邮箱地址（必要） |
| strVerificationCode | string | 发给邮箱的验证码（必要） |

### 悠星账号验证码获取

悠星账号系统的验证码请求均为该API，验证码会发送到传入的邮箱内，所有回调接口不会包含验证码，只有ERRCODE。

+ 调用API: 	
```csharp
ResultCode void VerificationCodeReq(string strEmail)
```
+ 调用示例:
```csharp
using Airisdk;
ResultCode rc = AiriSDK.Instance.VerificationCodeReq(strEmail);
If(rc == ResultCode.OK){ 
  //todo suc 
} else { 
  //todo failed 
}
```
+ 回调Event:			
```csharp
AirisdkEvent.Instance.VerificationCodeEvent
```
+ 回调Event类型:	
```csharp
VerificationCodeRet
```
+ 回调Event 示例:
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.VerificationCodeEvent += OnVerificationCodeRespone;
private void OnVerificationCodeRespone(VerificationCodeRet ret){ 
  //to do 
} 
```
+ 接口参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| strEmail | string | 邮箱地址（必要） |

+ 回调Event参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| R_CODE | string | 错误码 : 0成功，其它见后面统一错误码表 |
| R_MSG | string | 错误信息，辅助用 |

### Facebook 、Twitter账号绑定

调用函数返回值ResultCode（后续文章专门介绍）仅用来验证参数合法性，实际成功与否需要根据LinkEvent的返回数据进行判断。后面会介绍。

注意：不可以覆盖绑定，FB、TW账号如果已有绑定账号，需要先解绑。

注意：只能在登陆成功之后调用。

+ 调用API: 	

```csharp
ResultCode void LinkSocial(LoginPlatform platform)
```
+ 调用示例： 
```csharp
using Airisdk;
ResultCode rc = AiriSDK.Instance.LinkSocial(LoginPlatform.FACEBOOK);
If(rc == ResultCode.OK){ 
  //todo suc 
 } else { 
  //todo failed 
 }
```
+ 回调Event:	
```csharp
AirisdkEvent.Instance.LinkEvent（后续文章详细介绍）
```
+ 接口参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| platform | LoginPlatform（枚举） | 平台类型（必要） |

### 悠星账号绑定（已有账号）

调用函数返回值ResultCode（后续文章专门介绍）仅用来验证参数合法性，实际成功与否需要根据LinkEvent的返回数据进行判断。后面会介绍。

注意：不可以覆盖绑定，悠星账号不可以解绑。

注意：只能在登陆成功之后调用。

注意：一个悠星账号下可以允许有无数个绑定游戏，如在A游戏注册的悠星账号，对于B游戏就是已有账号。

+ 调用API: 	
```csharp
ResultCode void LinkSocial(LoginPlatform platform, string strEmail, string strVerificationCode)
```
+ 调用示例:
```csharp
using Airisdk;
ResultCode rc = AiriSDK.Instance.LinkSocial(LoginPlatform.YOSTAR, strEmail, strVerificationCode);
If(rc == ResultCode.OK){ 
  //todo suc 
 } else { 
  //todo failed 
 }
```
+ 回调Event:	
```csharp
AirisdkEvent.Instance.LinkEvent（后续文章详细介绍）
```

+ 接口参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| platform | LoginPlatform（枚举） | 平台类型（必要） |
| strEmail | string | 邮箱地址（必要） |
| strVerificationCode | string | 平台类型（必要） |


### 悠星账号绑定（注册新账号）

API说明：调用函数返回值ResultCode（后续文章专门介绍）仅用来验证参数合法性，实际成功与否需要根据LinkEvent的返回数据进行判断。后面会介绍。

注意：不可以覆盖绑定，悠星账号不可以解绑。

注意：只能在登陆成功之后调用。

注意：该API是在游戏内注册悠星账号并同时绑定。

+ 调用API: 	
```csharp
ResultCode void SDKRegsitLink(string strEmail, string strEmailDoubleCheck, string strVerificationCode)
```
+ 调用示例:
```csharp
using Airisdk;
ResultCode rc = AiriSDK.Instance.SDKRegsitLink(strEmail, strEmailDoubleCheck,strVerificationCode);
If(rc == ResultCode.OK){ 
  //todo suc 
} else { 
  //todo failed 
}
```
+ 回调Event:	
```csharp
AirisdkEvent.Instance.LinkEvent（后续文章详细介绍）
```
+ 接口参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| strEmail | string | 邮箱地址（必要） |
| strEmailDoubleCheck | string | 邮箱地址二次检查（必要） |
| strVerificationCode | string | 发给邮箱的验证码（必要） |


### 特殊绑定

API说明：调用函数无返回值，成功与否需要根据LinkEvent的返回数据进行判断。后面会介绍。

注意：只能在登陆成功之后调用。

注意：仅在登陆返回数据字段“ISCAN_BIND_GUEST != 0”时可以调用 。

注意：详细解释见“登陆统一回调事件”该字段说明。

+ 调用API: 	
```csharp
public void NewAccountLink()
```
+ 调用示例:
```csharp
using Airisdk;
AiriSDK.Instance.NewAccountLink();
```
+ 回调Event:	
```csharp
AirisdkEvent.Instance.LinkEvent（后续文章详细介绍）
```

### 绑定统一回调EVENT

+ 回调Event:		
```csharp
	AirisdkEvent.Instance.LinkEvent
 ```
+ 回调Event类型:	
```csharp
LinkRet
```
+ 回调Event 示例:
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.LinkEvent+= OnLinkRespone;
private void OnLinkRespone(LinkRet ret) {  
  //to do  
} 
```
+ 回调Event参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| R_CODE | string | 错误码 : 0成功，其它见后面统一错误码表 |
| R_MSG | string | 错误信息，辅助用 |
| ACCESS_TOKEN | string | 绑定成功之后返回ACCESS_TOKEN |
| LOGIN_PLATFORM | LoginPlatform（枚举） | 当前游戏绑定平台，枚举Airisdk.LoginPlatform |
| SOCAIL_NAME | string | 当前游戏绑定平台用户名称 |

### 账号解绑系统

API说明：调用函数返回值ResultCode（后续文章专门介绍）仅用来验证参数合法性，实际成功与否需要根据UnLinkEvent的返回数据进行判断。

注意：不可以覆盖绑定，FB、TW账号如果已有绑定账号，需要先解绑。

注意：只能在登陆成功之后调用。

注意：仅FB、TW支持解绑操作

+ 调用API: 	
```csharp
ResultCode void UnLinkSocial(LoginPlatform platform)
```
+ 调用示例:
```csharp
using Airisdk;
AiriSDK.Instance.UnLinkSocial(LoginPlatform.FACEBOOK);
```
+ 接口参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| platform | LoginPlatform（枚举） | 平台类型（必要） |














### 1、账号绑定系统

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

### 2、悠星账号绑定

调用函数返回值ResultCode（后续文章专门介绍）仅用来验证参数合法性，实际成功与否需要根据LinkEvent的返回数据进行判断。后面会介绍。

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
| strVerificationCode | string | 发给邮箱的验证码（必要） |

### 3、特殊绑定

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

### 4、绑定统一回调EVENT

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

### 5、账号解绑系统

API说明：调用函数返回值ResultCode（后续文章专门介绍）仅用来验证参数合法性，实际成功与否需要根据UnLinkEvent的返回数据进行判断。

注意：不可以覆盖绑定，FB、TW账号如果已有绑定账号，需要先解绑。

注意：只能在登陆成功之后调用。


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

### 6、悠星账号解绑

+ 调用API: 	
```csharp
ResultCode void UnLinkSocial(LoginPlatform platform, string strEmail, string strVerificationCode)
```
+ 调用示例:
```csharp
using Airisdk;
ResultCode rc = AiriSDK.Instance.UnLinkSocial(LoginPlatform.YOSTAR, strEmail, strVerificationCode);
If(rc == ResultCode.OK){ 
  //todo suc 
 } else { 
  //todo failed 
 }
```
+ 回调Event:	
```csharp
AirisdkEvent.Instance.UnLinkEvent（后续文章详细介绍）
```

+ 接口参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| platform | LoginPlatform（枚举） | 平台类型（必要） |
| strEmail | string | 邮箱地址（必要） |
| strVerificationCode | string | 发给邮箱的验证码（必要） |

### 7、解绑回调EVENT

+ 回调Event:			
```csharp
AirisdkEvent.Instance.UnLinkEvent
```
+ 回调Event类型:	
```csharp
UnLinkRet
```
+ 回调Event 示例：
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.UnLinkEvent+= OnUnLinkRespone;
private void OnUnLinkRespone(UnLinkRet ret) {  
	//to do  
} 
```
+ 回调Event参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| R_CODE | string | 错误码 : 0成功，其它见后面统一错误码表 |
| R_MSG | string | 错误信息，辅助用 |
| LOGIN_PLATFORM | LoginPlatform（枚举） | 当前游戏绑定平台，枚举Airisdk.LoginPlatform |
| SOCAIL_NAME | string | 当前游戏绑定平台用户名称 |


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

### 3、游客登陆

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

### 4、快速登陆

使用最近一次登陆过游戏的账号快速登陆，若没有最近一次账号，则默认使用游客登陆。注：手机重装或本地账号缓存清除，最近登陆信息清空。

+ 调用API:		
```csharp
public void QuickLogin()
```
+ 调用示例: 
```csharp
using Airisdk;
AiriSDK.Instance.QuickLogin();
```
+ 回调Event:
```csharp
AirisdkEvent.Instance.LoginEvent
```

### 5、Facebook登陆

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

### 6、Twitter登陆

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

### 7、继承码登陆

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


### 8、继承码获取

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

### 9、登陆统一回调EVENT

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

### 10、悠星账号注册

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

### 11、悠星账号登陆

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

### 12、悠星账号验证码获取

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

### 13、Facebook 、Twitter账号绑定

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

### 14、悠星账号绑定（已有账号）

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


### 15、悠星账号绑定（注册新账号）

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


### 16、特殊绑定

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

### 17、绑定统一回调EVENT

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

### 18、账号解绑系统

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

### 19、解绑回调EVENT

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

### 20、PC端调试

由于大部分功能都涉及到手机端原生API
暂时PC端调试仅仅开放了以下接口：
+ SDK初始化：public void Init()
+ 快速登陆：public void QuickLogin()
+ 设备号登陆：public void LoginWithDevice()
+ 继承码登陆：	ResultCode void LoginWithTranscode(string strTranscode, string strUid)

### 21、设置用户生日

调用该接口，可以设置用户的生日。在日本，用户的年轻决定了它当月可以氪金的上限。

+ 调用API: 	
```csharp
public ResultCode SetBirth(string strBirth)
```
调用示例： 
```csharp
using Airisdk;
AiriSDK.Instance.SetBirth(“19901212”);
```
+ 回调Event：	
```csharp
AirisdkEvent.Instance.BirthSetEvent
```
+ 回调Event类型：
```csharp
BirthSetRet
```
回调Event 示例：
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.BirthSetEvent+= OnBirthSetRespone;
private void OnBirthSetRespone(BirthSetRet ret) {  
	//to do  
} 
```
+ 接口参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| strBirth | string | 生日，格式“yyyymmdd”，如“19901212”（必要） |

+ 回调Event参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| R_CODE | string | 错误码 : 0成功，其它见后面统一错误码表 |
| R_MSG | string | 错误信息，辅助用 |

### 22、清除本地账号缓存

调用该接口可以清楚设备上的账号信息。

注意：清空后快速登陆将无法使用上一次的账号直接登录，FB\TW\悠星账号都需要重新登录。

注意：请慎重调用，并在执行前向玩家多确认。

注意：如果玩家没有发行继承码，并且没有FB\TW\悠星账号，清除账号数据将很难找回账号。

+ 调用API: 	
```csharp
public void ClearAccountInfo()
```
+ 调用示例: 
```csharp
using Airisdk;
AiriSDK.Instance.ClearAccountInfo();
```
+ 回调Event:	
```csharp
AirisdkEvent.Instance.ClearAccountEvent
```
+ 回调Event类型:	
```csharp
ClearAccountInfoRet
```
+ 回调Event 示例:
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.ClearAccountEvent+= OnClearAccountRespone;
private void OnClearAccountRespone(ClearAccountInfoRet ret) {  
	//to do  
} 
```
### 23、用户行为数据上报（数据统计）

调用这些接口，可以通知SDK服务器一些用户事件。具体需要哪些用户事件会由运营人员和CP方进行对接。

+ 调用API: 	
```csharp
public void UserEventUpload(string strEventName, Dictionary<string, string> strCallbackParameter = null)
```
+ 调用示例： 
```csharp
using Airisdk;
Dictionary<string, string> dicParam = new Dictionary<string, string>();
dicParam.Add("test1", "test1");
dicParam.Add("test2", "test2");
AiriSDK.Instance.UserEventUpload(m_inputEventName.text, dicParam);
```
+ 回调Event：
```
无
```
+ 接口参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| strEventName | string | 事件名称（运营方提供）（必要） |
| strCallbackParameter | Dictionary<string, string> | 回调参数（运营方提供）（非必要） |

### 24、分享游戏自定义图片

调用该接口，可以将自定义的Texture2D进行分享iOS或Android的原生分享。该接口从参数texture获取贴图数据，

+ 调用API: 	
```csharp
public void SystemShare(string strShareText, Texture2D texShare = null)
```
+ 调用示例： 
```csharp
using Airisdk;
Texture2D screenShot = GetScreeShot()；
AiriSDK.Instance.SystemShare("test share", screenShot)；
```
+ 回调Event：	
```csharp
AirisdkEvent.Instance.SystemShareEvent
```
+ 回调Event数据参数：
```csharp
SystemShareRet
```
+ 回调Event 示例：
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.SystemShareEvent += OnSystemShareRespone;
private void OnSystemShareRespone(SystemShareRet ret) {  
	//to do  
} 
```
+ 接口参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| strShareText | string | 分享文字（必要） |
| texShare  | Texture2D | 分享图片（非必要） |

+ 回调Event参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| R_CODE | string | 错误码 : 0成功，其它见后面统一错误码表 |
| R_MSG | string | 错误信息，辅助用 |

### 25、APPSTORE商店评分

调用该接口，可以在不跳转APPSTORE的前提下，自动给应用打分。

注意：单个用户每年只能使用三次，所以需要在合适的时机提示玩家。

+ 调用API: 	
```csharp
public string RequestStoreReview()
```
+ 调用示例： 
```csharp
using Airisdk;
AiriSDK.Instance.RequestStoreReview();
```

### 26、第三方客服HelpShift

调用该接口，会自动打开HelpShift第三方客服插件，玩家可以通过上面查看基本疑问或者向官方进行QA。

+ 调用API: 	
```csharp
public string OpenHelpShift()
```
+ 调用示例： 
```csharp
using Airisdk;
AiriSDK.Instance.OpenHelpShift();
```

### 27、购买商品

调用该接口会开始执行商品的购买。商品信息是配置在AiriSDK后台的，具体请参考服务端接入文档。调用函数返回值ResultCode（后续文章专门介绍）仅用来验证参数合法性，实际成功与否需要根据BuyEvent的返回数据进行判断。

+ 调用API:
```csharp
ResultCode void Buy(string strProductId, BuyServerTag eServerTag, string strExtraData)
```

+ 调用示例： 
```csharp
using Airisdk;
AiriSDK.Instance.Buy(“productid”, BuyServerTag.preAudit, “ExtraData”);
```

+ 回调Event:		
```csharp
AirisdkEvent.Instance.BuyEvent 
```
+ 回调Event类型：	
```csharp
BuyRet
```

+ 回调Event示例：
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.BuyEvent += OnBuyRespone;
private void OnBuyRespone(BuyRet ret) {  
	//to do  
} 
```
+ 接口参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| strProductId | string | 商品ID，和运营方协商后获取，该ID是配置在AiriSDK后台（必要） |
| eServerTag  | BuyServerTag(枚举) | 服务器枚举（提审服、预发布服、正式服）（必要）支付对应的服务器tag。根据这个tag不同，最后服务端的支付通知URL也会不同 |
| strExtraData  | string | 透传字段，该字段会在客户端的回调，以及服务端的支付回调中原样返回。服务端的支付回调通知请参见服务端接入文档。（必要） |

+ 回调Event参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| R_CODE | string | 错误码 : 0成功，其它见后面统一错误码表 |
| R_MSG | string | 错误信息，辅助用 |
| EXTRADATA | string | 透传参数，发起购买请求时的透传字段 |
| ORDERID | string | 订单号，如果正确地发起了购买请求，该字段就是在AiriSDK的订单号 |

### 28、公用数据获取接口

| 属性 | 说明 | 
| ------ | ------ |
| AiriSDK.Instance.GetDeviceID() | 获取用户设备的唯一标识号 |
| AiriSdkData.Instance.AiriSDK_VERSION | SDK版本号 |


### 29、错误码

[错误码文档](https://github.com/Yostardev/yostarsdk/blob/master/docs/ZH/errorcode.md)

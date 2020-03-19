### 1、PC端调试

由于大部分功能都涉及到手机端原生API
暂时PC端调试仅仅开放了以下接口：
+ SDK初始化：
```csharp
public void Init()
```
+ 快速登陆：
```csharp
public void QuickLogin()
```
+ 设备号登陆：
```csharp
public void LoginWithDevice()
```
+ 继承码登陆：	
```csharp
ResultCode void LoginWithTranscode(string strTranscode, string strUid)
```

### 2、清除本地账号缓存

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
### 3、用户行为数据上报（数据统计）

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

### 4、分享游戏自定义图片

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

### 5、商店评分

调用该接口，可以在不跳转APPSTORE的前提下，自动给应用打分。

注意：单个用户每年只能使用三次，所以需要在合适的时机提示玩家。

+ 调用API: 	
```csharp
public void RequestStoreReview()
```
+ 调用示例： 
```csharp
using Airisdk;
AiriSDK.Instance.RequestStoreReview();
```

### 6、第三方客服HelpShift

调用该接口，会自动打开HelpShift第三方客服插件，玩家可以通过上面查看基本疑问或者向官方进行QA。

+ 调用API: 	
```csharp
public void OpenHelpShift()
```
+ 调用示例： 
```csharp
using Airisdk;
AiriSDK.Instance.OpenHelpShift();
```

### 7、第三方客服HelpShift(角色参数)

调用该接口，会自动打开HelpShift第三方客服插件，玩家可以通过上面查看基本疑问或者向官方进行QA。

+ 调用API:


```csharp
public void OpenHelpShift(string roleUid, string roleName, string roleLevel, string roleServer, string rolePurchase, string createTime)
```
+ API参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| roleUid | string | 角色ID |
| roleName  | string | 角色名称 |
| roleLevel  | string | 角色等级 |
| roleServer  | string | 角色所在服务器（格式：服务器ID - 服务器名称） |
| rolePurchase  | string | 角色在此服务器的充值金额（美元） |
| createTime  | string | 角色创建的时间（yyyy-mm-dd hh:MM:ss） |



+ 调用示例:


```csharp
using Airisdk;
AiriSDK.Instance.OpenHelpShift("11552233", "昨日方舟", 1+"", "2 - 雄霸天下",18 + "", "2019-08-06 10:57:11");
```

### 8、删除账号

调用该接口，会自动此账号与所有第三方的账号绑定，并清理本地缓存，删除服务器数据记录，请CP谨慎调用。

+ 调用API: 	
```csharp
public void DeleteAccount()
```
+ 调用示例： 
```csharp
using Airisdk;
AiriSDK.Instance.DeleteAccount();
```
+ 回调Event

```csharp
AirisdkEvent.Instance.DeleteAccountEvent
```
+ 回调Event类型
```
DeleteAccountRet
```
+ 回调Event参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| R_CODE | string | 错误码 : 0成功，其它见后面统一错误码表 |
| R_MSG | string | 错误信息，辅助用 |


### 9、恢复账号

调用该接口，会自动此账号与所有第三方的账号绑定，并清理本地缓存，删除服务器数据记录，请CP谨慎调用。

+ 调用API: 	
```csharp
public void RebornAccount()
```
+ 调用示例： 
```csharp
using Airisdk;
AiriSDK.Instance.RebornAccount();
```
+ 回调Event

```csharp
AirisdkEvent.Instance.RebornAccountEvent
```
+ 回调Event类型
```
RebornAccountRet
```
+ 回调Event参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| R_CODE | string | 错误码 : 0成功，其它见后面统一错误码表 |
| R_MSG | string | 错误信息，辅助用 |


### 10、公用数据获取接口

| 属性 | 说明 | 
| ------ | ------ |
| ```AiriSDK.Instance.GetDeviceID()``` | 获取用户设备的唯一标识号 |
| ```AiriSdkData.Instance.AiriSDK_VERSION``` | SDK版本号 |

### 11、确认用户协议

此接口再用户点击同意协议时调用。

+ 调用API: 	
```csharp
public void ConifrmAgreement()
```
+ 调用示例： 
```csharp
using Airisdk;
AiriSDK.Instance.ConifrmAgreement();
```

### 12、用户协议链接获取

此接口用于CP需要显示用户协议时调用

+ 调用API: 
```csharp
public string GetAgreement()
```
+ 调用示例:
```csharp
using Airisdk;
string greement_url = AiriSDK.Instance.GetAgreement();
```

+ 注意
此接口返回的是一个完整的网络链接，CP可以请求此链接获取到协议的相关信息
返回参数示例：
```
http://test.sdk.azurlane.jp:3011/user/agreement?version=v1.0.0
```
请求后获取的参数示例：
```json
{
    "version": "v1.0.0",
    "data": [
        "Part 1",
        "Part 2"
    ]
}
```

### 13、用户协议具体内容获取

+ 调用API：
```csharp
public void GetAgreementInfo()
```

+ 调用示例：
```csharp
AiriSDK.Instance.GetAgreementInfo();
```
+ 回调Event

```csharp
AirisdkEvent.Instance.GetAgreementEvent
```

+ 回调类型

```csharp
GetAgreementRet
```

+ 回调示例：

```csharp
using Airisdk.Event;
AirisdkEvent.Instance.GetAgreementEvent += OnGetAgreementResponse;
private void OnGetAgreementResponse(GetAgreementRet ret) {  
	//to do  
} 
```
+ 回调Event参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| R_CODE | string | 错误码 : 0成功，其它见后面统一错误码表 |
| R_MSG | string | 错误信息，辅助用 |
| Agreements | string | 具体的协议，格式位JsonArray字符串 |

+ 返回值Agreements示例

```json
["Part 1 ","Part 2"]
```

### 13、未成年人退款协议

+ 调用API：
```csharp
public void GetUnderAgeAgrement()
```

+ 调用示例：
```csharp
AiriSDK.Instance.GetUnderAgeAgrement();
```

+ 回调Event

```csharp
AirisdkEvent.Instance.GetUnderAgreementEvent
```

+ 回调示例：

```csharp
using Airisdk.Event;
AirisdkEvent.Instance.GetUnderAgreementEvent += OnGetUnderAgreementResponse;
private void OnGetUnderAgreementResponse(GetUnderAgreementRet ret)
{
//to do  
}
```

+ 回调Event参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| R_CODE | string | 错误码 : 0成功，其它见后面统一错误码表 |
| R_MSG | string | 错误信息，辅助用 |
| SHOP_AGREEMENT | string | 具体的协议，格式位JsonArray字符串 |
| isSHOW | int | 是否需要显示协议，1：需要，0：不需要 |


### 14、Google S2S接口

+ 调用API：
```csharp
public void GoogleServerToServer(string devToken, string linkID, string eventName, string priceValue, string currencyCode)
```

+ 调用示例：
```csharp
AiriSDK.Instance.GoogleServerToServer(
                "xxxxxxxxxxxxxxxxxxxxx",
                "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
                "xxxxxxxxxxxxxx S2S_purchase_click",
                "xxx",
                "USD"
            );
```


### 15、错误码信息返回接口

+ 调用API：
```csharp
public string GetSDKRecommendedErrorMsg(int code, LanguageType type)
```

+ 调用示例：
```csharp
string strMsg = AiriSDK.Instance.GetSDKRecommendedErrorMsg(100404, LanguageType.MSG_EN);
```

+ 参数说明：

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| code | int | 错误码 :具体的错误码为每个接口返回的R_CODE参数 |
| type | LanguageType | 语言参数，暂时只支持中文，英文，韩文，日文 |


### 16、剪贴板

+ 调用API：
```csharp
public ResultCode SDKToClipboard(string cValue);
```

+ 调用示例：
```csharp
ResultCode code = AiriSDK.Instance.SDKToClipboard(cValue);
if (code == ResultCode.OK) {
   Debug.Log("SUCCESS");
}
```

+ 参数说明：

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| cValue | string | 需要复制到剪贴板的内容 |

### 17、iOS系统是否支持Sign in with apple

+ 调用API：
```csharp
public bool IOSAppleSignInAvailable();
```

+ 调用示例：
```csharp
bool isAvailable = AiriSDK.Instance.IOSAppleSignInAvailable();
```




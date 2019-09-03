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

### 5、APPSTORE商店评分

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

### 6、第三方客服HelpShift

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

### 7、删除账号

调用该接口，会自动此账号与所有第三方的账号绑定，并清理本地缓存，删除服务器数据记录，请CP谨慎调用。

+ 调用API: 	
```csharp
public string SDKDeleteAccount()
```
+ 调用示例： 
```csharp
using Airisdk;
AiriSDK.Instance.SDKDeleteAccount();
```
+ 回调Event

```csharp
AirisdkEvent.Instance.DeleteAccountRet
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


### 8、公用数据获取接口

| 属性 | 说明 | 
| ------ | ------ |
| ```AiriSDK.Instance.GetDeviceID()``` | 获取用户设备的唯一标识号 |
| ```AiriSdkData.Instance.AiriSDK_VERSION``` | SDK版本号 |


### 9、错误码

[错误码文档](https://github.com/Yostardev/yostarsdk/blob/master/docs/ZH/errorcode.md)

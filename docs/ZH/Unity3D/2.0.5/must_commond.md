
### 1、初始化

初始化只需要调用一次。在调用其它的任何API前，必须执行初始化。初始化结果会在回调EVENT中给出。

 + 调用API:		
 ```csharp
 public void Init(PayStore payStore)
 ```
 + 调用示例:
```csharp
using Airisdk;
AiriSDK.Instance.Init(PayStore.appstore);
```
+ 参数说明:

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
|payStore|PayStore|对应的支付平台|
```csharp
public enum PayStore
    {
        googleplay,
        appstore,
        au,
        amazon,
        onestore,
        samsung,
    };
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
| ISCACHE | Int | 是否存在登陆缓存，存在1，不存在0 |
| LOGIN_PLATFORM | LoginPlatform（枚举） | 缓存登陆的平台 |
| LOGIN_UID | string | 缓存的UID |
| LOGIN_NAME | string | 缓存的名称 |
| IS_POPUP_AGREEMENT | Int | 是否需要弹出公告栏，1：需要 ，0：不需要 |

### 2、后台切换

在unity程序前后台切换时调用。
**OnResume需要在初始化成功后额外调用一次。**

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

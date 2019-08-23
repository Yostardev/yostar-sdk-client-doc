
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

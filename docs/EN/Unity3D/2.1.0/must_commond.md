
### 1、Initialization

Initialization only needs to be called once and must be performed before calling any other API. The initialization result will be given in the callback ```EVENT```.

 + Calling API:		
 ```csharp
 public void Init()
 ```
 + Examples of API Call:
```csharp
using Airisdk;
AiriSDK.Instance.Init();
```
 + Callback EVENT		
```csharp
AirisdkEvent.Instance.InitEvent
```
 + Callback Event Type:
```csharp
InitRet
```
+ Callback Parameter Description

| Parameter Name | Parameter Type | Parameter Description |
| ------ | ------ | ------ |
| R_VIRTUAL | Int | Whether it is simulator 1: Simulator 0: Real machine |
| R_CODE | ResultCode | Error code: 0 success. See Error Code Table for other error codes. |
| R_MSG | string | Error message, auxiliary |
| ISCACHE | Int | Whether the login cache exists, 1 Exists, 0 Does not exist |
| LOGIN_PLATFORM | LoginPlatform | Cached Login Platform |
| LOGIN_UID | string | Cached UID |
| LOGIN_NAME | string | Cached Name |
| IS_POPUP_AGREEMENT | Int | Whether to pop up the bulletin board, 1: Required, 0: Not required |

### 2、Backend Switch

Called when the unity program switches between the frontend and the backend. 
```OnResume``` needs to be called once after the initialization succeeds.

+ Calling API:		

```csharp
public void OnResume()
```
```csharp
public void OnPause()
```
+ Examples of API Call:
```csharp
using Airisdk;
private void OnApplicationPause(bool isPause)
{
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

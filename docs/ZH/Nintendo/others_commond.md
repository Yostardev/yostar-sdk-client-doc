### 1、用户协议链接获取

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

### 2、用户协议具体内容获取

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


### 3、确认用户协议

此接口再用户点击同意协议时调用。

+ 调用API: 	
```csharp
public void ConifrmAgreement()
```
+ 调用示例： 
```csharp
using Airisdk;
AiriSDK.Instance.ConifrmAgreement();
``


### 17、错误码信息返回接口

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




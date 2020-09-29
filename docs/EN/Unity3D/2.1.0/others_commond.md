
### 1、PC-side Debugging

Since the native API on mobile phone is involved in most of the functionalities, the PC-side debugging is open for the following interfaces for now:
+ SDK Initialization:：
```csharp
public void Init()
```
+ Quick Login：
```csharp
public void QuickLogin()
```
+ Device Number Login
```csharp
public void LoginWithDevice()
```
+ Inheritance Code Login	
```csharp
ResultCode void LoginWithTranscode(string strTranscode, string strUid)
```

### 2、Clear Local Account Cache

Call this interface to clear the account information on the device.

Note: After clearing the account information, you will not be able to log in using the most recent account directly. Need to log in again with FB/TW/Yostar accounts.

Note: Please call the interface with caution and confirm with the player for multiple times before the execution.

Note: If the player does not have inheritance code, FB, TW or Yostar account, clearing the account data will make it difficult to recover the account.

+ Calling API: 	
```csharp
public void ClearAccountInfo()
```
+ Examples of API Call: 
```csharp
using Airisdk;
AiriSDK.Instance.ClearAccountInfo();
```
+ Callback Event:	
```csharp
AirisdkEvent.Instance.ClearAccountEvent
```
+ Callback Event Type:	
```csharp
ClearAccountInfoRet
```
+ Examples of Callback Event:
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.ClearAccountEvent+= OnClearAccountRespone;
private void OnClearAccountRespone(ClearAccountInfoRet ret) {  
	//to do  
} 
```
### 3、User Behavior Data Report (data statistics)

Calling these interfaces can notify the SDK server of some user events. Which user events are required will be negotiated by the SP and the CP.

+ Calling API: 	
```csharp
public void UserEventUpload(string strEventName, Dictionary<string, string> strCallbackParameter = null)
```
+ Examples of API Call： 
```csharp
using Airisdk;
Dictionary<string, string> dicParam = new Dictionary<string, string>();
dicParam.Add("test1", "test1");
dicParam.Add("test2", "test2");
AiriSDK.Instance.UserEventUpload(m_inputEventName.text, dicParam);
```

+ Interface parameter description

| Parameter Name | Parameter Type | Parameter Description |
| ------ | ------ | ------ |
| strEventName | string | Event Name (provided by the SP) (required) |
| strCallbackParameter | Dictionary<string, string> | Callback Parameters (provided by the SP) (not required) |

### 4、Share Game Customized Pictures

Calling this interface could share customized Texture2D on iOS or through native share of Android. This interface obtains texture data from the parameter texture.

+ Calling API: 	
```csharp
public void SystemShare(string strShareText, Texture2D texShare = null)
```
+ Examples of API Call： 
```csharp
using Airisdk;
Texture2D screenShot = GetScreeShot()；
AiriSDK.Instance.SystemShare("test share", screenShot)；
```
+ Callback Event：	
```csharp
AirisdkEvent.Instance.SystemShareEvent
```

+ Examples of Callback Event：
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.SystemShareEvent += OnSystemShareRespone;
private void OnSystemShareRespone(SystemShareRet ret) {  
	//to do  
} 
```
+ Interface parameter description

| Parameter Name | Parameter Type | Parameter Description |
| ------ | ------ | ------ |
| strShareText | string | Share Text (required) |
| texShare  | Texture2D | Share Pictures (required) |

+ Callback EventParameter Description

| Parameter Name | Parameter Type | Parameter Description |
| ------ | ------ | ------ |
| R_CODE | string | Error code: 0 success. See Error Code Table for other error codes. |
| R_MSG | string | Error message, auxiliary |

### 5、APPSTORE Store Rating

Calling this interface could automatically rate the application without jumping to APPSTORE.

Note: The API can only be used three times a year on a single user. You should prompt the player with perfect timing.

+ Calling API: 	
```csharp
public void RequestStoreReview()
```
+ Examples of API Call： 
```csharp
using Airisdk;
AiriSDK.Instance.RequestStoreReview();
```

### 6、Third-party Customer Service AiHelp

Calling this interface will automatically open the AiHelp third-party customer service plug-in. Players can view FAQ on it or make direct inquiry to the developer team.

+ Calling API: 	
```csharp
public void ShowAiHelpFAQs()
```
+ Examples of API Call： 
```csharp
using Airisdk;
AiriSDK.Instance.ShowAiHelpFAQs();
```

### 7、Third-party Customer Service AiHelp (role parameters)

Calling this interface will automatically open the AiHelp third-party customer service plug-in. Players can view FAQ on it or make direct inquiry to the developer team.

+ Calling API:


```csharp
public void ShowAiHelpFAQs(string serverId, string roleUid, string roleName, string roleCreateTime, int purchase, string[] tags)
```
+ APIParameter Description

| Parameter Name | Parameter Type | Parameter Description |
| ------ | ------ | ------ |
| serverId | string | Server ID |
| roleUid | string | Role ID |
| roleName  | string | Role Name |
| roleCreateTime  | string | When the role was created（yyyy-MM-dd） |
| purchase  | int | 充值金额 |
| tags  | string[] | 标签数组 |




+ Examples of API Call:


```csharp
using Airisdk;
AiriSDK.Instance.ShowAiHelpFAQs("serverId", "id123456", "roleName_one", "2020-09-10", 1000, {"bad_user", "bug"});
```



### 8、Delete account

Calling this interface will automatically bind this account to all third-party accounts, and clear the local cache, delete server data records. CP needs to call it with caution.

+ Calling API: 	
```csharp
public void DeleteAccount()
```
+ Examples of API Call： 
```csharp
using Airisdk;
AiriSDK.Instance.DeleteAccount();
```
+ Callback Event

```csharp
AirisdkEvent.Instance.DeleteAccountEvent
```
+ Callback Event Type
```
DeleteAccountRet
```
+ Callback EventParameter Description

| Parameter Name | Parameter Type | Parameter Description |
| ------ | ------ | ------ |
| R_CODE | string | Error code: 0 success. See Error Code Table for other error codes. |
| R_MSG | string | Error message, auxiliary |


### 9、Recover Account

Calling this interface will automatically bind this account to all third-party accounts, and clear the local cache, delete server data records. CP needs to call it with caution.

+ Calling API: 	
```csharp
public void RebornAccount()
```
+ Examples of API Call： 
```csharp
using Airisdk;
AiriSDK.Instance.RebornAccount();
```
+ Callback Event

```csharp
AirisdkEvent.Instance.RebornAccountEvent
```
+ Callback Event Type
```
RebornAccountRet
```
+ Callback EventParameter Description

| Parameter Name | Parameter Type | Parameter Description |
| ------ | ------ | ------ |
| R_CODE | string | Error code: 0 success. See Error Code Table for other error codes. |
| R_MSG | string | Error message, auxiliary |


### 10、Public Data Acquisition Interface

| Interface | Parameter Description | 
| ------ | ------ |
| ```AiriSDK.Instance.GetDeviceID()``` | Obtain the unique identification number of the user device |
| ```AiriSdkData.Instance.AiriSDK_VERSION``` | SDK Version Number |

### 11、Confirm User Agreement

This interface is called when the user clicks to approve the User Agreement.

+ Calling API: 	
```csharp
public void ConifrmAgreement()
```
+ Examples of API Call： 
```csharp
using Airisdk;
AiriSDK.Instance.ConifrmAgreement();
```

### 12、Obtain the Link of the User Agreement

This interface is used when the CP needs to display the User Agreement.

+ Calling API: 
```csharp
public string GetAgreement()
```
+ Examples of API Call:
```csharp
using Airisdk;
string greement_url = AiriSDK.Instance.GetAgreement();
```

+ Note
Note This interface returns a complete web link. CP can request to obtain relevant information about the agreement from the link. Examples of return parameters:
```
http://test.sdk.azurlane.jp:3011/user/agreement?version=v1.0.0
```

```json
{
    "version": "v1.0.0",
    "data": [
        "Part 1",
        "Part 2"
    ]
}
```

### 13、User Agreement Content Acquisition

+ Calling API：
```csharp
public void GetAgreementInfo()
```

+ Examples of API Call：
```csharp
AiriSDK.Instance.GetAgreementInfo();
```
+ Callback Event

```csharp
AirisdkEvent.Instance.GetAgreementEvent
```

+ Callback Event Type:

```csharp
GetAgreementRet
```

+ Examples of Callback Event:：

```csharp
using Airisdk.Event;
AirisdkEvent.Instance.GetAgreementEvent += OnGetAgreementResponse;
private void OnGetAgreementResponse(GetAgreementRet ret) {  
	//to do  
} 
```
+ Callback EventParameter Description

| Parameter Name | Parameter Type | Parameter Description |
| ------ | ------ | ------ |
| R_CODE | string | Error code: 0 success. See Error Code Table for other error codes. |
| R_MSG | string | Error message, auxiliary |
| Agreements | string | The content of the agreement in the format of JsonArray string. |

+ Examples of the Return Value, Agreements

```json
["Part 1 ","Part 2"]
```

### 14、Minor Refund Agreement

+ Calling API：
```csharp
public void GetUnderAgeAgrement()
```

+ Examples of API Call：
```csharp
AiriSDK.Instance.GetUnderAgeAgrement();
```

+ Callback Event

```csharp
AirisdkEvent.Instance.GetUnderAgreementEvent
```

+ Examples of Callback Event:：

```csharp
using Airisdk.Event;
AirisdkEvent.Instance.GetUnderAgreementEvent += OnGetUnderAgreementResponse;
private void OnGetUnderAgreementResponse(GetUnderAgreementRet ret)
{
//to do  
}
```

+ Callback EventParameter Description

| Parameter Name | Parameter Type | Parameter Description |
| ------ | ------ | ------ |
| R_CODE | string | Error code: 0 success. See Error Code Table for other error codes. |
| R_MSG | string | Error message, auxiliary |
| SHOP_AGREEMENT | string | Structral Agreement, format bit JsonArray string |
| isSHOW | int | Do you want Agreement to display? 1: Yes 0: No |

### 15、Google S2S Interface

+ Calling API：
```csharp
public void GoogleServerToServer(string devToken, string linkID, string eventName, string priceValue, string currencyCode)
```

+ Examples of API Call：
```csharp
AiriSDK.Instance.GoogleServerToServer(
                "xxxxxxxxxxxxxxxxxxxxx",
                "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
                "xxxxxxxxxxxxxx S2S_purchase_click",
                "xxx",
                "USD"
            );
```


### 16、Error Code Message Return Interface

+ Calling API：
```csharp
public string GetSDKRecommendedErrorMsg(int code, LanguageType type)
```

+ Examples of API Call：
```csharp
string strMsg = AiriSDK.Instance.GetSDKRecommendedErrorMsg(100404, LanguageType.MSG_EN);
```

+ Parameter Description：

| Parameter Name | Parameter Type | Parameter Description |
| ------ | ------ | ------ |
| code | int | R_CODE |
| type | LanguageType | Language parameters, currently only supports Chinese, English, Korean and Japanese |


### 17、Clipboard

+ Calling API：
```csharp
public ResultCode SDKToClipboard(string cValue);
```

+ Examples of API Call：
```csharp
ResultCode code = AiriSDK.Instance.SDKToClipboard(cValue);
if (code == ResultCode.OK) {
   Debug.Log("SUCCESS");
}
```

+ Parameter Description：

| Parameter Name | Parameter Type | Parameter Description |
| ------ | ------ | ------ |
| cValue | string | Content that needs to be copied to the clipboard |

### 18、Does the iOS system support Sign in with apple

+ Calling API：
```csharp
public bool IOSAppleSignInAvailable();
```

+ Examples of API Call：
```csharp
bool isAvailable = AiriSDK.Instance.IOSAppleSignInAvailable();
```

### 19、Minor Agreement confirmed

+ Calling API：
```csharp
public void ConfirmUnderAger();
```

+ Examples of API Call：
```csharp
AiriSDK.Instance.ConfirmUnderAger();
```



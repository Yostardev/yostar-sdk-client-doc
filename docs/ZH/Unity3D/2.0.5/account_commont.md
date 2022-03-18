
### 1、游客登陆

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

### 2、快速登陆

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

### 3、Facebook登陆

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

### 4、Google邮箱登陆

使用Google账号登陆游戏，若第一次使用Google账号登陆，会自动创建SDK ID。

+ 调用API:		
```csharp
public void LoginWithGoogle()
```
+ 调用示例:
```csharp
using Airisdk;
AiriSDK.Instance.LoginWithGoogle();
```
+ 回调Event:
```csharp
AirisdkEvent.Instance.LoginEvent
```

### 5、GooglePlayGames登陆
LoginWithGooglePlay方法在2.1.60已废弃；
+ GooglePlayGames在调用初始化后会自动验证登录。
+ GooglePlayGames在调用登录后会与账号自动绑定。
其中游客账号不能绑定，会返回PLAY_GAME_ACCOUNT_CAN_NOT_LINK_GUEST；
第三方账号（游客绑定过第三方也算）会直接绑定，如果有绑定冲突会返回PLAY_GAME_ACCOUNT_LINK_OTHER_UID_ALREADY、UID_LINK_OTHER_PLAY_GAME_ACCOUNT_ALREADY、UID_AND_PLAY_GAME_ACCOUNT_ALL_LINKED_OTHER，如果要强制绑定可以调用ConfirmLinkGooglePlayGame方法；

+ 接入示例:
请查看 【配置工程参数-8、GooglePlayGames配置】

+ 调用示例:
```csharp
If(rc == ResultCode.OK){
  //todo suc
} else if (rc == ResultCode.PLAY_GAME_ACCOUNT_LINK_OTHER_UID_ALREADY){
//todo
} else if (rc == ResultCode.UID_LINK_OTHER_PLAY_GAME_ACCOUNT_ALREADY){
 //todo
} else if (rc == ResultCode.UID_AND_PLAY_GAME_ACCOUNT_ALL_LINKED_OTHER){
 //todo
} else if (rc == ResultCode.PLAY_GAME_ACCOUNT_CAN_NOT_LINK_GUEST){
 //todo
} else {
//todo
}
```
+ 回调Event:
```csharp
AirisdkEvent.Instance.LoginEvent
```

### 6、Apple登陆

使用Apple账号登陆游戏，若第一次使用Apple登陆，会自动创建SDK ID。

+ 调用API:		
```csharp
public void LoginWithApple()
```
+ 调用示例:
```csharp
using Airisdk;
AiriSDK.Instance.LoginWithApple();
```
+ 回调Event:
```csharp
AirisdkEvent.Instance.LoginEvent
```

### 7、Twitter登陆

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

### 8、Amazon登陆

使用amazon账号登陆游戏，若第一次使用amazon账号登陆，会自动创建SDK ID。

调用API:		
```csharp
public void LoginWithAmazon()
```
调用示例: 
```csharp
using Airisdk;
AiriSDK.Instance.LoginWithAmazon();
```
回调Event:	
```csharp
AirisdkEvent.Instance.LoginEvent 
```

### 9、继承码登陆

使用继承码登陆游戏，继承码信息获取需要调用独立API获取，下面解释。调用函数返回值ResultCode（后续文章专门介绍）仅用来验证参数合法性，实际成功与否需要根据LoginEvent的返回数据进行判断。

+ 调用API: 		
```csharp
ResultCode void LoginWithMigrationCode(string strTranscode, string strUid)
```
+ 调用示例： 
```csharp
using Airisdk;
ResultCode rc = AiriSDK.Instance.LoginWithMigrationCode(strcode, struid);
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


### 10、继承码获取

在登陆游戏后，调用该API可以获取到当前账号的继承码和UID信息，当在未绑定第三方账号时，更换设备等可以通过继承码登陆找回之前账号。

+ 调用API: 
```csharp
public void MigrationCodeRequest()
```
+ 调用示例:
```csharp
using Airisdk;
AiriSDK.Instance.MigrationCodeRequest();
```
+ 回调Event:			
```csharp
AirisdkEvent.Instance.MigrationCodeEvent
```
+ 回调Event类型:	
```csharp
MigrationCodeRet
```
+ 回调Event参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| R_CODE | string | 错误码 : 0成功，其它见后面统一错误码表 |
| R_MSG | string | 错误信息，辅助用 |
| MIGRATIONCODE | string | 继承码 |
| UID | string | SDK UID |

+ 回调Event 示例

```csharp
using Airisdk.Event;
AirisdkEvent.Instance.MigrationCodeEvent += OnMigrationRespone;
private void OnMigrationRespone(MigrationCodeRet ret) {  
  //to do  
} 
```

### 11、登陆统一回调EVENT

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
| GOOGLE_EMAIL | string | Google登陆或绑定的Google邮箱 |
| SDK_NAME | string | 悠星账号登陆的名称 |
| ISCAN_BIND_GUEST | int | 是否可以绑定游客账号(0不可以绑定, 非0可以绑定)，发生在用新FB、TW、悠星账号登陆时，同时检测到相同设备上一次登陆过游客账号。则可以调用API NewAccountLink() 进行绑定，也可不绑定。 |
| R_DELETETIME | string | 时间单位(单位：毫秒),最终确定删除此账号的时间，在这个时间之前，可通过调用恢复账号接口来取消账号删除 |
| ISNEW | int | 是否为新账号，1：是新账号，0：不是新账号 |
| R_COOL_WAIT_DAY | int | 冷静期天数 |
| MIGRATIONCODE | string | 继承码，账号没有继承码或者继承码过期时，参数为空 |
| AMAZON_NAME | string | 用于标识是否绑定亚马逊账号 |
| CHANNEL_ID| int| 账户创建的渠道，-1：未知，0：Google，1：Apple，2：au，3：Amazon，4：onestore，5：Samsung |

+ 回调Event 示例：
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.LoginEvent+= OnLoginRespone;
private void OnLoginRespone(LoginRet ret) {  
  //to do  
} 
```

### 12、悠星账号登陆

悠星账号登陆成功后，回调EVENT还是登陆回调。调用函数返回值ResultCode（后续文章专门介绍）仅用来验证参数合法性，实际成功与否需要根据LoginEvent的返回数据进行判断。

+ 调用API: 	
```csharp
ResultCode void LoginWithSDK(string strEmail, string strVerificationCode)
```

+ 调用示例： 
```csharp
using Airisdk;
ResultCode rc = AiriSDK.Instance.LoginWithSDK(strEmail, strVerificationCode);
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

### 13、悠星账号验证码获取

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


### 14、获取当前SDK登陆信息

+ 调用API：

```csharp
public string SDKGetUID();
public string SDKGetAccessToken();
```

+ 调用示例：

```csharp
string Sdk_Uid = AiriSDK.Instance.SDKGetUID();
string Sdk_AccessToken = AiriSDK.Instance.SDKGetAccessToken();
```

+ 接口说明：

`SDKGetUID`接口用于获取当前的SDK UID，
`SDKGetAccessToken`接口用于获取当前缓存的SDK AccessToken，AccessToken用于游戏验证登陆的有效性


### 15、删除账号

调用该接口，会将此账号与所有第三方的账号解绑定，并清理本地缓存；在冷静期内可以通过调用恢复账号接口来取消操作；

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
| R_COOL_WAIT_DAY | int | 冷静期天数，在冷静期内可以调用恢复账号接口取消删除操作 |
| R_DELETETIME | string | 真正删除的时间，过期后即便调用恢复账号接口也无法恢复 |
| HAS_COOL_DAYS | int | 1：有冷静期；0：无冷静期 |


### 16、恢复账号

在冷静期内调用该接口，取消删除操作。

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


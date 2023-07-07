

### 功能概述

为了让开发人员能更好的理解我们的SDK的账户登录&验证流程，我们为游戏开发人员绘制了下列登录时序图:

![登陆时序图](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/sdk_login.jpg)



### 1、Nintendo登录

使用Nintendo账号登陆游戏；

+ 调用API:		
```csharp
public void LoginWithNintendo();
```
+ 调用示例:
    ```csharp
    using Airisdk;
    private void OnLoginRespone(LoginRet ret)
    {
  
        if (ret.R_CODE == ResultCode.OK)
        {
            // 登录成功，进入游戏
        }else if(ret.R_CODE == ResultCode.NINTENDO_ACCOUNT_UNLINK_UID) //该nintendo账号下没有绑定uid
        {
               //改用悠星账号登录，可弹窗让用户输入邮箱账号和验证码进行登录
              AiriSDK.Instance.LoginWithSDK(strEmail, strVerificationCode);
      
        }else if(ret.R_CODE == ResultCode.YOSTAR_ACCOUNT_NOT_EXIST)
        {
               //提示用户: 用户输入的邮箱号是个新号，是否需要创建游戏账号并与Nintendo账号绑定？
               //确定:  AiriSDK.Instance.ConfirmCreateLinkNintendo();
               //取消: 返回登陆界面
  
        }else if (ret.R_CODE == ResultCode.YOSTAR_ACCOUNT_LINKED_NINTENDO_ALREADY)
        {
                  //  提示用户:输入的邮箱悠星账号已和其他nintendo账号绑定，不可在本机登录；
        }else if (ret.R_CODE == ResultCode.YOSTAR_ACCOUNT_UNLINKED_NINTENDO)
        {
                 //提示用户: 用户输入的邮箱悠星号，没有和nintendo账号绑定过，提示是否需要绑定？
                 //确定:  AiriSDK.Instance.ConfirmLinkNintendo();
                 //取消: 返回登陆界面
         }else{
 
            //提示用户: 登录失败
         }
    }
    
    AirisdkEvent.Instance.LoginEvent += OnLoginRespone;
    
    AiriSDK.Instance.LoginWithNintendo();
    ```


+ 回调LoginRet参数说明

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
| R_DELETETIME | string | 时间单位(单位：毫秒),最终确定删除此账号的时间，在这个时间之前，账号都是可以恢复的 |
| ISNEW | int | 是否为新账号，1：是新账号，0：不是新账号 |
| MIGRATIONCODE | string | 继承码，账号没有继承码或者继承码过期时，参数为空 |
| AMAZON_NAME | string | 用于标识是否绑定亚马逊账号 |
| CHANNEL_ID| int| 账户创建的渠道，-1：未知，0：Google，1：Apple，2：au，3：Amazon，4：onestore，5：Samsung, 6:Nintendo |



### 2、悠星账号登录
该函数不可主动发起调用，需在调用 LoginWithNintendo登录，LoginEvent登录回调R_CODE为 400050(释义见错误码表) 时,才可调用本函数；

+ 调用API: 	
```csharp
ResultCode void LoginWithSDK(string strEmail, string strVerificationCode)
```

+ 调用示例： 
    ```csharp
    using Airisdk;
    private void OnLoginRespone(LoginRet ret)
    {
    }
    
    AirisdkEvent.Instance.LoginEvent += OnLoginRespone;
        
    ResultCode rc = AiriSDK.Instance.LoginWithSDK(strEmail, strVerificationCode);
    if(rc == ResultCode.OK){
      //suc  入参格式正确
    } else { 
      //fail  入参格式错误，检查邮箱格式
    }
    ```

+ 接口参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| strEmail | string | 邮箱地址（必要） |
| strVerificationCode | string | 发给邮箱的验证码（必要） |

### 3、悠星账号验证码获取

请求获取悠星账号系统的验证码，验证码会发送到传入的邮箱内，回调接口不会包含验证码。

+ 调用API: 	
```csharp
ResultCode void VerificationCodeReq(string strEmail)
```

+ 接口参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| strEmail | string | 邮箱地址（必要） |


+ 调用示例:
    ```csharp
    using Airisdk;
    private void OnVerificationCodeResponse(VerificationCodeRet ret)
    {
    }
    AirisdkEvent.Instance.VerificationCodeEvent += OnVerificationCodeResponse;
    
    ResultCode rc = AiriSDK.Instance.VerificationCodeReq(strEmail);
    if(rc == ResultCode.OK){
          //suc  入参格式正确
       } else {
          //fail  入参格式错误，检查邮箱格式
      }
    ```

+ 回调VerificationCodeRet参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| R_CODE | string | 错误码 : 0成功，其它见后面统一错误码表 |
| R_MSG | string | 错误信息，辅助用 |



### 4、删除账号

调用该接口，会自动删除此账号与所有第三方的账号绑定，删除服务器数据记录，请CP谨慎调用。

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


### 5、恢复账号

调用该接口，可恢复被删除后还处于冷静期内的账号。

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


### 6、账号绑定系统

调用函数返回值ResultCode（后续文章专门介绍）仅用来验证参数合法性，实际成功与否需要根据LinkEvent的返回数据进行判断。后面会介绍。

注意：Nintendo平台，只可以绑定Nintendo账号

+ 调用API: 	

```csharp
ResultCode void LinkSocial(LoginPlatform platform)
```
+ 调用示例： 
```csharp
using Airisdk;
ResultCode rc = AiriSDK.Instance.LinkSocial(LoginPlatform.NINTENDO);
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



### 7、绑定回调EVENT

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

### 8、账号解绑系统

API说明：调用函数返回值ResultCode（后续文章专门介绍）仅用来验证参数合法性，实际成功与否需要根据UnLinkEvent的返回数据进行判断。

注意：：Nintendo平台，只可以解绑Nintendo账号

+ 调用API: 	
```csharp
ResultCode void UnlinkSocial(LoginPlatform platform)
```
+ 调用示例:
```csharp
using Airisdk;
AiriSDK.Instance.UnlinkSocial(LoginPlatform.NINTENDO);
```
+ 接口参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| platform | LoginPlatform（枚举） | 平台类型（必要） |


### 9、解绑回调EVENT

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

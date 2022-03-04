
### 1、初始化

初始化只需要调用一次。在调用其它的任何API前，必须执行初始化。初始化结果会在回调EVENT中给出。

+ 调用API:		
 ```csharp
 public  bool Init(PayStore payStore,string mountName,nn.account.UserHandle mUserHandle);
 ```

+ 入参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| payStore | PayStore枚举 | 出包平台 |
| mountName | string | 数据持久化路径 |
| mUserHandle | UserHandle | nintendo账号对应的UserHandle |


+ 调用示例:
 
    ```csharp
    using Airisdk;
    #if UNITY_SWITCH
    using Airisdk.ns;
    #endif
    
        private void OnInitRespone(InitRet ret)
        {
        }
        AirisdkEvent.Instance.InitEvent += OnInitRespone;
    
        bool bIsInitSuc = AiriSDK.Instance.Init(PayStore.nintendo,"mountName",openedUserHandle);
        if (!bIsInitSuc)
        {
            Debug.LogError("SDK Init Failed");
        }
    
    ```


+ 回调InitRet参数说明

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


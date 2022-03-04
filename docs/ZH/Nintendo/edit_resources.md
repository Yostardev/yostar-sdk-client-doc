
### 获取接入参数

在接入前，请联系AiriSDK平台的负责人员，获取应用的接入参数：

| 参数名称 | 参数说明 |
| ------ | ------ | 
| Test SdkUrl | 分配的AiriSDK测试服务器访问地址 |
| Release SdkUrl | 分配的AiriSDK正式服务器访问地址 |

以上参数是在SDK初始化时需要的参数。这些参数可以使得SDK能够正常使用nintendo账号、支付系统。

### 创建和设置config文件

首次导入SDK包，请创建config asset文件，菜单如下图

![config_accsets](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/config_assets.png)

创建成功后会在目录
..\Assets\AiriSDK\Resources\下生成文件ConfigSettings.asset，点击后在inspecrtor如下图

![airisdk_setting](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/unity_config.png)

#### Save config

从AiriSDK平台的负责方那里获取到对应的参数，并在ConfigSettings中完整填写，点击```Save Config``` 按钮，会在同目录下生成文件 ```SDKConfigSettings.json```。该数据会在游戏运行时由SDK读取。

注意：填写正确后必须执行，否则游戏运行时讲获取不到SDK配置数据


### 设置Nintendo出包参数

appid、data sie
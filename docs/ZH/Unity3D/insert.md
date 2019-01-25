### 接入前期准备

在接入前，请联系AiriSDK平台的负责人员，获取分配给您的应用的以下参数：

| 参数名称 | 参数说明 |
| ------ | ------ | 
| Test SdkUrl | 分配的AiriSDK测试服务器访问地址 |
| Release SdkUrl | 分配的AiriSDK正式服务器访问地址 |
| Facebook AppID | 分配的facebook AppID |
| Twitter Key | 分配的Twitter Key |
| 安卓包名 | 安卓注册用包名 |
| IOS BUNDLEID | 苹果注册bundleid |
| HelpShift 各参数 | 第三方客服需要的参数 |

以上参数是在SDK初始化时锁需要的参数。这些参数可以使得SDK能够正常使用账号系统。支付系统的正常工作还需要服务端程序进行配合，请参考AiriSDK(JP)服务端集成文档。

### SDK配置

+ 导入SDK文件

在和本文档一起提供的压缩包中，可以找到 AiriSDK.unitypackage 。
在Unity编辑器打开了您的游戏工程后，双击即可通过正常的流程导入所需的文件。
在导入时请注意AndroidManifest.xml的导入与覆盖。若您已经有正在使用的Manifest文件，
请参见 “AiriSDK_AndroidManifest文件说明.doc”。

确认Plugins文件夹内容以及更新

![logo](https://github.com/Yostardev/yostarsdk/blob/master/docs/_media/plugin.png)

以上是unitypackage的所有内容。在更新时，可以将上面除了AndroidManifest.xml文件以外的都删除后，重新导入。

+ BundleID（包名）规范

从AiriSDK平台的负责人员处，可以获知您的应用在Google Play、iTunes Store及其它渠道（例如AU）中使用的游戏包名。您可以在Unity的PlayerSettings中Android及iOS的设置中设置成对应的包名。

![BundleId](https://github.com/Yostardev/yostarsdk/blob/master/docs/_media/bundleid_unity.png)

### SDK配置文件设置
#### 创建和设置config文件

首次导入SDK包，请创建config asset文件，菜单如下图

![config_assets](https://github.com/Yostardev/yostarsdk/blob/master/docs/_media/config_assets.png)

创建成功后会在目录
..\Assets\AiriSDK\Resources\下生成文件ConfigSettings.asset，点击后在inspecrtor如下图

![config_setting](https://github.com/Yostardev/yostarsdk/blob/master/docs/_media/config_setting.png)

#### Save config

从AiriSDK平台的负责方那里获取到对应的参数，并在ConfigSettings中完整填写，点击Save Config 按钮，会在同目录下生成文件 SDKConfigSettings.json。该数据会在游戏运行时由SDK读取。
注意：填写正确后必须执行，否则游戏运行时讲获取不到SDK配置数据

#### Modify manifest

ConfigSettings填写完整正确参数后，点击Modify Manifest，会将manifest下的参数修改成填写的参数内容。
注意：填写正确后必须执行，否则HELPSHIFT功能失效

#### modify google service params

从AiriSDK平台的负责方获取文件google-services.json，并替换目录
..\Assets\Plugins\Android\assets下相同文件
执行此操作，会将替换目录文件
..\Assets\Plugins\Android\res\values\google_service_strings.xml中的各项参数，用于	 
google firebase 使用
注意：填写正确后必须执行，否则ADJUST、HELPSHIFT功能将受到影响

### AndroidManifeset.xml配置

####


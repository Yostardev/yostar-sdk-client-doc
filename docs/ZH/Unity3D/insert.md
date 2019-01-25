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

### SDK接入

+ 导入SDK文件

在和本文档一起提供的压缩包中，可以找到 AiriSDK.unitypackage 。
在Unity编辑器打开了您的游戏工程后，双击即可通过正常的流程导入所需的文件。
在导入时请注意AndroidManifest.xml的导入与覆盖。若您已经有正在使用的Manifest文件，
请参见 “AiriSDK_AndroidManifest文件说明.doc”。

确认Plugins文件夹内容以及更新

![logo](https://github.com/Yostardev/yostarsdk/blob/master/docs/_media/plugin.png)

以上是unitypackage的所有内容。在更新时，可以将上面除了AndroidManifest.xml文件以外的都删除后，重新导入。

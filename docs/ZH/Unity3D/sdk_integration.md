

### 下载资源文件

[AiriSDK.unitypackage](https://sdkresources.oss-cn-shanghai.aliyuncs.com/YostarSDK/2.0.4/AiriSDK_2.0.4_f9.unitypackage)

### 资源文件导入到项目

在Unity编辑器打开了您的游戏工程后，双击下载的资源文件即可通过正常的流程导入所需的文件。
在导入时请注意AndroidManifest.xml的导入与覆盖。若您已经有正在使用的Manifest文件，
请参见 "配置工程参数"。

#### 确认Plugins文件夹内容以及更新

![logo](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/plugin.png)

以上是unitypackage的所有内容。在更新时，可以将上面除了AndroidManifest.xml文件以外的都删除后，重新导入。

### BundleID（包名）规范

从AiriSDK平台的负责人员处，可以获知您的应用在Google Play、iTunes Store及其它渠道（例如AU）中使用的游戏包名。您可以在Unity的PlayerSettings中Android及iOS的设置中设置成对应的包名。

![BundleId](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/bundleid_unity.png)

### 1.x版本更新到2.x版本

+ 旧版本资源务必删除干净，不然可能会造成打包过程中资源冲突的问题
+ 旧版本和新版本的接口调用不一致，请仔细查看2.x的接入文档，以免造成接口调用失败。
+ 为了Firebase工作，需要替换新版SDK的Android\assets\google-services.json文件，并根据modify google service params进行配置工作

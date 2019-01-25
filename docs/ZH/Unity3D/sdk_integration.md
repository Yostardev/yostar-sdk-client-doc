
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

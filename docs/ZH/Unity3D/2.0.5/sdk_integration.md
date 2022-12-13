


### Step1 获取SDK接入包和SDK接入参数
联系悠星运营获取下列SDK接入包,以及接入配置参数:

- **AiriSDK_2.x.x.unitypackage** &nbsp;&nbsp;&nbsp;(*AiriSDK For Unity*)
- **SDK接入配置参数表**

| 参数名称 | 参数说明                                                     |
| -- |----------------------------------------------------------|
| Test SdkUrl | 分配的AiriSDK测试服务器访问地址                                      |
| Release SdkUrl | 分配的AiriSDK正式服务器访问地址                                      |
| Facebook AppID | 分配的facebook AppID                                        |
| Twitter Key | 分配的Twitter Key                                           |
| 安卓包名 | 安卓注册用包名                                                  |
| IOS BUNDLEID | 苹果注册bundleid                                             |
| AiHelp 各参数 | 第三方客服需要的参数                                               |
| Google Play AppID| Google Play Games Services登陆的必须参数，AppId为Google控制台对应游戏的ID |
| Amazon API KEY| Amazon登陆所需参数                                             |
| OneStore API KEY| OneStore支付所需参数                                           |
| GoogleService-Info.plist、google-services.json| Firebase 配置文件                |


### Step2: 导入SDK
\* Unity编辑器打开游戏工程后, 双击SDK Unitypackage 导入到游戏工程;<br/>
\* 如果你的游戏工程中已经有自定义的AndroidManifest.xml ,在导入AiriSDK时请注意，避免该文件被覆盖重写;

##### YostarSDK目录结构
<img src="https://sdkresources.oss-cn-shanghai.aliyuncs.com/AiriSDK%E6%8E%A5%E5%85%A5%E6%96%87%E6%A1%A3%E5%9B%BE%E5%BA%8A/unity_dir.png" alt="" width="330" height="260" align="left"  />
<br/><br/><br/><br/><br/><br/><br/><br/><br/><br/>

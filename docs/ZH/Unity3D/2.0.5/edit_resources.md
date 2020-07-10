### 配置参数获取

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
| Google Api Client ID | Google账号登陆的必须参数，为 OAuth 2.0 客户端的网页客户端ID |
| Google Play AppID| Google Game Services登陆的必须参数，AppId为Google控制台对应游戏的ID |
| Amazon API KEY| Amazon登陆所需参数 |

以上参数是在SDK初始化时需要的参数。这些参数可以使得SDK能够正常使用账号系统。支付系统的正常工作还需要服务端程序进行配合，请参考服务端文档。

### 创建和设置config文件

首次导入SDK包，请创建config asset文件，菜单如下图

![config_accsets](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/config_assets.png)

创建成功后会在目录
..\Assets\AiriSDK\Resources\下生成文件ConfigSettings.asset，点击后在inspecrtor如下图

![airisdk_setting](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/unity_config.png)

#### Save config

从AiriSDK平台的负责方那里获取到对应的参数，并在ConfigSettings中完整填写，点击```Save Config``` 按钮，会在同目录下生成文件 ```SDKConfigSettings.json```。该数据会在游戏运行时由SDK读取。

如果游戏有`Amazon登陆`需求，需要在`Amazon ApiKey`中添加内容，并且点击`save Config`后，数据会在`Android/assets/api_key.txt`文件中更新。

注意：填写正确后必须执行，否则游戏运行时讲获取不到SDK配置数据

#### Modify manifest

ConfigSettings填写完整正确参数后，点击```Modify Manifest```，会将manifest下的参数修改成填写的参数内容。

注意：填写正确后必须执行，否则HELPSHIFT功能失效

#### modify google service params

从AiriSDK平台的负责方获取文件```google-services.json```，并替换目录\Assets\Plugins\Android\assets下相同文件执行此操作，会将替换目录文件\Assets\Plugins\Android\res\values\google_service_strings.xml中的各项参数，用于google firebase 使用

注意：填写正确后必须执行，否则ADJUST、HELPSHIFT功能将受到影响

### AndroidManifest.xml配置

针对海外版本，SDK在android平台下需要对manifest.xml文件做一下必要修改

#### 1、权限设置

```xml
<uses-permission android:name="android.permission.INTERNET"/>
```

#### 2、AU支付

```xml
<uses-permission android:name="com.kddi.market.permission.USE_ALML" />
```

#### 3、分享

```xml
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```
#### 4、Application设置

必须包含```android:networkSecurityConfig="@xml/airisdk_network_security_config"```的application配置，以适配Android 9.0的网络请求.

```xml
<application android:allowBackup="true"
  android:networkSecurityConfig="@xml/airisdk_network_security_config"
  android:icon="@drawable/app_icon"
	android:label="@string/app_name"
  android:supportsRtl="true" >
<!-- 这里配置firebase、helpshift 等的具体内容，下文详细介绍-->
<!-- airisdk、facebook、twitter、google、adjsut 的配置以及转移到各AAR文件中，		这里不需要再单独配置-->
</application>
```

#### 5、airisdk主activity配置

注意:该步骤主要是用于将android原生平台的信息与支付插件之间互相通信。

注意:必须配置在```Application```域中

注意:```com.unity3d.player.UnityPlayerActivity```可以根据CP需求更改，不强制，但是更改的Activity必须继承```com.unity3d.player.UnityPlayerActivity```或```com.unity3d.player.UnityPlayerNativeActivity```


```xml
<activity android:name="com.unity3d.player.UnityPlayerActivity"
	android:label="@string/app_name" >
<intent-filter>
	<action android:name="android.intent.action.MAIN" />
	<category android:name="android.intent.category.LAUNCHER" />
</intent-filter>
<meta-data android:name="unityplayer.UnityActivity" android:value="true" />
</activity>
```

#### 6、helpshift配置

注意:helpshift_apiKey、helpshift_demain、helpshift_appId 三个参数的value需从运营商获取，并在UNITY的ConfigSettings.asset文件设置后，执行ModifyManifest填充正确的数据

注意:必须配置在Application域中

```xml
<meta-data android:name="helpshift_apiKey" android:value="xxx" />
<meta-data android:name="helpshift_demain" android:value="xxx" />
<meta-data android:name="helpshift_appId" android:value="xxx" />
```

#### 7、Google登陆配置

注意:com.google.android.gms.games.APP_ID 参数的value需从运营商获取，并在UNITY的ConfigSettings.asset文件设置后，执行ModifyManifest填充正确的数据到google_service_strings.xml文件中

Google依赖参数对应：
```xml
    <string name="default_web_client_id">1xxxxxx.apps.googleusercontent.com</string>
    <string name="fcm_fallback_notification_channel_label">xxxxxx</string>
    <string name="firebase_database_url">xxxxxxxxxxx</string>
    <string name="gcm_defaultSenderId">xxxxxx</string>
    <string name="google_api_key">xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</string>
    <string name="google_app_id">xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</string>
    <string name="google_crash_reporting_api_key">xxxxxxxxxxxxxxxxxxxxxxxxxx</string>
    <string name="google_storage_bucket">xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</string>
    <string name="project_id">xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</string>
    <string name="server_client_id">xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</string>
    <string name="app_id">xxxxxxxxxx</string>
```

注意:必须配置在Application域中

```xml
<meta-data android:name="com.google.android.gms.games.APP_ID" android:value="@string/app_id" />
```

#### 8、Amazon支付设置

注意:必须配置在Application域中

```xml

        <receiver android:name="com.amazon.device.iap.ResponseReceiver" >
            <intent-filter>
                <action
                    android:name="com.amazon.inapp.purchasing.NOTIFY"
                    android:permission="com.amazon.inapp.purchasing.Permission.NOTIFY" />
            </intent-filter>
        </receiver>

```

### Xcode工程需要的配置

#### 需要在`Xcode`工程的`Capability`开启`Push Notifications`和`Sign In with Apple`

![Capability_setting](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/2.0.5_Capability_setting.png)

#### 检查Link->Runpath Search Paths下，是否有@executable_path/Frameworks， 没有的话新增

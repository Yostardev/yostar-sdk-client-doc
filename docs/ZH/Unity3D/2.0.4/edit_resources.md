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

以上参数是在SDK初始化时需要的参数。这些参数可以使得SDK能够正常使用账号系统。支付系统的正常工作还需要服务端程序进行配合，请参考服务端文档。

### 创建和设置config文件

首次导入SDK包，请创建config asset文件，菜单如下图

![config_accsets](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/config_assets.png)

创建成功后会在目录
..\Assets\AiriSDK\Resources\下生成文件ConfigSettings.asset，点击后在inspecrtor如下图

![config_setting](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/config_setting.png)

#### Save config

从AiriSDK平台的负责方那里获取到对应的参数，并在ConfigSettings中完整填写，点击```Save Config``` 按钮，会在同目录下生成文件 ```SDKConfigSettings.json```。该数据会在游戏运行时由SDK读取。

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
#### 3、Application设置

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

#### 4、airisdk主activity配置

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

#### 5、firebase配置

注意:必须配置在Application域中

```xml
<service android:name="com.airisdk.firebase.MyFirebaseInstanceIDService">
  <intent-filter>
  <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
  </intent-filter>
</service>

<service android:name="com.airisdk.firebase.MyFirebaseMessagingService">
  <intent-filter>
    <action android:name="com.google.firebase.MESSAGING_EVENT"/>
  </intent-filter>
</service>

<service android:exported="true" 			 			
  android:name="com.google.firebase.messaging.FirebaseMessagingService">
  <intent-filter android:priority="-500">
    <action android:name="com.google.firebase.MESSAGING_EVENT"/>
  </intent-filter>
</service>

<service android:name="com.google.firebase.components.ComponentDiscoveryService">
  <meta-data 	android:name="com.google.firebase.components:com.google.firebase.iid.Registrar" 	
              android:value="com.google.firebase.components.ComponentRegistrar"/>
</service>

<receiver android:exported="true" 	
  android:name="com.google.firebase.iid.FirebaseInstanceIdReceiver" 	
  android:permission="com.google.android.c2dm.permission.SEND">
    <intent-filter>
      <action android:name="com.google.android.c2dm.intent.RECEIVE"/>
      <category android:name="${applicationId}"/>
    </intent-filter>
</receiver>

<service android:exported="true" 	
  android:name="com.google.firebase.iid.FirebaseInstanceIdService">
  <intent-filter android:priority="-500">
    <action android:name="com.google.firebase.INSTANCE_ID_EVENT"/>
  </intent-filter>
</service>

```

#### 6、helpshift配置

注意:helpshift_apiKey、helpshift_demain、helpshift_appId 三个参数的value需从运营商获取，并在UNITY的ConfigSettings.asset文件设置后，执行ModifyManifest填充正确的数据

注意:必须配置在Application域中

```xml
<meta-data android:name="helpshift_apiKey" android:value="xxx" />
<meta-data android:name="helpshift_demain" android:value="xxx" />
<meta-data android:name="helpshift_appId" android:value="xxx" />
```

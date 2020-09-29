### Edit Resources

Please contact Yostar to acquire the following parameters:

| Parameter | Description |
| ------ | ------ | 
| Test SdkUrl | AiriSDK test server address |
| Release SdkUrl | AiriSDK official server address |
| Facebook AppID | Facebook AppID |
| Twitter Key | Twitter Key |
| Android Package Name | Android Package Name |
| IOS BUNDLEID | iOS BundleID |
| HelpShift parameters | The parameters needed for HelpShift, a third-party customer support addon|

For AiriSDK to run its account system properly, the parameters mentioned above are required during the initialization of the SDK. The payment system, on the other hand, won't function normally without some collaboration from server-side, please use the "AiriSDK(JP)" as a reference.

### Creating and editing config file

If your AiriSDK was installed for the first time, please create a config file as the image shown below:

![config_accsets](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/config_assets.png)

Once the config file is created, a file named "ConfigSettings.asset" will appear under "..\Assets\AiriSDK\Resources\", click it, and you will find its inspector as the image shown below:

![config_setting](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/unity_config.png)

#### Save config

Contact Yostar to acquire the parameter settings and then fill them in ConfigSettings. ```SDKConfigSettings.json``` will be generated under the same folder after clicking ```Save Config```. This ```SDKConfigSettings.json``` will later be loaded while running the game.

Please note: you must ```Save Config``` after correctly editing ConfigSettings, otherwise the game will fail to obtain the SDK data.

#### Modify manifest

After the ConfigSettings is saved, click ```Modify Manifest```, it will change the parameter settings in manifest to the ones you have filled.

Please note: This step is a necessity for HELPSHIFT to function properly.

#### modify google service params

Acquire ```google-services.json``` from Yostar, and use it to replace the same file under \Assets\Plugins\Android\assets. It will also replace the settings of \Assets\Plugins\Android\res\values\google_service_strings.xml, allowing the usage of Google Firebase.

Please note: This step is a necessity for ADJUST and HELPSHIFT to function properly.

### AndroidManifest.xml Settings

For games to be released outside of China, please do the following adjustments to manifest.xml file for Android.

#### 1、Permission Settings

```xml
<uses-permission android:name="android.permission.INTERNET"/>
```

#### 2、AU Payment

```xml
<uses-permission android:name="com.kddi.market.permission.USE_ALML" />
```
#### 3、Application Settings

The network of Android 9.0 requires the application settings of ```android:networkSecurityConfig="@xml/airisdk_network_security_config"``` being included.

```xml
<application android:allowBackup="true"
  android:networkSecurityConfig="@xml/airisdk_network_security_config"		
  android:icon="@drawable/app_icon"
	android:label="@string/app_name"
  android:supportsRtl="true" >
<!-- Add the specific contents of Firebase, Helpshift here. More detailed description can be found in a later section-->
<!-- The settings of AiriSDK、Facebook、Twitter、Google、Adjust have already been transferred to AAR files, there's no need to edit them here again.-->
</application>
```

#### 4、Airisdk major activity settings

Please note: The main purpose of this step in to to sync the data between Android platform and payment addons.

Please note: It must be configured within the `Application'domain

Please note: :```com.unity3d.player.UnityPlayerActivity``` can be changed according to CP requirements, not mandatory, but the changed activity must inherit ```com.unity3d.player.UnityPlayerActivity``` or ```com.unity3d.player .UnityPlayerNativeActivity```

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

#### 5、Firebase Settings

Please note: It must be configured within the `Application'domain

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

#### 6、HelpShift Settings

Please note:Acquire the values of helpshift_apiKey、helpshift_demain、helpshift_appId from Yostar. After complete editing your ConfigSettings.asset, run "ModifyManifest", then fill in these three values.

Please note: It must be configured within the `Application'domain

```xml
<meta-data android:name="helpshift_apiKey" android:value="xxx" />
<meta-data android:name="helpshift_demain" android:value="xxx" />
<meta-data android:name="helpshift_appId" android:value="xxx" />
```

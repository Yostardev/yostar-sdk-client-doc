
### Obtain Configuration Parameters

Before integrating the SDK into the project, please contact the staff of the AiriSDK platform for the following parameters that need to be assigned to your application:

| Parameter name | Parameter description |
| ------ | ------ | 
| Test SdkUrl | Assigned AiriSDK test server access address |
| Release SdkUrl | Assigned AiriSDK official server access address |
| Facebook AppID | Assigned Facebook AppID |
| Twitter Key | Assigned Twitter Key |
| Android package name | Android package name for registration |
| IOS BUNDLEID | Apple bundleid for registration |
| HelpShift Parameters | Parameters required by third-party customer service |
| Google Api Client ID | Parameters required for Google account login: web client ID of OAuth 2.0 client. |
| Google Play AppID| Parameters required for Google Game Services login: AppID, the ID of the corresponding game on Google Play Console. |

Parameters above are required for SDK initialization. These parameters enable SDK to use the account system normally. Cooperation from the server end is required for the payment system to work normally. Please read for more details in documentations for server end.

### Create and Set Up config File

Please create config asset file when importing SDK for the first time. The menu is shown as follows:

![config_accsets](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/config_assets.png)

A file with the name ConfigSettings.asset will be created under the directory "..\Assets\AiriSDK\Resources\" after the successful creation of config asset file. After clicking the file, the following view will show in the inspector.

![airisdk_setting](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/2.0.5_airisdk_setting.png)

#### Save config

After obtaining the parameters from the staff of the AiriSDK platform and filling them in ConfigSettings, please click the ```Save Config``` button. The file ```SDKConfigSettings.json```, which will be read by the SDK while the game is running, will be created under the same directory.

Note: It must be executed after being filled in correctly, otherwise the SDK configuration data will not be obtained when the game is running.

#### Modify manifest

After ConfigSettings is filled in with the correct parameters, click ```Modify Manifest```, and the parameters under the "manifest" will be modified to the parameters filled.

Note: It must be executed after being filled in correctly, otherwise the HELPSHIFT functionality will fail.

#### modify google service params

Obtain the file google-services.json from the staff of the AiriSDK platform and replace the same file under the directory "\Assets\Plugins\Android\assets" with it. Doing this will replace all the parameters in the file under the directory "\Assets\Plugins\Android\res\values\google_service_strings.xml" which is used for Google Firebase.

Note: It must be executed after being filled in correctly, otherwise the ADJUST and HELPSHIFT functionality will be affected.

### AndroidManifest.xml Configuration

Modifications need to be made to the file on Android platform which is required for the SDK when targeting overseas versions.

#### 1、Permission Settings

```xml
<uses-permission android:name="android.permission.INTERNET"/>
```

#### 2、AU payment

```xml
<uses-permission android:name="com.kddi.market.permission.USE_ALML" />
```

#### 3、Share

```xml
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```
#### 4、Application Settings

Must include the application configuration, ```android:networkSecurityConfig="@xml/airisdk_network_security_config"``` in order to be compatible with the network requests of Android 9.0.

```xml
<application android:allowBackup="true"
  android:networkSecurityConfig="@xml/airisdk_network_security_config"
  android:icon="@drawable/app_icon"
	android:label="@string/app_name"
  android:supportsRtl="true" >

</application>
```

#### 5、AiriSDK Main activity Configuration

Note: This step is mainly used to establish the communication between the Android native platform and the payment plugin

Note: Must be configured in the ```Application``` domain.

Note: ```com.unity3d.player.UnityPlayerActivity``` can be changed based on CP's needs. The change is not mandatory, but the changed Activity must inherit ```com.unity3d.player.UnityPlayerActivity``` or ```com.unity3d.player.UnityPlayerNativeActivity```.


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

#### 6、Helpshift Configuration

Note: The values of ```helpshift_apiKey```, ```helpshift_demain``` and ```helpshift_appId``` need to be obtained from SP. After setting up Unity's ```ConfigSettings.asset``` file, ModifyManifest needs to be executed to fill in the correct parameters.

Note: Must be configured in the Application domain.

```xml
<meta-data android:name="helpshift_apiKey" android:value="xxx" />
<meta-data android:name="helpshift_demain" android:value="xxx" />
<meta-data android:name="helpshift_appId" android:value="xxx" />
```

#### 7、Google Login Configuration

Note: The value of com.google.android.gms.games.APP_ID needs to be obtained from the SP. After setting up Unity's ConfigSettings.asset file, ModifyManifest needs to be executed to fill in the correct parameters to the file google_service_strings.xml.

Parameters Required for Google Functionalities：
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

Note: Must be configured in the Application domain.

```xml
<meta-data android:name="com.google.android.gms.games.APP_ID" android:value="@string/app_id" />
```

### Configuration Required by Xcode Project

#### Need to enable ```Push Notifications``` and ```Sign In with Apple``` in ```Xcode``` project's ```Capability```.

![Capability_setting](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/2.0.5_Capability_setting.png)

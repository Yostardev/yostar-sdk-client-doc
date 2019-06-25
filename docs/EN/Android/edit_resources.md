

### 1.Assets

Settings of AiriSDK are all controled by```assets/AiriSDKConf.properties``` It is advised for the developers to adjust the settings：

Please contact Yostar to acquire the setting values.

| Parameter | Description | Necessity |
| ------ | ------ | ------ |
| AIRISDK_URL | Assigned AiriSDK server address | 是 |
| AIRISDK_PAYSTOREID | Payment method(s) of your game, Google Play is chosen as the default | 是 |
| AIRISDK_SHOWDEBUGLOG | Show/Hide AiriSDK log, the default is false (Hide AiriSDK log) | 是 |
| AIRISDK_NEWDEVICE | Treat the current device as a brand new device, the default is false | 是 |

### 2.AndroidManifeset Settings

#### Customer Support System

Helpshift has been implemented within AiriSDK as a customer service tool, therefore it is required to edit Helpshift setting and add meta-data below to the <application> section in AndroidManifest.xml.

Please contact Yostar to acquire the setting values.

```xml
<meta-data android:name="helpshift_apiKey" android:value="xxxxxxx" />
<meta-data android:name="helpshift_demain" android:value="xxxxx" />
<meta-data android:name="helpshift_appId" android:value="xxxxxxxxxxx" />
```

### 3.AU Payment Permission

AU payment has been implemented within AiriSDK, if your game accepts AU payment, then please add the following permission to your AndroidManifeset.xml：

```xml
<uses-permission android:name="com.kddi.market.permission.USE_ALML" />
```

### 4.res Settings

A part of Firebase's functions have been implemented within AiriSDK,please edit Firebase setting values in ```res/values/google_service_strings.xml```.

Please contact Yostar to acquire the setting values.

```xml
<string name="default_web_client_id">***</string>
<string name="fcm_fallback_notification_channel_label">****</string>
<string name="firebase_database_url">*****</string>
<string name="gcm_defaultSenderId">*****</string>
<string name="google_api_key">******</string>
<string name="google_app_id">******</string>
<string name="google_crash_reporting_api_key">******</string>
<string name="google_storage_bucket">*****</string>
<string name="project_id">*****</string>
```

### 5.AiriSDK Settings

```xml
        <activity
            android:name="com.airisdk.sdkcall.AiriSDKContentActivity"
            android:launchMode="singleTask"
            android:taskAffinity="com.xjp"
            android:theme="@style/AiriSDKThemeTranslucent" />
```

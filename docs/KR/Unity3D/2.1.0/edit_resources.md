
### 세팅 파라미터 획득

SDK를 프로젝트에 연동하기전,  책임자에게 문의하여 애플리케이션에 할당해야하는 아래의 파라미터를 문의하십시오:

| 파라미터 명칭 | 파라미터 설명 |
| ------ | ------ | 
| Test SdkUrl | 할당 받은 AiriSDK 테스트 서버 방문 주소 |
| Release SdkUrl | 할당 받은 AiriSDK 라이브 서버 방문 주소 |
| Facebook AppID | 할당 받은 Facebook AppID |
| Twitter Key | 할당 받은 Twitter Key |
| Android PackageName | 등록 할 Android 패키지 이름 |
| IOS BUNDLEID | 등록 할 Apple 번들 ID |
| HelpShift | 제3자 고객 서비스에 필요한 파라미터 |
| Google Api Client ID | Google 계정 로그인에 필요한 파라미터, OAuth 2.0 클라이언트의 웹 클라이언트 ID입니다. |
| Google Play AppID| Google 게임 서비스 로그인에 필요한 파라미터,  AppID는 Google Play Console에 대응하는 게임 ID 입니다. |

SDK 초기화에는 위의 파라미터가 필요합니다. 이 파라미터는 SDK가 계정 시스템을 정상적으로 사용할 수 있게 합니다. 결제 시스템이 정상적으로 작동하려면 서버 쪽에서 협력하여 진행 해야 합니다.  자세한 내용은 서버 설명 파일을 참고하여 주십시오.

### 생성 및 config 파일 설정

처음 SDK 빌드를 import 할 땐 config asset 파일을 생성 하십시오. 메뉴는 다음과 같이 표시됩니다:

![config_accsets](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/config_assets.png)

생성을 완료하면  ".. \ Assets \ AiriSDK \ Resources \" 디렉토리에 ConfigSettings.asset, 파일이 생성됩니다.  파일을 클릭하면 inspector에서 다음과 같이 표시됩니다. 

![airisdk_setting](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/2.0.5_airisdk_setting.png)

#### Save config

AiriSDK 플랫폼 책임자로부터 대응되는 파라미터를 획득 후 ConfigSettings에서 입력하여 ```Save Config``` 하면 동일한 디렉토리에 ```SDKConfigSettings.json``` 파일이 생성 됩니다.  해당 데이터는 게임 진행시 SDK 에서 로딩 합니다.

주의: 실행 시 반드시 올바르게 입력하여 주십시오. 입력이 잘못된 경우 게임을 실행할 때 SDK 세팅 데이터를 로딩할 수 없습니다.

#### Modify manifest

ConfigSettings에 올바른 파라미터를 입력후  ```Modify Manifest```를 클릭하면 ```manifest```아래의 파라미터를 입력한 파라미터로 변경합니다.

주의: 실행 시 반드시 올바르게 입력하여 주십시오.  입력이 잘못된 경우 HELP SHIFT  기능은 사용할수 없습니다.

#### modify google service params

AiriSDK 플랫폼 책임자로부터 ```google-services.json``` 파일을 획득 후 ```\ Assets \ Plugins \ Android \ assets```디렉토리에 있는 동일한 파일을 변경하고 실행합니다. 이렇게 하면 Google Firebase에 사용되는 ```\ Assets \ Plugins \ Android \ res \ values \ google_service_strings.xml```디렉토리 아래 파일의 모든 파라미터가 대체됩니다.

주의: 실행 시 반드시 올바르게 입력하여 주십시오.  입력이 잘못된 경우 ADJUST 및 HELPSHIFT 기능이 영향을 받을 수 있습니다.

### AndroidManifest.xml 세팅

해외 버전에 사용 시 Android 플랫폼에서의 SDK 는 manifest.xml 파일 수정이 필요합니다. 

#### 1、권한 설정

```xml
<uses-permission android:name="android.permission.INTERNET"/>
```

#### 2、AU 결제

```xml
<uses-permission android:name="com.kddi.market.permission.USE_ALML" />
```

#### 3、공유

```xml
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```
#### 4、애플리케이션 설정

Android 9.0의 네트워크 요청과 호환 되려면 애플리케이션 구성 ```android : networkSecurityConfig = "@ xml/airisdk_network_security_config"```를 포함해야합니다.

```xml
<application android:allowBackup="true"
  android:networkSecurityConfig="@xml/airisdk_network_security_config"
  android:icon="@drawable/app_icon"
	android:label="@string/app_name"
  android:supportsRtl="true" >

</application>
```

#### 5、AiriSDK 주요 Activity 설

주의: 이 단계는 주로 Android native 플랫폼의 정보와 결제 플러그인 간의 통신에 사용됩니다.

주의:  애플리케이션의 응용 프로그램 도메인에서 구성해야 합니다.

주의: ```com.unity3d.player.UnityPlayerActivity```는 CP의 요구에 따라 변경 될 수 있습니다. 변경은 필수 사항은 아니지만 변경된 활동은 ```com.unity3d.player.UnityPlayerActivity``` 또는 ```com.unity3d.player.UnityPlayerNativeActivity```를 계승해야 합니다.


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

#### 6、Helpshift 설정

주의: helpshift_apiKey, helpshift_demain 및 helpshift_appId의 값은 SP에서 가져와야합니다. Unity의 ConfigSettings.asset 파일을 설정 한 후 올바른 파라미터를 채우려면 ModifyManifest를 실행해야합니다.

주의: 반드시 애플리케이션 도메인에 세팅해야 합니다.

```xml
<meta-data android:name="helpshift_apiKey" android:value="xxx" />
<meta-data android:name="helpshift_demain" android:value="xxx" />
<meta-data android:name="helpshift_appId" android:value="xxx" />
```

#### 7、Google 로그인 설정

주의: ```com.google.android.gms.games.APP_ID```의 파라미터 value는 운영사에서 획득해야 하며 Unity의 ConfigSettings.asset 파일을 세팅 후 ModifyManifest 를 실행하여 정확한 데이터를  ```google_service_strings.xml``` 파일에 입력해야 합니다. 

Google 기능에 필요한 파라미터:
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

주의: 애플리케이션 도메인에 세팅해야합니다.

```xml
<meta-data android:name="com.google.android.gms.games.APP_ID" android:value="@string/app_id" />
```

### Xcode 프로젝트에 필요한 설정

#### Xcode 프로젝트의 `Capability` 중의 `Push Notifications` 와 `Sign In with Apple` 를 오픈.

![Capability_setting](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/2.0.5_Capability_setting.png)

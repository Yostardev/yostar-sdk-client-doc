

### 리소스 파일 다운로드

[AiriSDK.unitypackage](https://sdkresources.oss-cn-shanghai.aliyuncs.com/YostarSDK/2.1.0/AiriSDK_2.1.39.unitypackage)

### 리소스 파일을 프로젝트에 import

Unity 에디터로 게임 프로젝트를 연 후 다운로드 한 리소스 파일을 더블 클릭하여 필요한 모든 파일을 import할 수 있습니다. 파일을 import 할때 AndroidManifest.xml의 import과 덮어쓰기에 주의하십시오.  이미 사용 중인 Manifest 파일이있는 경우 "프로젝트 파라미터 세팅" 을 참고하여 주시기 바랍니다.

#### 플러그인 폴더의 내용을 확인 및 업데이트

![logo](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/plugin210.png)

이상은 unitypackage 의 모든 내용입니다.  파일을 업데이트 할 때 AndroidManifest.xml을 제외한 모든 파일을 삭제 후 다시 import할 수 있습니다.

### BundleID (패키지 이름) 규범

AiriSDK 플랫폼 책임자를 통하여 Google Play, iTunes Store 및 기타 채널 (예 : AU)에서 사용되는 게임 패키지 네임을 알 수 있습니다.  Unity PlayerSettings의 Android 및 iOS 설정에서 대응되는 해당 패키지 네임을 설정할 수 있습니다.

![BundleId](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/bundleid_unity.png)



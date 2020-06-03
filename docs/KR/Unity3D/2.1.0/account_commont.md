
### 1、게스트 로그인

디바이스 번호로 로그인하며, 보안에 취약합니다.

+ 호출 API :		
```csharp
public void LoginWithDevice()
```
+ API 호출의 사례 :
```csharp
using Airisdk;
AiriSDK.Instance.LoginWithDevice();
```
+ 콜백 이벤트 :	
```csharp
AirisdkEvent.Instance.LoginEvent (문서의 뒷부분에서 자세히 설명)
```

### 2、간편 로그인

최근에 게임에 로그인 한 계정으로 빠르게 로그인하십시오. 로그인 한 계정이 없으면 디폴트로 게스트 계정으로 로그인 됩니다. 
주의: 휴대폰 시스템 재설치 또는 로컬 계정 캐시를 지웠을 경우, 최근 로그인 정보는 지워집니다. 

+ 호출 API :		
```csharp
public void QuickLogin()
```
+ API 호출의 사례 : 
```csharp
using Airisdk;
AiriSDK.Instance.QuickLogin();
```
+ 콜백 이벤트 :
```csharp
AirisdkEvent.Instance.LoginEvent
```

### 3、Facebook 로그인

Facebook 계정으로 게임에 로그인. Facebook 계정으로 처음 로그인하면 SDK ID가 자동으로 생성됩니다.

+ 호출 API :		
```csharp
public void LoginWithFB()
```
+ API 호출의 사례 :
```csharp
using Airisdk;
AiriSDK.Instance.LoginWithFB();
```
+ 콜백 이벤트 :
```csharp
AirisdkEvent.Instance.LoginEvent
```

### 4、Google mail 로그인

Google 계정으로 게임에 로그인. SDK ID는 Google 계정으로 처음 로그인 한 경우 자동으로 생성됩니다.

+ 호출 API :		
```csharp
public void LoginWithGoogle()
```
+ API 호출의 사례 :
```csharp
using Airisdk;
AiriSDK.Instance.LoginWithGoogle();
```
+ 콜백 이벤트 :
```csharp
AirisdkEvent.Instance.LoginEvent
```

### 5、Google Play 게임 서비스 로그인

Google 계정으로 게임에 로그인. SDK ID는 Google Play 게임 서비스에 처음 로그인 한 경우 자동으로 생성됩니다.

+ 호출 API :		
```csharp
public void LoginWithGooglePlay()
```
+ API 호출의 사례 :
```csharp
using Airisdk;
AiriSDK.Instance.LoginWithGooglePlay();
```
+ 콜백 이벤트 :
```csharp
AirisdkEvent.Instance.LoginEvent
```

### 6、애플 로그인

Apple 계정으로 게임에 로그인. SDK ID는 Apple 계정으로 처음 로그인 한 경우 자동으로 생성됩니다.

+ 호출 API :		
```csharp
public void LoginWithApple()
```
+ API 호출의 사례 :
```csharp
using Airisdk;
AiriSDK.Instance.LoginWithApple();
```
+ 콜백 이벤트 :
```csharp
AirisdkEvent.Instance.LoginEvent
```

### 7、트위터 로그인

트위터 계정으로 게임에 로그인하십시오. Twitter 계정으로 처음 로그인하면 SDK ID가 자동으로 생성됩니다.

+ 호출 API :		
```csharp
public void LoginWithTW()
```
+ API 호출의 사례 : 
```csharp
using Airisdk;
AiriSDK.Instance.LoginWithTW();
```
+ 콜백 이벤트 :	
```csharp
AirisdkEvent.Instance.LoginEvent 
```

### 8、인계코드 로그인

인계코드를 사용하여 게임에 로그인. 인계코드 정보를 얻으려면 독립 API를 호출하여 획득 해야 합니다 (아래 설명 참조). 함수의 결과 값인 ResultCode (문서의 뒷부분에서 더 설명)는 파라미터 합법성을 검증하는 데만 사용됩니다. 성공 여부는 LoginEvent의 리턴데이터로 판단해야합니다.

+ 호출 API : 		
```csharp
ResultCode void LoginWithMigrationCode(string strTranscode, string strUid)
```
+ 호출 사례： 
```csharp
using Airisdk;
ResultCode rc = AiriSDK.Instance.LoginWithMigrationCode(strcode, struid);
If(rc == ResultCode.OK){ 
    //todo suc 
  } else { 
  //todo failed 
}
```
+ 콜백 이벤트 :	
```csharp
AirisdkEvent.Instance.LoginEvent
```

+ 인터페이스 파라미터 설명

| 파라미터 명칭 | 파라미터 유형 | 파라미터 설명 |
| ------ | ------ | ------ |
| strTranscode | string | 인계코드 (필수) |
| strUid | string | SDK UID (필수) |


### 9、인계코드 얻기

게임에 로그인 한 후이 API를 호출하여 인계코드와 UID를 얻을 수 있습니다. 제3자 게임 계정과 연동되지 않았을 경우, 디바이스 변경 등으로 이전의 인계코드를 통해 예전의 계정을 복구 할 수 있습니다. 

+ 호출 API : 
```csharp
public void MigrationCodeRequest()
```
+ API 호출의 사례 :
```csharp
using Airisdk;
AiriSDK.Instance.MigrationCodeRequest();
```
+ 콜백 이벤트 :			
```csharp
AirisdkEvent.Instance.MigrationCodeEvent
```
+ 콜백 이벤트 유형 :
```csharp
MigrationCodeRet
```
+ 콜백 이벤트 파라미터 설명

| 파라미터 명칭 | 파라미터 유형 | 파라미터 설명 |
| ------ | ------ | ------ |
| R_CODE | string | 오류 코드 : 0 성공 기타 오류 코드는 오류 코드 표를 참조하십시오. |
| R_MSG | string | 오류 메시지, 서포트용 |
| MIGRATIONCODE | string | 인계코드 |
| UID | string | SDK UID |

+ 콜백 이벤트의 사례

```csharp
using Airisdk.Event;
AirisdkEvent.Instance.MigrationCodeEvent += OnMigrationRespone;
private void OnMigrationRespone(MigrationCodeRet ret) {  
  //to do  
} 
```

### 10、로그인 통합 콜백 이벤트 

아래에 언급 할 Yostar 계정으로 로그인을 포함하여 위의 로그인 방법 중 어느 것을 사용하든 콜백 이벤트는 항상 AirisdkEvent.Instance.LoginEvent입니다.

+ 콜백 이벤트 :			
```csharp
AirisdkEvent.Instance.LoginEvent
```
+ 콜백 이벤트 유형 :
```csharp
LoginRet
```
+ 콜백 이벤트 파라미터 설명

| 파라미터 명칭 | 파라미터 유형 | 파라미터 설명 |
| ------ | ------ | ------ |
| R_CODE | string | 오류 코드 : 0 성공 기타 오류 코드는 오류 코드 표를 참조하십시오. |
| R_MSG | string | 오류 메시지, 서포트용 |
| ACCESS_TOKEN | string | SDK 로그인에 성공한 후  게임 서버 검증에 사용되는 ACCESS_TOKEN을 리턴 합니다. |
| UID | string | SDK 로그인에 성공한 후 게임 서버 인증을위한 UID를 리턴합니다.  |
| LOGIN_PLATFORM | LoginPlatform | 현재 게임 로그인 플랫폼. Enum Airisdk.LoginPlatform |
| BIRTH | string | 생일 정보 (일본에서만 유효하며 생일 정보 세팅하지 않은 계정은 결제 할 수 없음) |
| FACEBOOK_NAME | string | FB 로그인 또는 연동된 FB 명칭 |
| TWITTER_NAME | string | TW 로그인 또는 연동된 TW 명칭 |
| GOOGLE_EMAIL | string | Google 로그인 또는 연동된 Google 계정 |
| SDK_NAME | string | Yostar 계정 명칭 |
| ISCAN_BIND_GUEST | int | 게스트 계정을 연동 할 수 있는지 여부 (0은 연동 할 수 없고 0이 아닌 것은 연동 될 수 있음) 새로운 FB, TW 또는 Yostar 계정으로 로그인 할 때 유저가 디바이스에 마지막 로그인 계정이 게스트 계정으로 확인 되엇을때,  API NewAccountLink ()를 호출하여 연동 할 수 있습니다. |
| R_DELETETIME | string | 시간 단위 (단위 : 밀리 초) 실제로 계정을 삭제 한 시간입니다. 해당 시간 이전엔 복구 할 수 있습니다. |
| ISNEW | int | 새 계정인지 여부, 1 : 새 계정 임, 0 : 새 계정이 아님 |
| MIGRATIONCODE | string | 인계코드. 계정에 인계코드가 없거나 인계코드가 만료되면 파라미터가 비어 있게 됩니다.  |

+ 콜백 이벤트의 사례：
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.LoginEvent+= OnLoginRespone;
private void OnLoginRespone(LoginRet ret) {  
  //to do  
} 
```

### 11、Yostar 계정 로그인

Yostar 계정으로 게임에 로그인하십시오. 함수의 결과 값인 ResultCode (문서의 뒷부분에서 더 설명)는 파라미터를 확인하는 데만 사용됩니다. 성공 여부는 LoginEvent의 반환 값을 기준으로 판단해야합니다.

+ 호출 API : 	
```csharp
ResultCode void LoginWithSDK(string strEmail, string strVerificationCode)
```

+ 호출 사례： 
```csharp
using Airisdk;
ResultCode rc = AiriSDK.Instance.LoginWithSDK(strEmail, strVerificationCode);
If(rc == ResultCode.OK){ 
  //todo suc 
} else { 
  //todo failed 
}
```


+ 인터페이스 파라미터 설명

| 파라미터 명칭 | 파라미터 유형 | 파라미터 설명 |
| ------ | ------ | ------ |
| strEmail | string | 이메일로 전송 된 인증 코드 (필수) |
| strVerificationCode | string | Yostar 계정 인증 코드 받기(필수) |

### 12、Yostar 계정 인증 코드 받기

Yostar 계정 시스템의 인증 코드 요청은 API를 호출하고 인증 코드는 전달 된 이메일 주소로 전송됩니다. 모든 콜백 인터페이스는 확인 코드를 포함하지 않으며 ERRCODE 만 포함합니다.

+ 호출 API : 	
```csharp
ResultCode void VerificationCodeReq(string strEmail)
```
+ API 호출의 사례 :
```csharp
using Airisdk;
ResultCode rc = AiriSDK.Instance.VerificationCodeReq(strEmail);
If(rc == ResultCode.OK){ 
  //todo suc 
} else { 
  //todo failed 
}
```
+ 콜백 이벤트 :			
```csharp
AirisdkEvent.Instance.VerificationCodeEvent
```
+ 콜백 이벤트 유형 :
```csharp
VerificationCodeRet
```
+ 콜백 이벤트의 사례:
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.VerificationCodeEvent += OnVerificationCodeRespone;
private void OnVerificationCodeRespone(VerificationCodeRet ret){ 
  //to do 
} 
```
+ 인터페이스 파라미터 설명

| 파라미터 명칭 | 파라미터 유형 | 파라미터 설명 |
| ------ | ------ | ------ |
| strEmail | string | 이메일로 전송 된 인증 코드 (필수) |

+ 콜백 이벤트 파라미터 설명

| 파라미터 명칭 | 파라미터 유형 | 파라미터 설명 |
| ------ | ------ | ------ |
| R_CODE | string | 오류 코드 : 0 성공 기타 오류 코드는 오류 코드 표를 참조하십시오. |
| R_MSG | string | 오류 메시지, 서포트용 |


### 13、현재 SDK 로그인 정보 얻기

+ API 호출:

```csharp
public string SDKGetUID();
public string SDKGetAccessToken();
```

+ 호출 사례：

```csharp
string Sdk_Uid = AiriSDK.Instance.SDKGetUID();
string Sdk_AccessToken = AiriSDK.Instance.SDKGetAccessToken();
```

+ 인터페이스 설명：

```SDKGetUID``` 인터페이스는 현재 SDK UID를 얻는 데 사용됩니다. 

```SDKGetAccessToken``` 인터페이스는 현재 캐시의 SDK AccessToken을 얻는 데 사용됩되며 AccessToken은 게임 로그인의 유효성을 확인 하는데 사용됩니다. 

### 14、Amazon로그인

amazon 계정을 사용하여 처음 로그인 할 경우,SDK ID 는 자동 생성됩니다. 

+ API 호출:

```csharp
public void LoginWithAmazon()
```

+ 호출 사례：

```csharp
using Airisdk;
AiriSDK.Instance.LoginWithAmazon();
```
+ 콜백 이벤트：
```csharp
AirisdkEvent.Instance.LoginEvent 
```


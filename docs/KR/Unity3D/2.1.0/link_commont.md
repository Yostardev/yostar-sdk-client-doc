### 1、계정 연동 시스템

함수의 결과 값인 ResultCode (문서의 뒷부분에서 더 설명)는 파라미터 합법성을 검증하는데 사용되며, 실제 성공 여부는 LinkEvent 의 리턴 데이터로 판단해야 합니다. 뒤에 설명 드리겠습니다. 

주의: 중복 연동을 할 수 없습니다. FB 및 TW 계정이 이미 연동 된 경우 먼저 연동을 해제해야합니다.

주의: 로그인에 성공한 후 ​​호출 해야 합니다.

+ API 호출: 	

```csharp
ResultCode void LinkSocial(LoginPlatform platform)
```
+ 호출 사례： 
```csharp
using Airisdk;
ResultCode rc = AiriSDK.Instance.LinkSocial(LoginPlatform.FACEBOOK);
If(rc == ResultCode.OK){ 
  //todo suc 
 } else { 
  //todo failed 
 }
```
+ 콜백 이벤트 :	
```csharp
AirisdkEvent.Instance.LinkEvent(문서의 뒷부분에서 자세히 설명)
```
+ 인터페이스 파라미터 설명

| 파라미터 명칭 | 파라미터 유형 | 파라미터 설명 |
| ------ | ------ | ------ |
| platform | LoginPlatform | 플랫폼 유형 (필요) |

### 2、Yostar 계정 연동

함수 리턴값 ResultCode (문서의 뒷부분에서 더 설명) 호출은 파라미터 합법성을 검증하는데만 사용, 실제 성공 여부는 LinkEvent 의 리턴값을 기준을 판단. 뒤에서 자세하게 설명 하겠습니다.

주의: 로그인에 성공한 후에 만 ​​호출 할 수 있습니다.

주의: Yostar 계정은 다른 게임 계정에 연동 될 수 있습니다. 예를 들어, 게임 A에 등록 된 Yostar 계정은 게임 B의 기존 계정입니다.

+ API 호출: 	
```csharp
ResultCode void LinkSocial(LoginPlatform platform, string strEmail, string strVerificationCode)
```
+ 호출 사례:
```csharp
using Airisdk;
ResultCode rc = AiriSDK.Instance.LinkSocial(LoginPlatform.YOSTAR, strEmail, strVerificationCode);
If(rc == ResultCode.OK){ 
  //todo suc 
 } else { 
  //todo failed 
 }
```
+ 콜백 이벤트 :	
```csharp
AirisdkEvent.Instance.LinkEvent(문서의 뒷부분에서 자세히 설명)
```

+ 인터페이스 파라미터 설명

| 파라미터 명칭 | 파라미터 유형 | 파라미터 설명 |
| ------ | ------ | ------ |
| platform | LoginPlatform | 플랫폼 유형 (필요) |
| strEmail | string | 이메일 주소 (필수) |
| strVerificationCode | string | 이메일로 전송 된 인증 코드 (필수) |

### 3、특수 연동

API 설명 : 호출 함수엔 리턴값이 없으며 성공 여부는 LinkEvent의 리턴 값을 기준으로 판단해야합니다. 설명서의 뒷부분에서 자세히 설명합니다.

주의: 로그인에 성공한 후에 만 ​​호출 할 수 있습니다.

주의: 로그인 리턴 데이터 문자열 "ISCAN_BIND_GUEST! = 0" 일 경우에만 호출할수 있습니다.

주의: 자세한 설명은 "로그인 통합 콜백 이벤트"에 대한 설명을 참조하십시오.

+ API 호출: 	
```csharp
public void NewAccountLink()
```
+ 호출 사례:
```csharp
using Airisdk;
AiriSDK.Instance.NewAccountLink();
```
+ 콜백 이벤트 :	
```csharp
AirisdkEvent.Instance.LinkEvent(문서의 뒷부분에서 자세히 설명)
```

### 4、연동 통합 콜백 EVENT

+ 콜백 이벤트 :		
```csharp
AirisdkEvent.Instance.LinkEvent
```
+ 콜백 이벤트 유형 :	
```csharp
LinkRet
```
+ 콜백 이벤트의 사례:
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.LinkEvent+= OnLinkRespone;
private void OnLinkRespone(LinkRet ret) {  
  //to do  
} 
```
+ 콜백 이벤트 파라미터 설명:

| 파라미터 명칭 | 파라미터 유형 | 파라미터 설명 |
| ------ | ------ | ------ |
| R_CODE | string | 오류 코드 : 0 성공 , 기타 오류 코드는 오류 코드 표를 참조하십시오. |
| R_MSG | string | 오류 메시지, 서포트 용 |
| ACCESS_TOKEN | string | 연동 성공 후 ACCESS_TOKEN을 리턴 |
| LOGIN_PLATFORM | LoginPlatform | 현재 게임 연동 플랫폼, Enum Airisdk.LoginPlatform |
| SOCAIL_NAME | string | 현재 게임 연동 플랫폼의 유저 명칭 |

### 5、계정 연동해제 시스템

API 설명 : 함수의 리턴 값인 ResultCode (문서의 뒷부분에서 자세히 설명)는 파라미터 합법성을 확인하는 데만 사용됩니다. 성공 여부는 UnLinkEvent의 리턴 값을 기준으로 판단해야합니다.

주의: 중복 연동을 할 수 없습니다. FB 및 TW 계정이 이미 연동 된 경우 먼저 연동을 해제해야합니다.

주의: 로그인에 성공한 후에 만 ​​호출 할 수 있습니다.


+ API 호출: 	
```csharp
ResultCode void UnlinkSocial(LoginPlatform platform)
```
+ 호출 사례:
```csharp
using Airisdk;
AiriSDK.Instance.UnlinkSocial(LoginPlatform.FACEBOOK);
```
+ 인터페이스 파라미터 설명

| 파라미터 명칭 | 파라미터 유형 | 파라미터 설명 |
| ------ | ------ | ------ |
| platform | LoginPlatform | 플랫폼 유형 (필요) |

### 6、Yostar 계정 연동 해제

+ API 호출: 	
```csharp
ResultCode void UnlinkSocial(LoginPlatform platform, string strEmail, string strVerificationCode)
```
+ 호출 사례:
```csharp
using Airisdk;
ResultCode rc = AiriSDK.Instance.UnlinkSocial(LoginPlatform.YOSTAR, strEmail, strVerificationCode);
If(rc == ResultCode.OK){ 
  //todo suc 
 } else { 
  //todo failed 
 }
```
+ 콜백 이벤트 :	
```csharp
AirisdkEvent.Instance.UnLinkEvent(문서의 뒷부분에서 자세히 설명)
```

+ 인터페이스 파라미터 설명

| 파라미터 명칭 | 파라미터 유형 | 파라미터 설명 |
| ------ | ------ | ------ |
| platform | LoginPlatform | 플랫폼 유형 (필요) |
| strEmail | string | 이메일 주소 (필수) |
| strVerificationCode | string | 이메일로 전송 된 인증 코드 (필수) |

### 7、연동 해제 콜백 이벤트

+ 콜백 이벤트 :			
```csharp
AirisdkEvent.Instance.UnLinkEvent
```
+ 콜백 이벤트 유형 :	
```csharp
UnLinkRet
```
+ 콜백 이벤트의 사례：
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.UnLinkEvent+= OnUnLinkRespone;
private void OnUnLinkRespone(UnLinkRet ret) {  
	//to do  
} 
```
+ 콜백 이벤트 파라미터 설명:

| 파라미터 명칭 | 파라미터 유형 | 파라미터 설명 |
| ------ | ------ | ------ |
| R_CODE | string | 오류 코드 : 0 성공 , 기타 오류 코드는 오류 코드 표를 참조하십시오. |
| R_MSG | string | 오류 메시지, 서포트 용 |
| LOGIN_PLATFORM | LoginPlatform | 현재 게임 연동 플랫폼, Enum Airisdk.LoginPlatform |
| SOCAIL_NAME | string | Current 게임의 연동 플랫폼의 유저 명칭 |

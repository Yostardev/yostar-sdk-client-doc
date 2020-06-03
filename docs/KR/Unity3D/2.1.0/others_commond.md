### 1、PC 단 디버깅

대부분 기능이 모두 휴대폰의 네이티브 API와 관련되기에 PC 단 디버깅은 아래의 인터페이스만 오픈 되어있습니다. 
+ SDK 초기화 :
```csharp
public void Init()
```
+ 빠른 로그인：
```csharp
public void QuickLogin()
```
+ 디바이스 번호 로그인 :
```csharp
public void LoginWithDevice()
```
+ 인계 코드 로그인 :	
```csharp
ResultCode void LoginWithTranscode(string strTranscode, string strUid)
```

### 2、로컬 계정 캐시 지우기

이 인터페이스를 호출하여 디바이스의 계정 정보를 지우십시오.

주의: 계정 정보를 지우면 지난 로그인시 사용했던 계정으로 빠른 로그인 할 수 없습니다. FB / TW / Yostar 모두 새로운 계정으로 다시 로그인해야합니다.

주의: 인터페이스 호출은 신중하게 진행 해야하며, 진행시 유저와 여러번 확인 해야 합니다. 

주의: 플레이어에 인계 코드, FB, TW 또는 Yostar 계정이 없는 경우 계정 데이터를 지우면 계정을 복구하기가 어렵습니다.

+ API 호출: 	
```csharp
public void ClearAccountInfo()
```
+ 호출 사례: 
```csharp
using Airisdk;
AiriSDK.Instance.ClearAccountInfo();
```
+ 콜백 이벤트:	
```csharp
AirisdkEvent.Instance.ClearAccountEvent
```
+ 콜백 이벤트 유형::	
```csharp
ClearAccountInfoRet
```
+ 콜백 이벤트의 사례:
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.ClearAccountEvent+= OnClearAccountRespone;
private void OnClearAccountRespone(ClearAccountInfoRet ret) {  
	//to do  
} 
```
### 3、유저 행위 데이터 보고서 (데이터 통계)

이러한 인터페이스를 호출하면 일부 유저 이벤트를 SDK 서버에 알릴 수 있습니다. 구체적으로 어떤 유저 이벤트가 필요할지는 운영사와 개발사가 협의하여 진행합니다.

+ API 호출: 	
```csharp
public void UserEventUpload(string strEventName, Dictionary<string, string> strCallbackParameter = null)
```
+ 호출 사례： 
```csharp
using Airisdk;
Dictionary<string, string> dicParam = new Dictionary<string, string>();
dicParam.Add("test1", "test1");
dicParam.Add("test2", "test2");
AiriSDK.Instance.UserEventUpload(m_inputEventName.text, dicParam);
```
+ 콜백 이벤트：
```
None
```
+ 인터페이스 파라미터 설명

| 파라미터 명칭 | 파라미터 유형 | 파라미터 설명 |
| ------ | ------ | ------ |
| strEventName | string | 이벤트 명칭 (운영사에서 제공) (필수) |
| strCallbackParameter | Dictionary<string, string> | 콜백 파라미터 (운영사에서 제공) (필수 아님) |

### 4、게임 자체정의 사진 공유

이 인터페이스를 호출하면 자체정의한 Texture2D IOS 또는 안드로이드에 네이티브 공유 할 수 있습니다. 이 인터페이스는 파라미터 texture에서 텍스처 데이터를 얻습니다.

+ API 호출: 	
```csharp
public void SystemShare(string strShareText, Texture2D texShare = null)
```
+ 호출 사례： 
```csharp
using Airisdk;
Texture2D screenShot = GetScreeShot()；
AiriSDK.Instance.SystemShare("test share", screenShot)；
```
+ 콜백 이벤트：	
```csharp
AirisdkEvent.Instance.SystemShareEvent
```
+ 콜백 이벤트의 사례：
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.SystemShareEvent += OnSystemShareRespone;
private void OnSystemShareRespone(SystemShareRet ret) {  
	//to do  
} 
```
+ 인터페이스 파라미터 설명

| 파라미터 명칭 | 파라미터 유형 | 파라미터 설명 |
| ------ | ------ | ------ |
| strShareText | string | 텍스트 공유 |
| texShare  | Texture2D | 사진 공유 |

+ 콜백 이벤트 파라미터 설명

| 파라미터 명칭 | 파라미터 유형 | 파라미터 설명 |
| ------ | ------ | ------ |
| R_CODE | string | 오류 코드 : 0 성공 , 기타 오류 코드는 오류 코드 표를 참조하십시오. |
| R_MSG | string | 오류 메시지, 서포트 용 |

### 5、앱 스토어 평점

이 인터페이스를 호출하면 APPSTORE로 이동하지 않고 애플리케이션을 자동으로 평가할 수 있습니다.

주의: 단일 유저에게 1 년에 세 번밖에 사용할수 없기에 적합한 시기에 유저에게 알림을 줘야합니다.

+ API 호출: 	
```csharp
public void RequestStoreReview()
```
+ 호출 사례： 
```csharp
using Airisdk;
AiriSDK.Instance.RequestStoreReview();
```

### 6、제3자 고객 서비스 HelpShift

이 인터페이스를 호출하면 HelpShift 제3자 고객 서비스 플러그인이 자동으로 열립니다. 유저는 Help Shift 를 통하여 FAQ를 보거나 개발자 팀에 직접 문의 할 수 있습니다.

+ API 호출: 	
```csharp
public void OpenHelpShift()
```
+ 호출 사례： 
```csharp
using Airisdk;
AiriSDK.Instance.OpenHelpShift();
```

### 7、제3자 고객 서비스 HelpShift (캐릭터 파라미터)

이 인터페이스를 호출하면 HelpShift 제3자 고객 서비스 플러그인이 자동으로 열립니다. 유저는 Help Shift 를 통하여 FAQ를 보거나 개발자 팀에 직접 문의 할 수 있습니다.

+ API 호출:


```csharp
public void OpenHelpShift(string roleUid, string roleName, string roleLevel, string roleServer, string rolePurchase, string createTime)
```
+ API 파라미터 설명

| 파라미터 명칭 | 파라미터 유형 | 파라미터 설명 |
| ------ | ------ | ------ |
| roleUid | string | 캐릭터 ID |
| roleName  | string | 캐릭터 명칭 |
| roleLevel  | string | 캐릭터 레벨 |
| roleServer  | string | 캐릭터가 존재하는 서버 (포맷 : 서버 ID- 서버 명칭) |
| rolePurchase  | string | 이 서버에서 결제한 금액 (USD) |
| createTime  | string | 캐릭터 생성 시간 |



+ 호출 사례:


```csharp
using Airisdk;
AiriSDK.Instance.OpenHelpShift("11552233", "xxxxxx", 1+"", "2 - rrrrrrr",18 + "", "2019-08-06 10:57:11");
```

### 8、계정 삭제

이 인터페이스를 호출하면 이 해당 계정과 제3자 측의 계정을 자동으로 연동 시키고 로컬 캐시 삭제, 서버 데이터 기록이 삭제 됩니다.  개발사측에선 신중히 사용하시기 바랍니다. 

+ API 호출: 	
```csharp
public void DeleteAccount()
```
+ 호출 사례： 
```csharp
using Airisdk;
AiriSDK.Instance.DeleteAccount();
```
+ 콜백 이벤트

```csharp
AirisdkEvent.Instance.DeleteAccountEvent
```
+ 콜백 이벤트 유형:
```
DeleteAccountRet
```
+ 콜백 이벤트 파라미터 설명

| 파라미터 명칭 | 파라미터 유형 | 파라미터 설명 |
| ------ | ------ | ------ |
| R_CODE | string | 오류 코드 : 0 성공 , 기타 오류 코드는 오류 코드 표를 참조하십시오. |
| R_MSG | string | 오류 메시지, 서포트 용 |


### 9、계정 복구

이 인터페이스를 호출하면 이 계정이 모든 타사 계정에 자동으로 연동되고, 로컬 캐시 및 서버 데이터 기록이 삭제됩니다. CP는 주의해서 호출하여 주십시오.

+ API 호출: 	
```csharp
public void RebornAccount()
```
+ 호출 사례： 
```csharp
using Airisdk;
AiriSDK.Instance.RebornAccount();
```
+ 콜백 이벤트

```csharp
AirisdkEvent.Instance.RebornAccountEvent
```
+ 콜백 이벤트 유형:
```
RebornAccountRet
```
+ 콜백 이벤트 파라미터 설명

| 파라미터 명칭 | 파라미터 유형 | 파라미터 설명 |
| ------ | ------ | ------ |
| R_CODE | string | 오류 코드 : 0 성공 , 기타 오류 코드는 오류 코드 표를 참조하십시오. |
| R_MSG | string | 오류 메시지, 서포트 용 |


### 10、퍼블릭 데이터 획득 인터페이스

| 属性 | 说明 | 
| ------ | ------ |
| ```AiriSDK.Instance.GetDeviceID()``` | 유저 디바이스를 획득하는 유일한 식별 번호입니다. |
| ```AiriSdkData.Instance.AiriSDK_VERSION``` | SDK 버전 번호 |

### 11、유저 약관 확인

이 인터페이스는 유저가 '유저 약관 동의'를 클릭 시 호출됩니다.

+ API 호출: 	
```csharp
public void ConifrmAgreement()
```
+ 호출 사례： 
```csharp
using Airisdk;
AiriSDK.Instance.ConifrmAgreement();
```

### 12、유저 약관 링크 획득

이 인터페이스는 CP가 유저 약관을 출력해야 할 때 사용됩니다.

+ API 호출: 
```csharp
public string GetAgreement()
```
+ 호출 사례:
```csharp
using Airisdk;
string greement_url = AiriSDK.Instance.GetAgreement();
```

+ 주의: 이 인터페이스는 완전한 네트워크 링크를 리턴합니다. 개발사는 링크에서 계약에 대한 관련 정보를 얻도록 요청할 수 있습니다. 

 
리턴 파라미터의 사례:
```
http://test.sdk.azurlane.jp:3011/user/agreement?version=v1.0.0
```
리턴 값 사례：
```json
{
    "version": "v1.0.0",
    "data": [
        "Part 1",
        "Part 2"
    ]
}
```

### 13、유저 약관 구체적인 내용 획득

+ API 호출：
```csharp
public void GetAgreementInfo()
```

+ 호출 사례：
```csharp
AiriSDK.Instance.GetAgreementInfo();
```
+ 콜백 이벤트

```csharp
AirisdkEvent.Instance.GetAgreementEvent
```

+ 콜백 이벤트 유형 :

```csharp
GetAgreementRet
```

+ 콜백 이벤트의 사례：

```csharp
using Airisdk.Event;
AirisdkEvent.Instance.GetAgreementEvent += OnGetAgreementResponse;
private void OnGetAgreementResponse(GetAgreementRet ret) {  
	//to do  
} 
```
+ 콜백 이벤트 파라미터 설명

| 파라미터 명칭 | 파라미터 유형 | 파라미터 설명 |
| ------ | ------ | ------ |
| R_CODE | string | 오류 코드 : 0 성공 , 기타 오류 코드는 오류 코드 표를 참조하십시오. |
| R_MSG | string | 오류 메시지, 서포트 용 |
| Agreements | string | 구체적인 약관 내용, JsonArray 문자열 형식. |

+ 리턴 값 Agreements 사례

```json
["Part 1 ","Part 2"]
```

### 14、소액 환불 계약

+ API 호출：
```csharp
public void GetUnderAgeAgrement()
```

+ 호출 사례：
```csharp
AiriSDK.Instance.GetUnderAgeAgrement();
```

+ 콜백 이벤트

```csharp
AirisdkEvent.Instance.GetUnderAgreementEvent
```

+ 콜백 이벤트의 사례：

```csharp
using Airisdk.Event;
AirisdkEvent.Instance.GetUnderAgreementEvent += OnGetUnderAgreementResponse;
private void OnGetUnderAgreementResponse(GetUnderAgreementRet ret)
{
//to do  
}
```

+ 콜백 이벤트 파라미터 설명

| 파라미터 명칭 | 파라미터 유형 | 파라미터 설명 |
| ------ | ------ | ------ |
| R_CODE | string | 오류 코드 : 0 성공 , 기타 오류 코드는 오류 코드 표를 참조하십시오. |
| R_MSG | string | 오류 메시지, 서포트 용 |
| SHOP_AGREEMENT | string | 구체적인 약관 내용, JsonArray 문자열 형식. |
| isSHOW | int | 프로토콜 표시 여부, 1 : 필수, 0 : 필수 |

### 15、Google S2S 인터페이스

+ API 호출：
```csharp
public void GoogleServerToServer(string devToken, string linkID, string eventName, string priceValue, string currencyCode)
```

+ 호출 사례：
```csharp
AiriSDK.Instance.GoogleServerToServer(
                "xxxxxxxxxxxxxxxxxxxxx",
                "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
                "xxxxxxxxxxxxxx S2S_purchase_click",
                "xxx",
                "USD"
            );
```


### 16、오류 코드 메시지 리턴 인터페이스

+ API 호출：
```csharp
public string GetSDKRecommendedErrorMsg(int code, LanguageType type)
```

+ 호출 사례：
```csharp
string strMsg = AiriSDK.Instance.GetSDKRecommendedErrorMsg(100404, LanguageType.MSG_EN);
```

+ 파라미터 설명：

| 파라미터 명칭 | 파라미터 유형 | 파라미터 설명 |
| ------ | ------ | ------ |
| code | int | 오류 코드 : 0 성공 , 기타 오류 코드는 오류 코드 표를 참조하십시오. |
| type | LanguageType | 언어 파라미터, 현재 중국어, 영어, 한국어 및 일본어 만 지원 |


### 17、클립 보드

+ API 호출：
```csharp
public ResultCode SDKToClipboard(string cValue);
```

+ 호출 사례：
```csharp
ResultCode code = AiriSDK.Instance.SDKToClipboard(cValue);
if (code == ResultCode.OK) {
   Debug.Log("SUCCESS");
}
```

+ 파라미터 설명：

| 파라미터 명칭 | 파라미터 유형 | 파라미터 설명 |
| ------ | ------ | ------ |
| cValue | string | 클립 보드에 복사해야하는 내용 |

### 18、iOS 시스템 Apple 로그인 지원 여부

+ API 호출：
```csharp
public bool IOSAppleSignInAvailable();
```

+ 호출 사례：
```csharp
bool isAvailable = AiriSDK.Instance.IOSAppleSignInAvailable();
```

### 19、미성년자 청약 철회 약관

+ API 호출：
```csharp
public void GetUnderAgeAgrement()
```

+ 호출 사례：
```csharp
AiriSDK.Instance.GetUnderAgeAgrement();
```

+ 콜백 이벤트

```csharp
AirisdkEvent.Instance.GetUnderAgreementEvent
```

+ 콜백 이벤트의 사례：

```csharp
using Airisdk.Event;
AirisdkEvent.Instance.GetUnderAgreementEvent += OnGetUnderAgreementResponse;
private void OnGetUnderAgreementResponse(GetUnderAgreementRet ret)
{
//to do  
}
```

+ 콜백 이벤트 파라미터 설명

| 파라미터 명칭 | 파라미터 유형 | 파라미터 설명 |
| ------ | ------ | ------ |
| R_CODE | string | 오류 코드 : 0 성공 , 기타 오류 코드는 오류 코드 표를 참조하십시오. |
| R_MSG | string | 오류 메시지, 서포트 용 |
| SHOP_AGREEMENT | string | 상세 약관, 포맷은 JsonArray 텍스트열 |
| isSHOW | int | 약관 출력 여부, 1: 필요, 0: 불필요 |


### 18、미성년자 약관 확인

+ API 호출：

```csharp
public void ConfirmUnderAger();
```

+ 호출 사례：

```csharp
AiriSDK.Instance.ConfirmUnderAger();
```



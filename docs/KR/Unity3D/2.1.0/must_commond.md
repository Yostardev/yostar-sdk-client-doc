
### 1、초기화

초기화는 한 번만 호출하면되며 다른 API를 호출하기 전에 수행해야합니다. 초기화 결과는 콜백 EVENT에 제공됩니다.

 + API 호출:		
 ```csharp
 public void Init()
 ```
 + 호출 사례:
```csharp
using Airisdk;
AiriSDK.Instance.Init();
```
 + 콜백 이벤트:		
```csharp
AirisdkEvent.Instance.InitEvent
```
 + 콜백 이벤트 유형:
```csharp
InitRet
```
+ 콜백 파라미터 설명

| 파라미터 명칭 | 파라미터 유형 | 파라미터 설명 |
| ------ | ------ | ------ |
| R_VIRTUAL | Int | 앱플레이어인지 여부 1 : 앱플레이어 0 : 실제 디바이스 |
| R_CODE | ResultCode | 오류 코드 : 0 성공 , 기타 오류 코드는 오류 코드 표를 참조하십시오. |
| R_MSG | string | 오류 메시지, 서포트 용 |
| ISCACHE | Int | 로그인 캐시 존재 여부, 1 존재, 0 존재하지 않음 |
| LOGIN_PLATFORM | LoginPlatform | 캐시가 존재하는 로그인 플랫폼 |
| LOGIN_UID | string | 캐시 된 UID |
| LOGIN_NAME | string | 캐시 명칭 |
| IS_POPUP_AGREEMENT | Int | 공지창 팝업 여부, 1 : 필요, 0 : 필요하지 않음 |

### 2、백그라운드 스위치

unity프로그램 프론트엔드/백엔드 전환 시 호출. 
**OnResume은 초기화 성공 후 추가로 한 번 더 호출해야 합니다.**

+ 호출 API :		

```csharp
public void OnResume()
```
```csharp
public void OnPause()
```
+ API 호출의 사례:
```csharp
using Airisdk;
private void OnApplicationPause(bool isPause)
{
  if (isPause)
  {
    AiriSDK.Instance.OnPause();
  }
  else
  {
    AiriSDK.Instance.OnResume();
  }
}
```

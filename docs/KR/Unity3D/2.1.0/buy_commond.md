### 1、유저의 생일을 설정

해당 인터페이스를 호출하면 유저의 생일을 설정 하실수 있습니다. 일본유저는 연령에 따라 한 달에 결제 상한이 결정 됩니다. 

+ API 호출: 	
```csharp
public ResultCode SetBirth(string strBirth)
```
+ 호출 사례： 
```csharp
using Airisdk;
AiriSDK.Instance.SetBirth(“19901212”);
```
+ 콜백 이벤트：	
```csharp
AirisdkEvent.Instance.BirthSetEvent
```
+ 콜백 이벤트 유형：
```csharp
BirthSetRet
```
+ 콜백 이벤트의 사례：
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.BirthSetEvent+= OnBirthSetRespone;
private void OnBirthSetRespone(BirthSetRet ret) {  
	//to do  
} 
```
+ 인터페이스 파라미터 설명

| 파라미터 명칭 | 파라미터 유형 | 파라미터 설명 |
| ------ | ------ | ------ |
| strBirth | string | 생일 : "yyyymmdd" 포맷 (예 : "19901212"(필수) |

+ 콜백 Event 의 사례 :

| 파라미터 명칭 | 파라미터 유형 | 파라미터 설명 |
| ------ | ------ | ------ |
| R_CODE | string | 오류 코드 : 0 성공 기타 오류 코드는 오류 코드 표를 참조하십시오. |
| R_MSG | string | 오류 메시지, 서포트용 |
| BIRTH | string | 생일 : "yyyymmdd" 포맷 (예 : "19901212"(필수) |

### 2、상품 구매

이 인터페이스를 호출하면 상품 구매가 시작됩니다. 상품 정보는 AiriSDK 백그라운드에 설정됩니다. 자세한 내용은 서버단 연동 문서를 참조하십시오. 함수의 리턴 값인 ResultCode (문서의 뒷부분에서 더 설명)호출은 파라미터 합법성을 확인하는 데만 사용됩니다. 성공 여부는 BuyEvent의 리턴 데이터를 기준으로 판단해야합니다.

+ API 호출:
```csharp
ResultCode void Buy(string strProductId, BuyServerTag eServerTag, string strExtraData)
```

+ 호출 사례： 
```csharp
using Airisdk;
AiriSDK.Instance.Buy(“productid”, BuyServerTag.preAudit, “ExtraData”);
```

+ 콜백 이벤트:		
```csharp
AirisdkEvent.Instance.BuyEvent 
```
+ 콜백 이벤트 유형：	
```csharp
BuyRet
```

+ 콜백 이벤트의 사례：
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.BuyEvent += OnBuyRespone;
private void OnBuyRespone(BuyRet ret) {  
	//to do  
} 
```
+ 파라미터 설명

| 파라미터 명칭 | 파라미터 유형 | 파라미터 설명 |
| ------ | ------ | ------ |
| strProductId | string | 상품 ID는 운영사측과 협의하여 획득 하고, 해당 ID는 AiriSDK 백그라운드에 세팅 필요 (필수) |
| eServerTag  | BuyServerTag | 서버 Enum (심사 서버, 배포예정서버(내부테스트 서버 포함), 공식 서버) (필수) . 결제는 각 서버 태그에 대응하며 태그가 다름에 따라 최종 서버단 결제 알림 URL 도 다릅니다. |
| strExtraData  | string | 트랜스페어런트 전송 문자열.  이 문자열은 클라이언트 측의 콜백과 서버 측의 결제 콜백에서는 원본대로 반환됩니다. 매번 다른 파라미터를 전송하도록 하세요. 서버 측의 결제 콜백 알림에 대해서는 서버 연동 가이드를  참조하십시오. |

+ 콜백 이벤트 파라미터 설명

| 파라미터 명칭 | 파라미터 유형 | 파라미터 설명 |
| ------ | ------ | ------ |
| R_CODE | string | 오류 코드 : 0 성공 기타 오류 코드는 오류 코드 표를 참조하십시오. |
| R_MSG | string | 오류 메시지, 서포트용 |
| EXTRADATA | string | 트랜스페어런트 전송 파라미터,  구매 요청 시작할 때 트랜스페어런트 전송 문자열 |
| ORDERID | string | 오더 번호. 구매 요청이 올바르게 시작된 경우이 해당 문자열은 AiriSDK의 오더 번호입니다. |

### 3、스토어 약관 획득

이 인터페이스를 호출하여 지역에 따라 스토어 약관을 획득하십시오.

+ API 호출: 	
```csharp
public void GetShopAgreement(ShopAgreementType agreementType);
```
+ 호출 사례： 
```csharp
using Airisdk;
AiriSDK.Instance.GetShopAgreement(ShopAgreementType.SHOP_AGREEMENT_1);
```
+ 콜백 이벤트：	
```csharp
AirisdkEvent.Instance.GetShopAgreementEvent
```
+ 콜백 이벤트 유형：
```csharp
GetShopAgreementRet
```
+ 콜백 이벤트의 사례：
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.GetShopAgreementEvent += OnGetShopAgreementResponse;
private void OnGetShopAgreementResponse(GetShopAgreementRet ret)
{
   Debug.Log("OnGetShopAgreementResponse:" + ret.R_CODE + "," + ret.R_MSG + "," + ret.SHOP_AGREEMENT);
}
```
+ 파라미터 설명

| 파라미터 명칭 | 파라미터 유형 | 파라미터 설명 |
| ------ | ------ | ------ |
| agreementType | ShopAgreementType | 약관 파라미터, SHOP_AGREEMENT_1 : 자금 결산 법 (JP 서버) 또는 환불 약관 (KR 서버) SHOP_AGREEMENT_2 : 특정 상업 거래법 (JP 서버) 또는 환불 약관 (KR 서버) |

+ Event파라미터 설명

| 파라미터 명칭 | 파라미터 유형 | 파라미터 설명 |
| ------ | ------ | ------ |
| R_CODE | string | 오류 코드 : 0 성공 기타 오류 코드는 오류 코드 표를 참조하십시오. |
| R_MSG | string | 오류 메시지, 서포트용 |
| SHOP_AGREEMENT | string | 특히 SDK 구성과 관련된 스토어 약관의 텍스트 |

+ SHOP_AGREEMENT프로토콜 예
```
["sa1"]
```

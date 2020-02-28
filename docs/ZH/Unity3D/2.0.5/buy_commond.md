### 1、Set User's Birthday

Call this interface to set user's birthday. In Japan, the maximum amount of money a user could spend in the game per month is determined by the user's age.

+ Calling API: 	
```csharp
public ResultCode SetBirth(string strBirth)
```
+ Examples of API Call： 
```csharp
using Airisdk;
AiriSDK.Instance.SetBirth(“19901212”);
```
+ Callback Event：	
```csharp
AirisdkEvent.Instance.BirthSetEvent
```
+ Callback Event Type：
```csharp
BirthSetRet
```
+ Examples of Callback Event：
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.BirthSetEvent+= OnBirthSetRespone;
private void OnBirthSetRespone(BirthSetRet ret) {  
	//to do  
} 
```
+ Interface parameter description

| Parameter Name | Parameter Type | Parameter Description |
| ------ | ------ | ------ |
| strBirth | string | Birthday, in the format "yyyymmdd", e.g. "19901212"(required) |

+ Callback EventParameter Description

| Parameter Name | Parameter Type | Parameter Description |
| ------ | ------ | ------ |
| R_CODE | string | Error code: 0 success. See Error Code Table for other error codes. |
| R_MSG | string | Error message, auxiliary |
| BIRTH | string | Birthday, in the format "yyyymmdd", e.g. "19901212" |

### 2、Purchase

Calling this interface will initiate the purchase request of the product. The product information is configured in the AiriSDK backend. For details, please refer to Server Access Documentation. The return value of the function, ResultCode (further explained in later part of the documentation) is only used to verify the parameters. Whether it succeeds should be judged based on the return value of BuyEvent.

+ Calling API:
```csharp
ResultCode void Buy(string strProductId, BuyServerTag eServerTag, string strExtraData)
```

+ Examples of API Call： 
```csharp
using Airisdk;
AiriSDK.Instance.Buy(“productid”, BuyServerTag.preAudit, “ExtraData”);
```

+ Callback Event:		
```csharp
AirisdkEvent.Instance.BuyEvent 
```
+ Callback Event Type：	
```csharp
BuyRet
```

+ Examples of Callback Event：
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.BuyEvent += OnBuyRespone;
private void OnBuyRespone(BuyRet ret) {  
	//to do  
} 
```
+ Interface parameter description

| Parameter Name | Parameter Type | Parameter Description |
| ------ | ------ | ------ |
| strProductId | string | Product ID, obtained after consultation with the SP, the ID is configured in the AiriSDK backend(required) |
| eServerTag  | BuyServerTag(enum) | Server enumeration (review server, pre-release server, formal server) (required) The corresponding server tags of payment. The final payment notification URL of the server side will be different based on the different server tags. |
| strExtraData  | string | Pass-through field(required). This field will be returned as it is in the callback of the client side and the payment callback of the server side. Please ensure that the parameters passed in each time are different. Please refer to Server Access Documentation for the payment callback notification of the server side.(required) |

+ Callback EventParameter Description

| Parameter Name | Parameter Type | Parameter Description |
| ------ | ------ | ------ |
| R_CODE | string | Error code: 0 success. See Error Code Table for other error codes. |
| R_MSG | string | Error message, auxiliary |
| EXTRADATA | string | Pass-through parameters. Pass-through fields when initiating a purchase request. |
| ORDERID | string | Order number. If the purchase request has been initiated correctly, this field is the order number in AiriSDK. |

### 3、Store Agreement Acquisition

Call this interface to obtain the store agreement based on region.

+ Calling API: 	
```csharp
public void GetShopAgreement(ShopAgreementType agreementType);
```
Examples of API Call： 
```csharp
using Airisdk;
AiriSDK.Instance.GetShopAgreement(ShopAgreementType.SHOP_AGREEMENT_1);
```
+ Callback Event：	
```csharp
AirisdkEvent.Instance.GetShopAgreementEvent
```
+ Callback Event Type：
```csharp
GetShopAgreementRet
```
Examples of Callback Event：
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.GetShopAgreementEvent += OnGetShopAgreementResponse;
private void OnGetShopAgreementResponse(GetShopAgreementRet ret)
{
   Debug.Log("OnGetShopAgreementResponse:" + ret.R_CODE + "," + ret.R_MSG + "," + ret.SHOP_AGREEMENT);
}
```
+ Interface parameter description

| Parameter Name | Parameter Type | Parameter Description |
| ------ | ------ | ------ |
| agreementType | ShopAgreementType | Agreement parameters, SHOP_AGREEMENT_1: Fund Settlement Law (JP server) or Refund Agreement (KR server) SHOP_AGREEMENT_2: Specified Commercial Transaction Law (JP server) or Refund Agreement (KR server) |

+ Callback EventParameter Description

| Parameter Name | Parameter Type | Parameter Description |
| ------ | ------ | ------ |
| R_CODE | string | Error code: 0 success. See Error Code Table for other error codes. |
| R_MSG | string | Error message, auxiliary |
| SHOP_AGREEMENT | string | The text of the store agreement, specifically related to the SDK configuration |

+ Examples of SHOP_AGREEMENT
```
["sa1"]
```

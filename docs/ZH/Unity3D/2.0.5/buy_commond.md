### 1、设置用户生日

调用该接口，可以设置用户的生日。在日本，用户的年轻决定了它当月可以氪金的上限。

+ 调用API: 	
```csharp
public ResultCode SetBirth(string strBirth)
```
调用示例： 
```csharp
using Airisdk;
AiriSDK.Instance.SetBirth(“19901212”);
```
+ 回调Event：	
```csharp
AirisdkEvent.Instance.BirthSetEvent
```
+ 回调Event类型：
```csharp
BirthSetRet
```
回调Event 示例：
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.BirthSetEvent+= OnBirthSetRespone;
private void OnBirthSetRespone(BirthSetRet ret) {  
	//to do  
} 
```
+ 接口参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| strBirth | string | 生日，格式“yyyymmdd”，如“19901212”（必要） |

+ 回调Event参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| R_CODE | string | 错误码 : 0成功，其它见后面统一错误码表 |
| R_MSG | string | 错误信息，辅助用 |
| BIRTH | string | 生日，格式“yyyymmdd”，如“19901212”（必要） |

### 2、购买商品

调用该接口会开始执行商品的购买。商品信息是配置在AiriSDK后台的，具体请参考服务端接入文档。调用函数返回值ResultCode（后续文章专门介绍）仅用来验证参数合法性，实际成功与否需要根据BuyEvent的返回数据进行判断。

+ 调用API:
```csharp
ResultCode void Buy(string strProductId, BuyServerTag eServerTag, string strExtraData)
```

+ 调用示例： 
```csharp
using Airisdk;
AiriSDK.Instance.Buy(“productid”, BuyServerTag.preAudit, “ExtraData”);
```

+ 回调Event:		
```csharp
AirisdkEvent.Instance.BuyEvent 
```
+ 回调Event类型：	
```csharp
BuyRet
```

+ 回调Event示例：
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.BuyEvent += OnBuyRespone;
private void OnBuyRespone(BuyRet ret) {  
	//to do  
} 
```
+ 接口参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| strProductId | string | 商品ID，和运营方协商后获取，该ID是配置在AiriSDK后台（必要） |
| eServerTag  | BuyServerTag(枚举) | 服务器枚举（提审服、预发布服、正式服）（必要）支付对应的服务器tag。根据这个tag不同，最后服务端的支付通知URL也会不同 |
| strExtraData  | string | 透传字段，该字段会在客户端的回调，以及服务端的支付回调中原样返回，请保证每次传入的参数不一致。服务端的支付回调通知请参见服务端接入文档。（必要） |

+ 回调Event参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| R_CODE | string | 错误码 : 0成功，其它见后面统一错误码表 |
| R_MSG | string | 错误信息，辅助用 |
| EXTRADATA | string | 透传参数，发起购买请求时的透传字段 |
| ORDERID | string | 订单号，如果正确地发起了购买请求，该字段就是在AiriSDK的订单号 |

### 3、商店协议获取

调用该接口，可以根据地区获取商店协议。

+ 调用API: 	
```csharp
public void GetShopAgreement(ShopAgreementType agreementType);
```
调用示例： 
```csharp
using Airisdk;
AiriSDK.Instance.GetShopAgreement(ShopAgreementType.SHOP_AGREEMENT_1);
```
+ 回调Event：	
```csharp
AirisdkEvent.Instance.GetShopAgreementEvent
```
+ 回调Event类型：
```csharp
GetShopAgreementRet
```
回调Event 示例：
```csharp
using Airisdk.Event;
AirisdkEvent.Instance.GetShopAgreementEvent += OnGetShopAgreementResponse;
private void OnGetShopAgreementResponse(GetShopAgreementRet ret)
{
   Debug.Log("OnGetShopAgreementResponse:" + ret.R_CODE + "," + ret.R_MSG + "," + ret.SHOP_AGREEMENT);
}
```
+ 接口参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| agreementType | ShopAgreementType | 协议参数，SHOP_AGREEMENT_1：资金结算法(日服)或退款说明(韩服) SHOP_AGREEMENT_2:特定商业交易法(日服)或退款协议(韩服) |

+ 回调Event参数说明

| 参数名称 | 参数类型 | 参数说明 |
| ------ | ------ | ------ |
| R_CODE | string | 错误码 : 0成功，其它见后面统一错误码表 |
| R_MSG | string | 错误信息，辅助用 |
| SHOP_AGREEMENT | string | 商店协议得文本信息，具体联系SDK配置 |

+ SHOP_AGREEMENT协议示例
```
["sa1"]
```

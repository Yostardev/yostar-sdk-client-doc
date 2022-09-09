### 中文对照表

| 错误码 | 错误说明 | 备注 |
| ------ | ------ | ------ |
| -1 | 	未知错误 | SDK服务器增加了新的错误码返回，SDK客户端没有及时更新 |
| 0  | 	成功 |成功 |
| 100100  | 	设备号被封 | 用户一些违规操作，让客服在后台禁止用户登陆 |
| 100110  | 	验证失败 | 1：SDK服务器配置不一致。2：客服在后台刷新了玩家的Token值 |
| 100111  | 	创建账号失败 | 可能设备号被封禁等原因 |
| 100112  | 	创建账号成功，绑定账号失败 |  -  |
| 100113  | 	绑定账号成功，验证失败 | 1：创建登陆成功后，返回的UID和Token错误。2：在登陆时，传递的UID和Token丢失或者出错 |
| 100114  | 	创建登陆时,IP访问被限制 | 悠星运营限制了地区IP的登陆 |
| 100115  | 	创建登陆时,设备号被封禁 | 悠星运营限制了玩家使用的设备号的登陆 |
| 100116  | 	创建登陆时,该UID被封禁 | 悠星运营限制了玩家的登陆 |
| 100117  | 	参数缺失 | CP调用时，参数少传 |
| 100120  | 	登陆时，IP访问被限制 | 悠星运营限制了地区IP的登陆 |
| 100130  | 	登陆时，该UID已被封禁 | 悠星运营限制了玩家的登陆 |
| 100140  | 	Access Token验证失败 | 玩家在其他的设备上登陆了此账号，造成AccessToken过期 |
| 100150  | 	提供的UID和Transcode不匹配 | 1：UID和当前的继承码已经使用过一次，过期了.2：UID和继承码不匹配 |
| 100160  | 	用户已经设置过了生日 | 重复设置生日日期，主要发生在日本支付之前 |
| 100170  | 	生日格式不正确 | 悠星SDK设置的生日格式为：yyyyMMdd,其他的格式不予通过 |
| 100180  | 	提供的第三方账号并未绑定过游戏账号 | 当前的第三方账号从来没有绑定过游戏账号(已过期或者游戏有特殊需求) |
| 100190  | 	提供的第三方参数在对应的服务器中验证失败 | 1：SDK服务器中配置的参数与游戏不符合.2：SDK客户端传递值得时候传了错误的参数. |
| 100200  | 	提供的第三方账号已经绑定过其它的UID | 绑定时，此第三方账号已经绑定过其他的账号 |
| 100201  | 	当前Google Play Games账号已与其他游戏账号绑定，确定换绑至该游戏账号吗？ | 
| 100202  | 	该游戏账号已绑定至其他Google Play Games账号，确定换绑至当前登录的Google Play Games账号吗？ |
| 100203  | 	该游戏账号已绑定至其他Google Play Games账号，且当前的Google Play Games账号已与其他游戏账号绑定，确定要重新换绑吗？ |
| 100204  | 	游客账号不会与Google Play Games账号绑定，因此无法支持使用该游客账号在其他设备上游玩。若您想要绑定，请先将游客账号与悠星账号/其他第三方账号进行绑定。 |
| 100205  | 	解绑失败，该游戏账号 未绑定 Google Play Games 账号。 |
| 100206  | 	非游客账号已与Google Play Games账号自动绑定，您可以通过Google Play Games账号在其他设备上进行登录。 |
| 100210  | 	提供的第三方账号和该账户绑定过的不匹配 | 玩家使用了另外的第三方账号尝试解除绑定。 |
| 100211  | 	绑定平台类型错误 | SDK内置的平台类型与CP传入的平台类型不匹配 |
| 100212  | 	解绑平台类型错误 | SDK内置的平台类型与CP传入的平台类型不匹配 |
| 100213  | 	不可执行解绑 | 当前账号只绑定一个第三方账户的时候，不可以对账户进行解绑 |
| 100214  | 	当前游戏账号与Google Play Games存在绑定，解绑除Google Play Games外的其他绑定方式，Google Play Games账号也将自动解绑。 |
| 100220  | 	取消授权 | 用户取消了第三方账户的授权 |
| 100221  | 	FB授权失败 | - |
| 100222  | 	TW授权失败 | - |
| 100223  | 	Google授权失败 | 1：开发者的Google api控制台没有设置游戏.2:签名和包名与在Google后台设置的不匹配.3.网络问题.具体的原因会在返回的Message中体现 |
| 100224  | 	Google服务不可用 | 1：请求Google服务失败 |
| 100225  | 	用户取消了Google授权 | - |
| 100226  | 	登录过程当前正在进行中，当前登录过程无法继续。 | - |
| 100227  | 	使用当前帐户登录尝试未成功。 | 1：开发者的Google api控制台没有设置游戏.2:签名和包名与在Google后台设置的不匹配. |
| 100228  | 	账号被用户删除 | 1：在发行的游戏会出现此状态 |
| 100229  | 	不可重复删除 | 不可重复删除 |
| 100231  | 	账号已经完全删除，恢复账号失败 | 恢复账号的时间超过了保存的配置的天 |
| 100232  | 	账号没有删除记录，不可恢复 | 账号还没有被删除 |
| 100233  | 	账号已经删除，不可登陆 | 账号执行过删除的操作，可以根据返回的时间，进行判断还有多长时间可以恢复账号 |
| 100234  | 	账号没有权限登陆 | 账号可能需要预约或者获取登陆资格才可以登陆游戏 |
| 100230  | 	初始化失败 | 1：网络问题.2：参数传递错误.3：SDK服务器地址传错 |
| 100240  | 	Apple授权信息不符 | - |
| 100241  | 	用户取消了Apple授权请求 | - |
| 100242  | 	Apple授权请求失败 | - |
| 100243  | 	Apple授权请求响应无效 | - |
| 100244  | 	未能处理Apple授权请求 | - |
| 100245  | 	Apple授权请求失败未知原因 | - |
| 100246  | 	系统版本不支持Apple授权 | ios登陆暂时只支持iOS13及以上的系统中 |
| 100300  | 	邮箱格式不正确 | 邮箱的格式必须是标准的邮箱格式 |
| 100301  | 	邮箱不一致 | 在需要确认邮箱的情况下，两次邮箱输入的不一致，将会出现此错误 |
| 100302  | 	验证码请求频率太快 | 邮箱发送频率为：1分钟1条，60分钟30条，24小时12条，超过此频率返回此错误 |
| 100303  | 	验证失败 | 1：验证失败，30分钟超时.2：验证码不一致 |
| 100304  | 	失败次数过多 | 1：一个邮箱发送一次验证码，最多可以验证十次，十次之后需要重新获取验证码 |
| 100305  | 	账户被封禁 | Yostar Account被封禁，可以换个邮箱试试 |
| 100306  | 	验证码为空 | - |
| 100307  | 	OneStore商店账号未登录 | - |
| 100404  | 	网络请求错误 | - |
| 200100  | 	用户生日未设置 | 在日本发行的游戏，必须要先设置生日 |
| 200110  | 	用户当月充值已超过保护上限 | 1：用户的充值成功的金额已经超过了当前保护值.2：用户的充值没有成功，但是一小时之内发起的订单金额的总和超过了当前的保护值 |
| 200120  | 	商品不存在 | 1：SDK服务器中没有配置商品.2：支付渠道后台没有配置商品 |
| 200130  | 	付款渠道不存在 | 悠星SDK现在暂时只支持iOS的appleStore支付，和Android的Google支付，还有日本Android的AU支付 |
| 200140  | 	serverTag不存在 | - |
| 200150  | 	支付收据验证失败 | 1：SDK服务器中配置的支付参数与当前的游戏不匹配.2：SDK客户端传递参数的时候出现错误 |
| 200160  | 	非法购买请求 | 1：用户token错误.2：订单、商品不存在 |
| 200170  | 	游戏服务端购买请求失败 | 1：游戏逻辑服务器认为购买非法 |
| 200180  | 	需要长时间查询购买的结果 | 1：SDK服务器和游戏服务器交互失败.2：服务器交互时间过长，需要等待确认 |
| 200190  | 	订单编号不存在 | - |
| 200200  | 	查询订单状态超时 | 1：SDK服务器和游戏服务器交互失败。 |
| 200210  | 	支付渠道后台没有这个productid | - |
| 200220  | 	支付渠道返回支付失败 | - |
| 200230  | 	支付渠道返回支付取消 | - |
| 200240  | 	请求的类型不支持结算API版本 | Google Play版本不支持支付 |
| 200250  | 	提供给API的参数无效 | 提供给API的参数无效。此错误还可能表示应用程序未正确签名或未正确设置为Google Play中的应用内结算，或者其清单中没有必要的权限 |
| 200260  | 	API操作期间发生致命错误 | 网络错误等特殊情况 |
| 200270  | 	当前设备上的Play商店不支持请求的功能。 | - |
| 200280  | 	由于物品已经拥有，未消耗 | - |
| 200290  | 	由于物品已经拥有，并且消耗失败 | - |
| 200300  | 	请求的产品无法购买 | 1：商品ID与Google后台配置的不一致。2：运营在Google后台限制了此商品的购买 |
| 200310  | 	Google Play服务无法连接 | 1：Google Play没有登陆 2：Google Play没有安装 3：网络环境不好 |
| 200320  | 	在Google Play响应之前，请求已达到最大超时时间 | 1：网络环境不好 |
| 200330  | 	网络连接已关闭 | - |
| 200340  | 	用户取消了支付 | - |
| 200350  | 	查询商品ID失败 | 检查Google后台配置的商品ID是否与当前支付的商品ID一致 |
| 200360  | 	连接play services失败 | - |
| 200370  | 	重复创建订单 | - |
| 200380  | 	未成年人退款协议未同意 | - |
| 300100  | 	系统分享失败 | - |

### 英语对照表

| Error Code | Description |
| ------ | ------ |
| -1 | 	Unknown Error |
| 0  | 	Success |
| 100100  | 	Device ID is banned |
| 100110  | 	Verification failed |
| 100111  | 	Account creation failed |
| 100112  | 	Account creation success; Account binding failed |
| 100113  | 	Account binding success; Verification failed |
| 100114  | 	IP is restricted during login creation |
| 100115  | 	Device ID is banned during login creation |
| 100116  | 	UID is banned during login creation |
| 100117  | 	Missing parameters |
| 100120  | 	Login failed, IP is restricted |
| 100130  | 	Login failed, UID is banned |
| 100140  | 	Access Token verification failed |
| 100150  | 	UID does not match with Transcode |
| 100160  | 	User birthday has already been added |
| 100170  | 	Invalid birthday format |
| 100180  | 	The third party account is not bound with any game account |
| 100190  | 	Failed to verify the third party parameter |
| 100200  | 	The third party account is already bound with another UID |
| 100201  | 	The Google Play Games account has been linked to another game account. Confirm to unlink it from the old game account and re-link to the current one? |
| 100202  | 	The game account has been linked to another Google Play Games account. Confirm to unlink it from the old Google Play Games account and re-link to the current one? |
| 100203  | 	The current game account and Google Play Games account have each been linked to other accounts. Confirm to unlink the both from the old accounts and re-link them together? |
| 100204  | 	The guest account can't be linked to a Google Play Games account so you can't log on another device with the guest account. If you want to link the guest account to a Google Play Games account, please link it to a Yostar account/third-party account first. |
| 100205  | 	Unbind failed. Your game account hasn't been linked to a Google Play Games account. |
| 100206  | 	The non-guest account has been linked to a Google Play Games account automatically. You can log on another device with the Google Play Games account. |
| 100210  | 	The third party account does not match with the one bound to this account |
| 100211  | 	Platform binding error |
| 100212  | 	Platform unbinding error |
| 100213  | 	Unable to unbind the account |
| 100214  | 	The game account now is linked to a Google Play Games account. If you unlink it from other accounts (except the Google Play Games account), it will also unlink from the Google Play Games account automatically. |
| 100220  | 	Authorization canceled |
| 100221  | 	FB authorization failed |
| 100222  | 	TW authorization failed |
| 100223  | 	Google authorization failed |
| 100224  | 	Unable to use Google service |
| 100225  | 	Google authorization was canceled by user |
| 100226  | 	Unable to login during another login request |
| 100227  | 	Failed to login with the current account |
| 100228  | 	The account was already deleted by user |
| 100229  | 	Account deletion cannot be performed repeatedly |
| 100231  | 	Failed to restore, the account was deleted completely |
| 100232  | 	Unable to restore, no deletion history of the account |
| 100233  | 	Unable to login, the account was deleted |
| 100234  | 	The account is not authorized to login |
| 100230  | 	Initialization failed |
| 100240  | 	Apple authorization information does not match |
| 100241  | 	User cancelled Apple authorization request |
| 100242  | 	Apple authorization request failed |
| 100243  | 	Invalid response from Apple authorization request |
| 100244  | 	Failed to process Apple authorization request |
| 100245  | 	Apple authorization request failed for unknown reason |
| 100246  | 	System version does not support Apple authorization |
| 100300  | 	Invalid email address format |
| 100301  | 	Email addresses do not match |
| 100302  | 	Verification code request is too frequent |
| 100303  | 	Verification failed |
| 100304  | 	Verification failed too many times |
| 100305  | 	The account is banned |
| 100306  | 	Verification code cannot be empty |
| 100404  | 	Network error |
| 200100  | 	User birthday is required |
| 200110  | 	Monthly purchase limit exceeded |
| 200120  | 	Item does not exist |
| 200130  | 	Payment method does not exist |
| 200140  | 	serverTag does not exist |
| 200150  | 	Payment receipt verification failed |
| 200160  | 	Invalid purchase request |
| 200170  | 	Purchase request failed on game server |
| 200180  | 	It takes a long time for searching the purchase result |
| 200190  | 	Order ID does not exist |
| 200200  | 	Order status tracking timed out |
| 200210  | 	productid does not exist on payment backend |
| 200220  | 	Payment backend response - payment failed |
| 200230  | 	Payment backend response - payment canceled |
| 200240  | 	Current API version does not support the request |
| 200250  | 	Invalid parameters provided to API |
| 200260  | 	Fatal error during API operation |
| 200270  | 	The request is not supported by the Play store on current device |
| 200280  | 	Item has already been purchased, not consumed yet |
| 200290  | 	Item has already been purchased, failed to consume |
| 200300  | 	Unable to purchase the requested item |
| 200310  | 	Unable to connect to Google Play service |
| 200320  | 	Request reached maximum timeout before receiving any response from Google Play |
| 200330  | 	Network connection is turned off |
| 200340  | 	Payment canceled by user |
| 200350  | 	Item ID search failed |
| 200360  | 	Connection to play services failed |
| 300100  | 	System sharing failed |

### 日语对照表

| エラーコード | エラー説明 |
| ------ | ------ |
| -1 | 	不明なエラーが発生しました\nエラーコード:-1 |
| 0  | 	操作に成功しました\nエラーコード:0 |
| 100100  | 	このデバイスによるゲーム利用は制限されています\nエラーコード:100100 |
| 100110  | 	ログイン中にエラーが発生しました（UIDとtoken照合失敗）\nエラーコード:100110 |
| 100111  | 	アカウント作成に失敗しました\nエラーコード:100111 |
| 100112  | 	アカウント連携に失敗しました\nエラーコード:100112 |
| 100113  | 	ユーザー認証に失敗したため、ログインに失敗しました\nエラーコード:100113 |
| 100114  | 	このIPアドレスでのアクセスは制限されています\nエラーコード:100114 |
| 100115  | 	このデバイスのゲーム利用は制限されています\nエラーコード:100115 |
| 100116  | 	このアカウントのゲーム利用は制限されています\nエラーコード:100116 |
| 100117  | 	認証データにエラーが発生しました\nエラーコード:100117 |
| 100120  | 	このIPアドレスでのアクセスは制限されています\nエラーコード:100120 |
| 100130  | 	このアカウントのゲーム利用は制限されています\nエラーコード:100130 |
| 100140  | 	アカウント認証に失敗しました\nエラーコード:100140 |
| 100150  | 	引継ぎコードとUIDが一致しません\nエラーコード:100150 |
| 100160  | 	誕生日が入力済です\nエラーコード:100160 |
| 100170  | 	誕生日は【YYYYMMDD】の形式（例：19900101）で入力してください\nエラーコード:100170 |
| 100180  | 	ゲームアカウントと連携していないSNSアカウントです\nエラーコード:100180 |
| 100190  | 	SNSアカウント連携状況の照合に失敗しました\nエラーコード:100190 |
| 100200  | 	提すでに他のアカウントと連携済みです\nエラーコード:100200 |
| 100201  | 	現在使用中のGoogle Play Gamesアカウントはすでに別のゲームデータと連携済みです。連携情報をリセットし、現在プレイ中のデータと連携しますか？ |
| 100202  | 	現在プレイ中のゲームデータはすでに別のGoogle Play Gamesアカウントと連携済みです。連携情報をリセットし、現在使用中のGoogle Play Gamesアカウントと連携しますか？ |
| 100203  | 	現在ご利用しているGoogle Play Gamesアカウントとゲームデータは、それぞれ異なる連携情報が登録されております。連携情報を全部リセットし、当該データとGoogle Play Gamesアカウントの連携を行いますか？ |
| 100204  | 	現在ご利用しているゲームデータは別の端末に移行するには、ほかのSNSアカウントやメールアドレスなどと連携する必要があります |
| 100205  | 	バインド解除に失敗しました。ゲーム アカウントが Google Play ゲーム アカウントにバインドされていません。 |
| 100206  | 	現在プレイ中のゲームデータがGoogle Play Gamesアカウントと自動的に連携され、別の端末でプレイできるようになります |
| 100210  | 	ゲームアカウントと連携していないSNSアカウントです\nエラーコード:100210 |
| 100211  | 	外部サービスとの通信時にエラーが発生しました\nエラーコード:100211 |
| 100212  | 	外部サービスとの通信時にエラーが発生しました\nエラーコード:100212 |
| 100213  | 	連携解除に失敗しました\nエラーコード:100213 |
| 100214  | 	Google Play Games以外の連携を解除すると、Google Play Gamesアカウントとの連携も自動的に解除されます。「本当に連携を解除しますか」 |
| 100220  | 	連携を解除しました\nエラーコード:100220 |
| 100221  | 	Facebook連携に失敗しました\nエラーコード:100221 |
| 100222  | 	Twitter連携に失敗しました\nエラーコード:100222 |
| 100223  | 	Google連携に失敗しました\nエラーコード:100223 |
| 100224  | 	Googleとの通信に失敗しました\nエラーコード:100224 |
| 100225  | 	Google連携を解除しました\nエラーコード:100225 |
| 100226  | 	ログイン中のため、しばらくお待ち下さい\nエラーコード:100226 |
| 100227  | 	このアカウントでのログインに失敗しました\nエラーコード:100227 |
| 100228  | 	アカウントが削除されました\nエラーコード:100228 |
| 100229  | 	すでに削除済みです\nエラーコード:100229 |
| 100231  | 	このアカウントは完全に削除されたため、復元できません\nエラーコード:100231 |
| 100232  | 	このアカウントは削除されていないため、復元できません\nエラーコード:100232 |
| 100233  | 	このアカウントは削除されたため、ログインできません\nエラーコード:100233 |
| 100234  | 	このアカウントはログインできません\nエラーコード:100234 |
| 100230  | 	SDK起動に失敗しました\nエラーコード:100230 |
| 100240  | 	Appleアカウントの情報を正しく入力してください\nエラーコード |
| 100241  | 	Apple連携がキャンセルされました\nエラーコード |
| 100242  | 	Apple連携に失敗しました\nエラーコード |
| 100243  | 	Apple連携に失敗しました\nエラーコード |
| 100244  | 	Apple連携に失敗しました\nエラーコード |
| 100245  | 	Apple連携に失敗しました\nエラーコード |
| 100246  | 	システムバージョンが古いため、Apple連携できません\nエラーコード |
| 100300  | 	無効なメールアドレスです\nエラーコード:100300 |
| 100301  | 	メールアドレスが一致しません\nエラーコード:100301 |
| 100302  | 	認証メッセージの送信回数が上限に達したため、しばらく経ってからお試しください\nエラーコード:100302 |
| 100303  | 	正しい認証コードを入力してください\nエラーコード:100303 |
| 100304  | 	認証コード入力に失敗しました。認証コードを再度発行してください\nエラーコード:100304 |
| 100305  | 	このメールアドレスでの利用は制限されています\nエラーコード:100305 |
| 100306  | 	認証コードを入力してください\nエラーコード:100306 |
| 100404  | 	通信エラーが発生しました\nエラーコード:100404 |
| 200100  | 	購入に失敗しました、誕生日が設定されていません\nエラーコード:200100 |
| 200110  | 	購入に失敗しました、今月の購入上限金額に達しています\nエラーコード:200110 |
| 200120  | 	購入に失敗しました、アイテムが存在しません\nエラーコード:200120 |
| 200130  | 	購入に失敗しました、決済システムにエラーが発生しました\nエラーコード:200130 |
| 200140  | 	購入に失敗しました、サーバーとの通信に失敗しました\nエラーコード:200140 |
| 200150  | 	領収書の照合に失敗しました\nエラーコード:200150 |
| 200160  | 	不正な購入リクエストです\nエラーコード:200160 |
| 200170  | 	不正な購入リクエストです\nエラーコード:200170 |
| 200180  | 	サーバーと通信中です。しばらくお待ち下さい\nエラーコード:200180 |
| 200190  | 	購入リクエストが存在しません\nエラーコード:200190 |
| 200200  | 	購入時に通信エラーが発生しました\nエラーコード:200200 |
| 200210  | 	決済システムにエラーが発生しました\nエラーコード:200210 |
| 200220  | 	決済システムへの通信時にエラーが発生しました\nエラーコード:200220 |
| 200230  | 	決済システムへの通信がキャンセルされました\nエラーコード:200230 |
| 200240  | 	Google Playをバージョンアップしてください\nエラーコード:200240 |
| 200250  | 	APIに問題が発生しました\nエラーコード:200250 |
| 200260  | 	APIに問題が発生しました\nエラーコード:200260 |
| 200270  | 	Google Playをバージョンアップしてください\nエラーコード:200270 |
| 200280  | 	このアイテムはすでに所持済みです\nエラーコード:200280 |
| 200290  | 	このアイテムはすでに所持済みです\nエラーコード:200290 |
| 200300  | 	このアイテムは現在購入できません\nエラーコード:200300 |
| 200310  | 	Google Playへの接続に失敗しました、電波の良いところで再度お試しください\nエラーコード:200310 |
| 200320  | 	Google Playへの接続に失敗しました、電波の良いところで再度お試しください\nエラーコード:200320 |
| 200330  | 	ネットワークに接続してください\nエラーコード:200330 |
| 200340  | 	購入がキャンセルされました\nエラーコード:200340 |
| 200350  | 	アイテムの照合に失敗しました\nエラーコード:200350 |
| 200360  | 	決済システムへの接続に失敗しました\nエラーコード:200360 |
| 300100  | 	システムシェアに失敗しました\nエラーコード:300100 |

### 韩语对照表

| 오류 코드 | 오류 설명 |
| ------ | ------ |
| -1 | 	알 수 없는 에러 |
| 0  | 	성공 |
| 100100  | 	디바이스 번호 사용 정지 |
| 100110  | 	인증 실패 |
| 100111  | 	계정 생성 실패 |
| 100112  | 	계정 생성 성공, 계정 연동 실패 |
| 100113  | 	계정 연동 성공, 인증 실패 |
| 100114  | 	계정 생성 및 로그인 - IP 접근 제한 |
| 100115  | 	계정 생성 및 로그인 - 디바이스 번호 사용 정지 |
| 100116  | 	계정 생성 및 로그인 - UID 사용 정지 |
| 100117  | 	파라미터 부족 |
| 100120  | 	로그인 - IP 접근 제한 |
| 100130  | 	로그인 - UID 사용 정지 |
| 100140  | 	Access Token 인증 실패 |
| 100150  | 	제공한 UID와 Transcode 매칭 실패 |
| 100160  | 	생일이 이미 설정되었습니다. |
| 100170  | 	잘못된 생일 격식입니다. |
| 100180  | 	제공한 제3자 계정이 게임 계정과 연동되지 않았습니다. |
| 100190  | 	제공한 제3자 파라미터가 서버 인증에 실패하였습니다. |
| 100200  | 	제공한 제3자 계정은 이미 다른 UID와 연동되였습니다. |
| 100201  | 	현재 사용 중인 Google Play Games 계정은 이미 다른 게임 계정과 연동되어 있습니다. 연동 정보를 재설정하여 현재 생성 중인 게임 계정과 연동하시겠습니까? |
| 100202  | 	해당 게임 계정은 이미 다른 Google Play Games 계정과 연동되어 있습니다. 연동 정보를 재설정하여 현재 사용 중인 Google Play Games 계정과 연동하시겠습니까? |
| 100203  | 	현재 사용 중인 Google Play Games 계정과 게임 계정에 서로 다른 연동 정보가 등록되어 있습니다. 연동 정보를 모두 재설정하고 해당 게임 데이터와 Google Play Games 계정을 연동하시겠습니까? |
| 100204  | 	게스트 계정은 연동이 불가하며, Google Play Games 계정과 연동하려면 해당 게스트 계정을 우선 다른 SNS 계정 혹은 이메일 주소 등과 연동해야 합니다. |
| 100205  | 	해당 UID는 Google Play Games 계정과 연동되지 않았습니다. |
| 100206  | 	본 계정은 Google Play Games 계정과 자동으로 연동되었습니다. 기타 기기에서 해당 Google Play Games 계정을 통해 로그인할 수 있습니다. |
| 100210  | 	제공한 제3자 계정이 연동 계정과 매칭되지 않았습니다. |
| 100211  | 	연동 플랫폼 타입 에러 |
| 100212  | 	연동 해제 플랫폼 타입 에러 |
| 100213  | 	연동을 해제할 수 없습니다 |
| 100214  | 	해당 계정과의 연동을 해제하면 Google Play Games 계정과의 연동도 자동으로 해제됩니다. [연동을 해제하시겠습니까?] |
| 100220  | 	권한 요청 수락 취소 |
| 100221  | 	Facebook 권한 요청 수락 실패 |
| 100222  | 	트위터 권한 요청 수락 실패 |
| 100223  | 	Google 권한 요청 수락 실패 |
| 100224  | 	Google 서비스 이용불가 |
| 100225  | 	유저가 Google 권한 요청 수락을 취소하였습니다. |
| 100226  | 	현재 진행 중인 로그인 프로세스를 계속 진행할 수 없습니다. |
| 100227  | 	해당 계정 로그인 시도 실패 |
| 100228  | 	계정이 삭제되었습니다. |
| 100229  | 	중복하여 삭제할 수 없습니다. |
| 100231  | 	계정이 이미 완전히 삭제되어, 계정 복구를 진행할 수 없습니다. |
| 100232  | 	계정 삭제 기록이 존재하지 않아 계정 복구를 진행할 수 없습니다. |
| 100233  | 	계정이 이미 삭제되어 로그인할 수 없습니다. |
| 100234  | 	로그인 할 권한이 없습니다. |
| 100230  | 	초기화 실패 |
| 100240  | 	Apple 권한 수락 정보가 정확하지 않습니다 |
| 100241  | 	유저가 Apple 권한 수락 요청을 취소했습니다 |
| 100242  | 	Apple 권한 수락 요청 실패 |
| 100243  | 	Apple 권한 수락 응답 무효 |
| 100244  | 	Apple 권한 수락 요청을 처리할 수 없습니다 |
| 100245  | 	알 수 없는 원인으로 인해 Apple 권한 수락 요청에 실패하였습니다 |
| 100246  | 	Apple 권한 수락을 지원하지 않는 시스템 버전입니다 |
| 100300  | 	메일 주소 격식이 정확하지 않습니다. |
| 100301  | 	메일 주소 불일치 |
| 100302  | 	인증 코드 요청 빈도가 너무 빠릅니다. |
| 100303  | 	인증 실패 |
| 100304  | 	실패 횟수가 너무 많습니다. |
| 100305  | 	계정이 정지당했습니다. |
| 100306  | 	인증 코드는 비워둘 수 없습니다. |
| 100404  | 	인터넷 청구중 에러가 발생하였습니다. |
| 200100  | 	유저 생일 미설정 |
| 200110  | 	당월 과금금액이 보호 한도를 초과하였습니다. |
| 200120  | 	상품이 존재하지 않습니다. |
| 200130  | 	결제 채널이 존재하지 않습니다. |
| 200140  | 	serverTag가 존재하지 않습니다. |
| 200150  | 	결제 영수증 인증 실패 |
| 200160  | 	잘못된 구매 요청입니다. |
| 200170  | 	게임 서버 구매 청구 실패 |
| 200180  | 	구매 결과를 조회하는데 시간이 오래 걸립니다. |
| 200190  | 	오더 번호가 존재하지 않습니다. |
| 200200  | 	오더 상태 조회 유효 시간 초과 |
| 200210  | 	결제 채널 백그라운드에 해당 상품ID가 존재하지 않습니다. |
| 200220  | 	결제 채널 결제 철회 실패 |
| 200230  | 	결제 채널 결제 철회 취소 |
| 200240  | 	청구한 타입은 결산 API 버전을 지원하지 않습니다. |
| 200250  | 	API에 제공한 파라미터가 무효합니다. |
| 200260  | 	API 조작 중 치명적인 에러가 발생하였습니다. |
| 200270  | 	해당 디바이스의 Play 스토어는 요청한 기능을 수행할 수 없습니다. |
| 200280  | 	이미 아이템을 보유하고 있으며, 소모되지 않았습니다. |
| 200290  | 	이미 아이템을 보유하고 있으며, 소모에 실패하였습니다. |
| 200300  | 	청구한 품목을 구매할 수 없습니다. |
| 200310  | 	Google Play 서비스에 연결할 수 없습니다. |
| 200320  | 	GGoogle Play에서 응답하기 전, 요청사항이 최대 초과 시간에 도달하였습니다. |
| 200330  | 	인터넷 연결이 끊겨있습니다. |
| 200340  | 	유저가 결제를 취소 하였습니다. |
| 200350  | 	상품 ID 조회 실패 |
| 200360  | 	Play Service 연결 실패 |
| 300100  | 	시스템 공유 실패 |





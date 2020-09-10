|  版本   |  日期  |  说明 |
|  ----  | ----  |   ----  | 
| 2.1.32  | 2020/04/30 | 1: 增加亚马逊渠道，亚马逊支付，亚马逊登录,绑定,解绑功能；<br>2: GooglePlay渠道 增加游戏内在售商品列表获取；  |
| 2.1.33   | 2020/05/03 | 1:登录接口统一回调函数里添加 AMAZON_USER_ID, cp可根据改字段判断账号是否绑定过亚马逊；  |
| 2.1.34   | 2020/05/09 | 1: 解决亚马逊账号无法获取userName的问题; 老版本取用的是user_id字段，该字段为一串无意义的字符。现更新为用户昵称userName，和Fb,Tw平台保持一致；<br>2: Google内购商品货币价格获取接口中，获取到的货币代码 改为 货币符号；<br>3：修复FB,TW,GoogleMail登录缺陷，删除AiriSDKContentActivity  lunchMode配置，该配置会导致fb tw gmail三方账号登录时，游戏闪退  |
| 2.1.35   | 2020/05/13 | 1:修复亚马逊登录在某些情况没有回调的bug；（唤起浏览器登录后，关闭浏览器，返回游戏）<br>2:修复无GooglePlay设备中,点击支付闪退的缺陷；<br>3:修复Twitter登录流程中，某一个流程网络访问失败无回调的缺陷；  |
| 2.1.36  | 2020/05/27 | 1：修复初始化接口入参IS_DEVICE_NEW_CREATE为true时; 清除游戏缓存后，游客登录依然无法创建新账号的缺陷; |
| 2.1.37  | 2020/05/28 | 1: 修复iOS HelpShift导致闪退的缺陷<br>2: 修复Android版本google商品查询空指针异常； |
| 2.1.38  | 2020/06/24 | 1: 修复Android图片分享功能；<br>2: 去除Android版本SDK最低版本限制；<br>3: 修复Unity导出XCode工程后，遗失HelpShift库自带plist文件的缺陷； |
| 2.1.39  | 2020/07/24 | 1: Android更换底层网络请求框架；<br>2: Android 三次调用发货接口请求失败，即刻消耗订单，避免自动退款；<br>3: iOS下单前添加查单-发货-消耗流程;<br>4: 兼容Ipad设备上分享功能;<br>5: 彻底移除AndroidSD卡读写权限;<br>6: 修复IPad设备上Twitter登录时，点击登录框外部引发没回调缺陷 |
| 2.1.40  | 2020/08/19 |1: Unity设置面板添加 SD存储卡读写权限控制开关<br>2: Android/iOS添加FireBase远程配置功能接口 QueryRemoteConfig(string configKey)<br>3: Android更新FireBase库解决Android P设备对binder数量限制导致在亚马逊pad上crash问题 |
| 2.1.41  | 2020/08/21 | 1: Android/iOS Firebase远程配置功能链接到FireBase数据埋点 |
| 2.1.42  | 2020/09/10 | 1: IOS平台: 更新Firebase到V6.31；<br>2: IOS平台: 更新Adjust到V4.23；<br>3: Android/iOS: helpShift切换到AiHelp |

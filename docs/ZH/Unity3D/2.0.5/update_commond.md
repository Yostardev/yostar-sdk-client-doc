|  版本   |  日期  |  说明 |
|  ----  | ----  |   ----  | 
| 2.1.32  | 2020/04/30 | 1: 增加亚马逊渠道，亚马逊支付，亚马逊登录,绑定,解绑功能；<br>2: GooglePlay渠道 增加游戏内在售商品列表获取；  |
| 2.1.33  | 2020/05/03 | 1:登录接口统一回调函数里添加 AMAZON_USER_ID, cp可根据改字段判断账号是否绑定过亚马逊；  |
| 2.1.34  | 2020/05/09 | 1: 解决亚马逊账号无法获取userName的问题; 老版本取用的是user_id字段，该字段为一串无意义的字符。现更新为用户昵称userName，和Fb,Tw平台保持一致；<br>2: Google内购商品货币价格获取接口中，获取到的货币代码 改为 货币符号；<br>3：修复FB,TW,GoogleMail登录缺陷，删除AiriSDKContentActivity  lunchMode配置，该配置会导致fb tw gmail三方账号登录时，游戏闪退  |
| 2.1.35  | 2020/05/13 | 1:修复亚马逊登录在某些情况没有回调的bug；（唤起浏览器登录后，关闭浏览器，返回游戏）<br>2:修复无GooglePlay设备中,点击支付闪退的缺陷；<br>3:修复Twitter登录流程中，某一个流程网络访问失败无回调的缺陷；  |
| 2.1.36  | 2020/05/27 | 1：修复初始化接口入参IS_DEVICE_NEW_CREATE为true时; 清除游戏缓存后，游客登录依然无法创建新账号的缺陷; |
| 2.1.37  | 2020/05/28 | 1: 修复iOS HelpShift导致闪退的缺陷<br>2: 修复Android版本google商品查询空指针异常； |
| 2.1.38  | 2020/06/24 | 1: 修复Android图片分享功能；<br>2: 去除Android版本SDK最低版本限制；<br>3: 修复Unity导出XCode工程后，遗失HelpShift库自带plist文件的缺陷； |
| 2.1.39  | 2020/07/24 | 1: Android更换底层网络请求框架；<br>2: Android 三次调用发货接口请求失败，即刻消耗订单，避免自动退款；<br>3: iOS下单前添加查单-发货-消耗流程;<br>4: 兼容Ipad设备上分享功能;<br>5: 彻底移除AndroidSD卡读写权限;<br>6: 修复IPad设备上Twitter登录时，点击登录框外部引发没回调缺陷 |
| 2.1.40  | 2020/08/19 | 1: Unity设置面板添加 SD存储卡读写权限控制开关<br>2: Android/iOS添加FireBase远程配置功能接口 QueryRemoteConfig(string configKey)<br>3: Android更新FireBase库解决Android P设备对binder数量限制导致在亚马逊pad上crash问题 |
| 2.1.41  | 2020/08/21 | 1: Android/iOS Firebase远程配置功能链接到FireBase数据埋点 |
| 2.1.42  | 2020/09/10 | 1: iOS平台: 更新Firebase到V6.31；<br>2: iOS平台: 更新Adjust到V4.23；<br>3: Android/iOS:helpShift切换到AiHelp；<br> 4:新增客服工具接口参数:充值金额；<br> 5:新增客服工具接口参数:标签数组|
| 2.1.43  | 2020/09/29 | 1: Android平台添加OneStore、三星渠道支付; <br>2: iOS平台初始化时添加IDFA权限获取弹窗<br>3: 优化未登录游戏用户发起Aihelp客诉的接入方式；|
| 2.1.44  | 2020/11/10 | 1: iOS: IDFA授权弹窗提示文字本地化 (美日韩三服显示不同语言提示文字);<br>2:  Android/iOS:  清除缓存接口功能，不清除游客账号 (避免日服丢失账号)；<br>3: Android/iOS：登录回调中添加CHANNEL枚举字段，用于标识用户的注册渠道(韩服)；|
| 2.1.45  | 2020/12/08 | 1: Firebase purchase 事件埋点添加value值;<br>2:iOS平台支持IDFA横屏引导窗；|
| 2.1.46  | 2020/12/18 | 1: 内购支付接口serviceTag(支付服务器环境)增加；<br>2: Android: Firebase “purchase”事件重复埋点问题修复; |
| 2.1.47  | 2021/02/02 | 1: iOS: 权限提示文案XUPorter自动化配置（idfa授权、AiHelp客诉读取图片授权）；<br>2: Android: 修复Google账号在日服登录时，如果账号未绑定过sdk uid, 返回100180错误码； |
| 2.1.48  | 2021/02/07 | 1：Tw登录闪退缺陷修复 |
| 2.1.49  | 2021/02/19 | 1:  Android: oneStore \三星支付 添加支付事件埋点；<br>2:  Android: oneStore \三星支付 取消支付添加错误码 200231；<br>3:  iOS: Facebook SDK 更新到9.0；<br>4:  iOS: 系统授权框提示文案配置方式，优化到Xuporter中做自动化配置； |
| 2.1.50  | 2021/03/10 | 1: 新增自定义标签同步到Aihelp后台CRM系统的功能接口 |
| 2.1.51  | 2021/03/24 | 1:  Android:  Google登录参数的配置方式由本地调整为服务器下发；<br>2: iOS: 更新Firebase库至 v6.34.0 |
| 2.1.52  | 2021/04/26 | Android:<br>1: 更新support库到 androidx库;<br>2: 更新Aihelp库到2.4.2;<br>3: 适配Target Api 30;<br>4: 新增用户设备语言埋点；<br>5: 新增推送功能<br>iOS:<br>1: 升级adjust版本到4.28<br>2: 新增用户设备语言埋点；<br>3: 修复沙箱环境沙箱账号支付闪退bug<br>4: 新增推送功能 |
| 2.1.53  | 2021/05/20 | 1: 修复android平台aihelp入参为空闪退的缺陷 |
| 2.1.54  | 2021/05/20 | 1: 修复ios平台aihelp客诉时，未同步用户信息到客诉后台的缺陷 |
| 2.1.55  | 2021/06/16 | Android:<br>1: 升级google内购库版本至3.0.3;<br>2: 加入google内购反欺诈计划; |
| 2.1.56  | 2021/06/28 | Android:<br>1: 兼容高版本系统中推送图标显示;<br>iOS:<br>1:修复推送Token上传缺陷<br>2:修复AiHelp客诉消息同步缺陷<br>3:添加adServices库支持adjust无idfa广告归因 |
| 2.1.57  | 2021/07/29 | Android:<br>1: AndroidMainfest文件添加oneStore、三星、亚马逊应用包可见性配置；;<br>2:修复氪金回调有可能丢失的缺陷 |
| 2.1.58  | 2021/10/13 | iOS:<br>1: 氪金流程中添加200390错误码；<br>Android:<br>1:  Firebase兼容性优化 |
| 2.1.60  | 2021/12/25 | iOS:<br>1: 添加删除/恢复账号功能；<br>Android:<br>1:  添加删除/恢复账号功能；<br>2：添加PGS登陆服务接入 |
| 2.1.61  | 2022/01/14 | 1:Aihelp客诉流程变更；<br>2:增加问卷功能 |
| 2.1.64  | 2022/06/30 | 1:ios支持pgs账号解绑；<br>2:登陆回调中添加pgs账号信息；<br>3:首次绑定pgs后登陆添加对应code码 |
| 2.1.65  | 2022/08/02 | 1:nintendo支付逻辑调整，支持一包多区服氪金 |
| 2.1.66  | 2022/08/30 | 1:新增韩服KMC实名制认证 |

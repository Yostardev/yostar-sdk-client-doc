## 概述

!> MSDK登录功能是游戏玩家登录游戏的最快捷方便的方式：玩家可以使用QQ帐号，微信帐号，游客帐号登录您的游戏，可用于iOS、Android的手机，平板设备。

您可以参照下图在游戏登录页面放置登录按钮，应Appstore的要求，游客登录按钮需要放在第一个位置。

<center><img src="https://wiki.ssl.msdk.qq.com/Unity/res/login_screen_c.png" width="500"/></center>

MSDK登录可以打造出如下体验：

1. **快速创建游戏登录账户**： MSDK登录让用户能够快速轻松地在游戏内创建游戏登录账户，无需设置密码（可能在之后忘记）。这一简单方便的体验可以产生更高的转化量。
2. **个性化游戏运营**： MSDK登录后您可以授权获得玩家的头像，基本资料信息，方便游戏运营，能够产生更高的留存率。
3. **社交功能**： MSDK登录后游戏玩家可以进行好友间分享，建立游戏工会群等，以促进游戏内体验的分享。

## QQ登录

您可以调用MSDK接口拉起手Q客户端引导玩家给游戏进行授权。一般登录流程如下。

1. 在游戏登录页点击“与QQ好友玩”

<center><img src="https://wiki.ssl.msdk.qq.com/Unity/res/login_qq1_c.png" width="500"/></center>

2. 在手Q登录页完成授权

<center><img src="https://wiki.ssl.msdk.qq.com/Unity/res/login_qq2_c.png" width="500"/></center>

其中各区域说明如下：

+ 功能1.1: 授权登录按钮，点击可完成对游戏的登录授权。 
+ 功能1.2: 用户给游戏授权的权限列表，特殊注意是否有"访问应用里你的QQ好友信息"项，如果没有则会在获取用户关系链时报错"100030"。需要确认在java代码中初始MSDK后调用WGPlatform.WGSetPermission(WGQZonePermissions.eOPEN_ALL);。 
+ 功能1.3: "返回"按钮，用户点击后会取消登录，游戏有收到登录回调且flag为eFlag_QQ_UserCancel。 
+ 功能1.4: "切换账号"按钮，用户点击此按钮可在手Q内切换手Q账号，并用切换后的账号对游戏授权。

3. 登录成功，回到游戏进行选择区服或直接开始游戏

<center><img src="https://wiki.ssl.msdk.qq.com/Unity/res/login_qq3_c.png" width="500"/></center>

+ 功能1.5: 游戏本身的"进入游戏按钮，与MSDK功能无关。 
+ 功能1.6: 游戏"切换账号"按钮，调用MSDK的登出接口，然后返回游戏登录页。

## 微信登录

您可以调用MSDK接口拉起微信客户端引导玩家给游戏进行授权。登录流程如下。

1. 在游戏登录页点击“与微信好友玩”

<center><img src="https://wiki.ssl.msdk.qq.com/Unity/res/login_wx1_c.png" width="500"/></center>

2. 在微信登录页完成授权

<center><img src="https://wiki.ssl.msdk.qq.com/Unity/res/login_wx2_c.png" width="500"/></center>

+ 功能2.1: 授权登录按钮，点击可完成对游戏的登录授权。 
+ 功能2.2: 用户给游戏授权的权限列表，其中"寻找与你共同使用该应用的好友"项表示可获取用户关系链。此项权限需要精品类游戏在PR2阶段由协同规划组申请开通，具体可咨询游戏的腾讯接口人。 
+ 功能2.3: "取消"按钮，用户点击后会取消登录，游戏有收到登录回调且flag为eFlag_WX_UserCancel。 
+ 功能2.4: "重试"按钮，用户点击此按钮在微信App上重试授权登录。


?> 文档更新于 {docsify-updated}
### 1.GooglePlayGames
接了GooglePlayGame游戏登录的项目需要注意以下错误码：
+ 100201，100202，100203，100204为登录方法（SDKLogin，QuickLogin）所返回，用户已成功登录，只是GooglePlayGame绑定失败；
+ 100201，100202，100203，如果想强制绑定(原来发生冲突的绑定关系会先解绑)，可以直接调用ConfirmLinkGooglePlayGame接口。
+ 100205为解绑GooglePlayGames方法（SDKUnLink，所传平台为8）所返回；
+ 100214为解绑第三方账号方法（SDKUnLink，所传平台除了8）所返回，因为GooglePlayGameID不能绑定游客；如果想同时解除GooglePlayGames账号，可以再调用ConfirmUnLinkGooglePlayGame接口。
+ 100206为sdk uid首次绑定pgs账号后并登陆成功 
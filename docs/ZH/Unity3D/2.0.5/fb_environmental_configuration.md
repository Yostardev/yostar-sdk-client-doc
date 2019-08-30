### Facebook配置说明

#### 环境配置
进入到游戏开发者界面：[https://developers.facebook.com/](https://developers.facebook.com/)

点击登录按钮，登录自己的开发者账户。

回到开发者界面，选择`我的应用`

![fb_myapp](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/fb_my_app.png)

如果游戏还没有在此创建过用户，请选择`创建应用`按钮

#### 创建应用

点击`我的应用`中的创建应用后，会弹出以下界面框：

![fb_create_app](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/fb_create_app.png)

按照要求填写设置后，点击创建应用编号，进入应用界面：

![fb_setting_app](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/fb_app_setting.png)

保存应用编号。并选择Facebook登录选项，进入`登录平台选择界面`。

![fb_login_platfrom.png](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/fb_login_platfrom.png)

YostarSDK只需要配置`iOS`和`Android`平台的配置。

#### iOS应用配置

在登录平台选择界面，选择iOS平台，进入iOS设置界面。

+ 设置开发环境：已经内置在YostarSDK中，CP不需要重新设置

+ 添加 `Bundle ID`：请填写游戏的正确`Bundle ID`，配置完成点击`save`，再点击`继续`按钮

+ 为应用启用单点登录：可以根据游戏要求选择不强制。选择完成后，点击`save`，再点击`下一页`按钮

+ 配置 `info.plist`：已经内置在YostarSDK中，CP不需要重新配置。

+ 连接应用委托：已经内置在YostarSDK中，CP不需要重新配置。

+ 添加“Facebook 登录”按钮：已经内置在YostarSDK中，CP不需要重新配置。

+ 检查当前登录状态：已经内置在YostarSDK中，CP不需要重新配置。

+ 请求权限：已经内置在YostarSDK中，CP不需要重新配置。

#### Android应用配置

在登录平台选择界面，选择`Android`平台，进入`Android`设置界面

+ 下载 Android 版 Facebook SDK：已经内置在YostarSDK中，CP不需要重新配置

+ 导入 Facebook SDK：已经内置在YostarSDK中，CP不需要重新配置

+ 提供您的 Android 项目信息：根据游戏实际情况添加包名和APP启动类，设置完成后，点击`save`后再点击继续按钮。

+ 添加开发和发布密钥散列：密钥散列与APP签名文件相关，具体的生成命令为：

开发密钥散列：

Mac：
```cmd
keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore | openssl sha1 -binary | openssl base64
```

Windows：
```cmd
keytool -exportcert -alias androiddebugkey -keystore "C:\Users\USERNAME\.android\debug.keystore" | "PATH_TO_OPENSSL_LIBRARY\bin\openssl" sha1 -binary | "PATH_TO_OPENSSL_LIBRARY\bin\openssl" base64
```

发布密钥散列：    

```cmd
keytool -exportcert -alias YOUR_RELEASE_KEY_ALIAS -keystore YOUR_RELEASE_KEY_PATH | openssl sha1 -binary | openssl base64
```
生成完成后，添加到输入框内，点击`save`后再点击`继续`按钮进入下一步操作。

+ 为应用启用单点登录，可以根据游戏要求选择，不强制，选择完成后点击`save`，再点击`下一页`按钮。

+ 编辑您的资源和清单：已经内置在YostarSDK中，CP不需要重新配置

+ 记录应用事件：已经内置在YostarSDK中，CP不需要重新配置

+ 添加“Facebook 登录”按钮：已经内置在YostarSDK中，CP不需要重新配置

+ 注册回调：已经内置在YostarSDK中，CP不需要重新配置

+ 检查登录状态：已经内置在YostarSDK中，CP不需要重新配置



### Google登录配置说明

#### 凭据配置

+ 在[API控制台](https://console.developers.google.com/apis/credentials)中打开`凭据`页面。

![game_api_console_create](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/game_api_console_create.png)

+ 点击`创建凭据`，并选择`OAuth 客户端 ID`

![create_credentials](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/create_credentials.png)

+ 创建 OAuth 客户端 ID

  + 应用类型选择`Android`
  + 名称根据CP创建，不强制要求
  + 签名证书的指纹SHA-1的值：指纹创建命令如下：
  ```cmd
  keytool -exportcert -keystore path-to-debug-or-production-keystore -list -v
  ```
  + 软件包名称，为游戏的包名
  
设置完成后点击`创建`,完成凭据的配置。

#### 凭据获取

+ AiriSDK使用的`Google Api Client ID`为配置完成后，在`凭据`界面中最新的web client的客户端ID

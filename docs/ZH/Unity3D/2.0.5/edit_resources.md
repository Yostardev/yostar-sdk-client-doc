


### 配置接入参数

\* iOS平台Firebase配置文件 GoogleService-Info.plist 添加到`\Assets\AiriSDK\Plugins\iOS\`目录中;

\* android台Firebase配置文件 google-services.json 添加到`\Assets\Plugins\Android\assets\`目录中;


\* 选择菜单栏 *AiriSDK > Config Settings* 菜单项,打开YoStarSDK的参数配置面板;<br/>

![loading.png](https://sdkresources.oss-cn-shanghai.aliyuncs.com/AiriSDK%E6%8E%A5%E5%85%A5%E6%96%87%E6%A1%A3%E5%9B%BE%E5%BA%8A/unity_asset.png)
<br/>

\* 在配置面板中填写各项功能的接入参数;(若无对应的功能接入需求，相关参数可为空);
![airisdk_setting](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/unity_config.png)

填写完毕后依次点击 **Save Config**、**Modify Manifest**、**Modify Google Service Params** 按钮会将上述配置参数保存在以下目录:
- \Assets\AiriSDK\Resources\SDKConfigSettings.json
- \Assets\Plugins\Android\assets\api_key.txt
- \Assets\Plugins\Android\res\values\pgs_service_strings.xml
- \Assets\Plugins\Android\AndroidManifest.xml
- \Assets\Plugins\Android\res\values\google_service_strings.xml



可根据你的需求,将上述目录加入版本管理,避免每次出包频繁配置参数;
<br/><br/>
注: 以上参数必须正确填写，每次修改后，均需执行一次保存操作，否则游戏运行时将无法获得SDK配置参数；



#### Save config 按钮详解

- 点击```Save Config``` 按钮后，配置参数将保存到`\Assets\AiriSDK\Resources\SDKConfigSettings.json`文件中，运行时供SDK读取。
- Amazon登录功能所需`Amazon ApiKey`参数会保存到`Android/assets/api_key.txt`文件中，运行时供SDK读取。
- PGS登录功能所需`Play game app id`参数会保存到`\Assets\Plugins\Android\res\values\pgs_service_strings.xml`文件中，运行时供SDK读取。


#### Modify Manifest按钮详解

点击```Modify Manifest```按钮后，会将接入aihelp客服sdk、oneStore支付sdk所需的相关参数保存到`\Assets\Plugins\Android\AndroidManifest.xml`文件中，运行时供SDK读取。

例：
```xml
<meta-data android:name="aihelp_apiKey" android:value="xxx" />
<meta-data android:name="aihelp_demain" android:value="xxx" />
<meta-data android:name="aihelp_appId" android:value="xxx" />
<meta-data android:name="oneStore_publicKey"  android:value="MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQCYEzSR7kxcQeVT3BPbSufVXH1SnRNjZlk8/G6CXjc8X5Ajms3YFUHtYJZ9/XaBFyJZpuG2OKxxPoXl9KjnRHLZELyxKdThJYYdWP6gpDJalsw+sem6hqiTwt5zeHsEFFv5UQPVU9G4rv99eXTbOvE1HN4phi2ydJH3YoWj781FfQIDAQAB" />
```


#### Modify Google Service Params按钮详解
点击```Modify Manifest```按钮后，会将`\Assets\Plugins\Android\assets\google-services.json`文件解析后，保存到`\Assets\Plugins\Android\res\values\google_service_strings.xml`中，运行时供Firebase SDK读取

例：
```xml
    <string name="default_web_client_id">1xxxxxx.apps.googleusercontent.com</string>
    <string name="fcm_fallback_notification_channel_label">xxxxxx</string>
    <string name="firebase_database_url">xxxxxxxxxxx</string>
    <string name="gcm_defaultSenderId">xxxxxx</string>
    <string name="google_api_key">xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</string>
    <string name="google_app_id">xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</string>
    <string name="google_crash_reporting_api_key">xxxxxxxxxxxxxxxxxxxxxxxxxx</string>
    <string name="google_storage_bucket">xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</string>
    <string name="project_id">xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</string>
    <string name="server_client_id">xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx</string>
    <string name="app_id">xxxxxxxxxx</string>
```

### AndroidManifest.xml配置

针对海外版本，SDK在android平台下需要对manifest.xml文件做一下必要修改

#### 1、AU支付

```xml
<uses-permission android:name="com.kddi.market.permission.USE_ALML" />
```

### Xcode工程需要的配置

#### 需要在`Xcode`工程的`Capability`开启`Push Notifications`和`Sign In with Apple`
![Capability_setting](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/2.0.5_Capability_setting.png)


#### Unity 2019.3之后，出xcode时，unity会把bundle资源包加到unity framework路径中，导致路径不对加载不到资源文件，需做如下设置
![bundle_setting](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/2.0.5_bundle_setting.png)


### 接入 `Associated Domains` 功能（可选）
`Associated Domains` *（此功能可选可以开启Apple universal link 功能）*
点击加号添加一项，输入`applinks:webusstatic.yo-star.com`
![Capability_setting](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/2.0.5_Associated_domains.png)


### 接入URL Scheme 功能 （可选）
#### 需要在`Xcode`工程的`Info`中的`URL Types`添加自己的scheme
`URL scheme` 格式 `Yostar-App的名称+区服`, 比如 `Yostar-ArknightsEN`
![URLType_setting](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/2.0.5_url_type_setting.png)

#### 检查Link->Runpath Search Paths下，是否有@executable_path/Frameworks， 没有的话新增


### iOS端接入远程推送功能（可选）

####  实现富媒体推送（主要指在推送中出现图片）,如下样式：
![notification_media_style](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/notification_media_style.png)

需要额外做一下工作：
##### 1. Notification Service Extension添加步骤：`Xcode` -> `File` -> `New` -> `Target`，选择Notification Service Extension，如下图所示：
![notification_ext_create](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/notification_ext_create.png)



输入ProductName名，请务必使用`YostarNotification`，**以便在使用手动签名时，我们配置正确的签名证书**，创建完成后在目录下Xcode会自动生成NotificationService的模板:
![notification_ext_named](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/notification_ext_named.png)

会出现一下文件夹:
![notification_ext_end](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/notification_ext_end.png)


需要如下设置：
![notification_ext_buildsetting](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/notification_ext_buildsetting.png)
##### 2. 在`NotificationService.m`文件中修改如下
```objectivec
@implementation NotificationService

- (void)didReceiveNotificationRequest:(UNNotificationRequest *)request withContentHandler:(void (^)(UNNotificationContent * _Nonnull))contentHandler {
    self.contentHandler = contentHandler;
    self.bestAttemptContent = [request.content mutableCopy];
    
    [self loadAttachments:self.bestAttemptContent.userInfo[@"fcm_options"][@"image"]];

}

- (void)serviceExtensionTimeWillExpire {
    // Called just before the extension will be terminated by the system.
    // Use this as an opportunity to deliver your "best attempt" at modified content, otherwise the original push payload will be used.
    self.contentHandler(self.bestAttemptContent);
}

- (void)loadAttachments:(NSString *)attachUrl {
    if (!attachUrl) {
        self.contentHandler(self.bestAttemptContent);
        return;
    }
    //另一种下载方式
    NSURLSession *session = [NSURLSession sharedSession];
    NSURL *url = [NSURL URLWithString:attachUrl];
    
    NSURLSessionDownloadTask *downloadTask = [session downloadTaskWithURL:url
                                                        completionHandler:^(NSURL * _Nullable location,
                                                                            NSURLResponse * _Nullable response,
                                                                            NSError * _Nullable error) {
        NSString *caches = [NSSearchPathForDirectoriesInDomains(NSCachesDirectory, NSUserDomainMask, YES) lastObject];
        // response.suggestedFilename ： 建议使用的文件名，一般跟服务器端的文件名一致
        NSString *file = [caches stringByAppendingPathComponent:response.suggestedFilename];
        
        // 将临时文件剪切或者复制Caches文件夹
        NSFileManager *mgr = [NSFileManager defaultManager];
        
        // AtPath : 剪切前的文件路径
        // ToPath : 剪切后的文件路径
        [mgr moveItemAtPath:location.path toPath:file error:nil];
        
        if (file && ![file  isEqualToString: @""])
        {
            UNNotificationAttachment *attch= [UNNotificationAttachment attachmentWithIdentifier:@"photo"
                                                                                            URL:[NSURL URLWithString:[@"file://" stringByAppendingString:file]]
                                                                                        options:nil
                                                                                          error:nil];
            if(attch)
            {
                self.bestAttemptContent.attachments = @[attch];
            }
        }
        self.contentHandler(self.bestAttemptContent);
    }];
    [downloadTask resume];
}

@end
```
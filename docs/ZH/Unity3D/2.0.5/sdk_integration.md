

### Step1: 导入AiriSDK
\* Unity编辑器打开游戏工程后, 依次双击AiriSDK和Resource的unitypackage 导入到游戏工程;<br/>
\* 如果你的游戏工程中已经有自定义的AndroidManifest.xml ,在导入AiriSDK时请注意，避免该文件被覆盖重写;

##### AiriSDK目录结构
![logo](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/plugin210.png)

### Step2: 配置接入参数
\* 选择菜单栏 *AiriSDK > Config Settings* 菜单项,打开AiriSDK的参数配置面板;<br/>
![loading.png](https://sdkresources.oss-cn-shanghai.aliyuncs.com/AiriSDK%E6%8E%A5%E5%85%A5%E6%96%87%E6%A1%A3%E5%9B%BE%E5%BA%8A/unity_asset.png)
<br/>

* 在配置面板中填写各项功能的接入参数;(若不打算接入对应的功能，相关参数可为空);
![airisdk_setting](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/unity_config.jpg)

* 填写完毕后,**请依次点击下方保存按钮**,会将上述配置参数保存在以下目录:
- \Assets\AiriSDK\Resources\
- \Assets\Plugins\Android\res\values\google_service_strings.xml
- \Assets\Plugins\Android\AndroidManifest.xml

可根据你的需求,将上述目录加入git管理,避免每次出包频繁配置参数;
<br/><br/>
注: 以上参数必须正确填写，每次修改后，均需执行一次保存按钮，否则游戏运行时将无法获得SDK配置参数；



### Xcode工程基础配置
- 在编译iOS平台游戏时,我们从Unity中导出Xcode工程后,需在Xcode工程中手动开启`Push Notifications`和`Sign In with Apple` 这两项`Capability`；

![Capability_setting](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/2.0.5_Capability_setting.png)


### Xcode工程可选配置（推送功能）
- 如果需实现如下的富媒体推送功（推送消息中支持图片媒体显示）,需在Xcode功能中做如下配置:

![notification_media_style](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/notification_media_style.png)

##### 1. Notification Service Extension添加步骤：`Xcode` -> `File` -> `New` -> `Target`，选择Notification Service Extension，如下图所示：
![notification_ext_create](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/notification_ext_create.png)

输入Target名，创建完成后在目录下Xcode会自动生成NotificationService的模板:
![notification_ext_named](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/notification_ext_named.png)

会出现一下文件夹:
![notification_ext_end](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/notification_ext_end.png)


需要如下设置：
![notification_ext_buildsetting](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/notification_ext_buildsetting.png)
##### 2. 在`NotificationService.m`文件中修改如下 (可完全复制替换)
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

    NSURLSession *session = [NSURLSession sharedSession];
    NSURL *url = [NSURL URLWithString:attachUrl];    
    NSURLSessionDownloadTask *downloadTask = [session downloadTaskWithURL:url
                                                        completionHandler:^(NSURL * _Nullable location,
                                                                            NSURLResponse * _Nullable response,
                                                                            NSError * _Nullable error) {

        NSString *caches = [NSSearchPathForDirectoriesInDomains(NSCachesDirectory, NSUserDomainMask, YES) lastObject];
        NSString *file = [caches stringByAppendingPathComponent:response.suggestedFilename];
     
        NSFileManager *mgr = [NSFileManager defaultManager];
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
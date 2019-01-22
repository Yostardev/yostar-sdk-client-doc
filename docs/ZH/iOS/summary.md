### 1. 概述
### 2. 接入流程
### 3. SDK使用
#### 1. 概述
本文档面向iOS开发者，Airi iOS SDK 使用OC编程开发。
本文档用于指导开发者快速接入 Airi iOS SDK 为iOS应用提供登录、注册、支付、分享、App Store评分、客服等功能。
**iOS 支持最低版本 iOS 9.0**
#### 2. 接入流程
* 在info.plist添加如下内容：

```
<key>NSPhotoLibraryUsageDescription</key>
<string>NeedToAccessYourPhotoAlbum</string>

<key>CFBundleURLTypes</key>
<array>
<dict>
<key>CFBundleURLName</key>
<string>facebook-unity-sdk</string>
<key>CFBundleURLSchemes</key>
<array>
<string>fb962***1548(填写你的fbid)</string>
</array>
</dict>
<dict>
<key>CFBundleTypeRole</key>
<string>Editor</string>
<key>CFBundleURLSchemes</key>
<array>
<string>twitterkit-e7wRygYH7***VXzeUKm(填写你的twkey)</string>
</array>
</dict>
</array>

<key>FacebookAppID</key>
<string>962****548(填写你的fbid)</string>
<key>LSApplicationQueriesSchemes</key>
<array>
<string>twitter</string>
<string>twitterauth</string>
<string>fbapi</string>
<string>fbauth2</string>
<string>fb-messenger-api</string>
<string>fbshareextension</string>
</array>
```

* 配置后台模式功能，启用以下功能:

•    Background fetch

•    Remote notifications
如图：
![](https://upload-images.jianshu.io/upload_images/1948913-02273c6beb8989b6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### 1. 使用Cocoapods进行自动集成
请Podfile根据要集成的版本将以下行之一添加到您的行中。
```
pod 'AiriSDK'，'~>2.1.4'＃需要接入的版本
```
并运行`pod install`或`pod update`刷新您的依赖项，至此接入完成。
##### 2. 手动集成

[下载最新的Airi iOS SDK]()
* 将下载的包解压后添加到项目中，并导入所需的系统framework

```
AdSupport
iAd
CoreTelephony
CoreGraphics
QuartzCore
CoreText
SystemConfiguration
CoreTelephony
UIKit
Security
QuickLook
CoreLocation
MobileCoreServices
CoreSpotlight
Photos (needed only for v5.10.0 or later)
WebKit (needed only for v5.10.0 or later)
SafariServices
libsqlite3.tbd
libicucore.tbd
libz.tbd
```
添加完成后如图：
![](https://upload-images.jianshu.io/upload_images/1948913-cebf3cf912812bc6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* 导入资源包成功如图：
![](https://upload-images.jianshu.io/upload_images/1948913-8575cd5252d89fa6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
* 设置Other Linker Flags
在工程 Target 的 Build Settings ->Linking ->Other Linker Flags 添加“-ObjC”，如下图：
![](https://upload-images.jianshu.io/upload_images/1948913-41590a26bd94178c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#### 3. SDK使用

```
// 导入头文件
#import "AiriSDKAppDelegate.h"

// 在以下方法中添加如下代码：
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
[AiriSDKAppDelegate AiriSDKApplication:application didFinishLaunchingWithOptions:launchOptions];
return YES;
}

- (BOOL)application:(UIApplication *)app openURL:(NSURL *)url options:(NSDictionary<NSString *,id> *)options{
return [AiriSDKAppDelegate AiriSDKApplication:app openURL:url options:options];
}

- (void)application:(UIApplication*)application didReceiveRemoteNotification:(NSDictionary*)userInfo{
[AiriSDKAppDelegate AiriSDKApplicationDidReceiveRemoteNotification:userInfo];
}

- (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken{
[AiriSDKAppDelegate AiriSDKApplicationDidRegisterForRemoteNotificationsWithDeviceToken:deviceToken];
}

- (void)applicationDidBecomeActive:(UIApplication *)application {
[AiriSDKAppDelegate AiriSDKApplicationDidBecomeActive];
}
```

* 在使用类中导入头文件`#import "AiriSDKInstance.h"`
* 在合理的地方调用初始化方法(该方法会请求平台获取相关应用配置信息) 

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

+ 配置后台模式功能，启用以下功能:

•    Background fetch

•    Remote notifications
如图：
![](https://upload-images.jianshu.io/upload_images/1948913-02273c6beb8989b6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### 1. 使用Cocoapods进行自动集成
请Podfile根据要集成的版本将以下行添加到您的行中。
```
pod 'AiriSDK'，'~>2.1.4'＃需要接入的版本
```
并运行`pod install`或`pod update`刷新您的依赖项，至此接入完成。
##### 2. 手动集成

[下载最新的Airi iOS SDK]()
+ 将下载的包解压后添加到项目中，并导入所需的系统framework
`AdSupport`
`iAd`
`CoreTelephony`
`CoreGraphics`
`QuartzCore`
`CoreText`
`SystemConfiguration`
`CoreTelephony`
`UIKit`
`Security`
`QuickLook`
`CoreLocation`
`MobileCoreServices`
`CoreSpotlight`
`Photos`
`WebKit`
`SafariServices`
`libsqlite3.tbd`
`libicucore.tbd`
`libz.tbd`
添加完成后如图：
![](https://upload-images.jianshu.io/upload_images/1948913-cebf3cf912812bc6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
+ 导入资源包成功如图：
![](https://upload-images.jianshu.io/upload_images/1948913-8575cd5252d89fa6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
+ 设置Other Linker Flags
在工程 Target 的 Build Settings ->Linking ->Other Linker Flags 添加“-ObjC”，如下图：
![](https://upload-images.jianshu.io/upload_images/1948913-41590a26bd94178c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#### 3. SDK使用
```objectivec
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
+ 在使用类中导入头文件`#import "AiriSDKInstance.h"`

#### 3.1. 创建单例接口
+ 调用API
```objectivec
+ (instancetype)yostarShareton;
```
+ 调用实例
```objectivec
self.airiSDK = [AiriSDKInstance yostarShareton];
```

#### 3.2. 获取DevicdID 接口
+ 调用API
```objectivec
+ (NSString *)SDKGetDeviceID;
```
+ 调用实例
```objectivec
NSString *deviceStr = [AiriSDKInstance SDKGetDeviceID];
```

#### 3.3. Helpshift客服 接口
+ 调用API
```objectivec
+ (void)SDKOpenHelpShift;
```
+ 调用实例
```objectivec
[AiriSDKInstance SDKOpenHelpShift];
```

#### 3.4. appstore 评分 接口
+ 调用API
```objectivec
+ (void)RequestStoreReview;
```
+ 调用实例
```objectivec
[AiriSDKInstance RequestStoreReview];
```

#### 3.5. 初始化SDK 接口
+ 调用API
```objectivec
- (void)initSDK:(InitSuccessHandle)success fail:(InitFailHandle)fail;
```
+ 调用实例
```objectivec
[self.airiSDK initSDK:^(NSDictionary *result) {
NSLog(@"%@", result);
} fail:^(NSDictionary *result) {
NSLog(@"%@", result);
}];
```

#### 3.6. 登录 接口
+ 调用API
```objectivec
- (void)SDKLogin:(NSInteger)platform param1:(NSString *)param1 param2:(NSString *)param2 isCreateNew:(BOOL)isCreateNew success:(LoginSuccessHandle)success fail:(LoginFailHandle)fail;
```
+ 调用实例
```objectivec
[self.airiSDK SDKLogin:platform param1:param1 param2:param2 isCreateNew:isNew success:^(NSDictionary *result) {
NSLog(@"%@*****", result);
} fail:^(NSDictionary *result) {
NSLog(@"%@*****", result);
}];
```
+ 接口参数说明

|参数名称|参数类型|参数说明|是否必须|
|----|----|----|----|
|platform|NSInteger|登录的渠道有DEVICE(0),TRANSCODE(1),TWITTER(2),FACEBOOK(3),YOSTAR(4)|是|
|param1|NSString|当Platform的值为1时，param1代表继承码。当Platform的值为4时，param1为邮箱账号|否|
|param2|NSString|当Platform的值为1时，param2代表继承码对应的UID。当Platform的值为4时，param2为邮箱收到的验证码|否|
|isNew|BOOL|是否强制创建新的账号|是|

#### 3.7. 快速登录 接口
+ 调用API
```objectivec
- (void)SDKQuickLogin:(QuickLoginSuccessHandle)success fail:(QuickLoginFailHandle)fail;
```
+ 调用实例
```objectivec
[self.airiSDK SDKQuickLogin:^(NSDictionary *result) {
NSLog(@"Quick::%@", result);
} fail:^(NSDictionary *result) {
NSLog(@"Quick::%@", result);
}];
```

#### 3.8. 发行继承码接口
+ 调用API
```objectivec
- (void)SDKTranscodeReq:(TranscodeReqSuccessHandle)success fail:(TranscodeReqFailHandle)fail;
```
+ 调用实例
```objectivec
[self.airiSDK SDKTranscodeReq:^(NSDictionary *result) {
NSLog(@"TranscodeReq::%@", result);
} fail:^(NSDictionary *result) {
NSLog(@"TranscodeReq::%@", result);
}];
```

#### 3.9. 请求验证码接口
+ 调用API
```objectivec
- (void)SDKVerificationCodeReq:(NSString *)accountEmail success:(VerCodeReqSuccessHandle)success fail:(VerCodeReqFailHandle)fail;
```
+ 调用实例
```objectivec
[self.airiSDK SDKVerificationCodeReq:accountEmail success:^(NSDictionary *result) {
NSLog(@"%@*****", result);
} fail:^(NSDictionary *result) {
NSLog(@"%@*****", result);
}];
```
+ 接口参数说明

|参数名称|参数类型|参数说明|是否必须|
|----|----|----|----|
|accountEmail|NSString|要验证的邮箱账号|是|






// 绑定
- (void)SDKLink:(NSInteger)platfrom param1:(NSString *)param1 param2:(NSString *)param2 success:(LinkSuccessHandle)success fail:(LinkFailHandle)fail;
// 解绑
- (void)SDKUnLink:(NSInteger)platform success:(UnLinkSuccessHandle)success fail:(UnLinkFailHandle)fail;
// 新绑定接口
- (void)SDKNewAccountLink:(ReLinkSuccessHandle)success fail:(ReLinkFailHandle)fail;
// 设置生日
- (void)SDKSetBirth:(NSString *)birthDay success:(BirthSuccessHandle)success fail:(BirthFailHandle)fail;
// 事件上传
- (void)SDKUserEventUpload:(NSString *)strEventName strJson:(NSString *)strJson;
// 注销、清空token
- (void)SDKLogout:(LogoutHandle)handle;
// 自带分享
- (void)SDKSystemShare:(NSString *)strShareText shareImageData:(NSData *)shareImageData success:(ShareSuccessHandle)success fail:(ShareFailHandle)fail;
// 购买商品
- (void)SDKPurchase:(NSString *)productId serverTag:(NSString *)serverTag extraData:(NSString *)extraData success:(PurchaseSuccessHandle)success fail:(PurchaseFailHandle)fail;

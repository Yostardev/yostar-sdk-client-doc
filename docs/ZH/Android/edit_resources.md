## 编辑您的资源和清单

### Assets资源

AiriSDK的环境资源和日志开关等参数都是由```assets/AiriSDKConf.properties```文件中的参数控制，请开发者设置一下参数：

参数值请联系悠星商务进行获取。

| 参数名称 | 参数说明 | 是否必须 |
| ------ | ------ | ------ |
| AIRISDK_URL | 分配的AiriSDK服务器访问地址 | 是 |
| AIRISDK_PAYSTOREID | 游戏支持的支付方式，默认为googleplay | 是 |
| AIRISDK_SHOWDEBUGLOG | AiriSDK日志打印，默认为false，不打印 | 是 |
| AIRISDK_NEWDEVICE | 是否将当前机器当作全新的机器使用，默认为false | 是 |

### AndroidManifeset配置

#### 客服系统

AiriSDK集成了Helpshift作为客服管理工具，所以在Package Explorer中，打开安卓项目的AndroidManifest.xml。在<application>元素中添加以下 meta-data 标签，配置对应的Helpshift参数。

获取参数值请咨询悠星商务人员。

```xml
<meta-data android:name="helpshift_apiKey" android:value="xxxxxxx" />
<meta-data android:name="helpshift_demain" android:value="xxxxx" />
<meta-data android:name="helpshift_appId" android:value="xxxxxxxxxxx" />
```

### AU支付权限

AiriSDK也集成了AU支付渠道，如果您的游戏有AU支付的需求，请在AndroidManifeset.xml文件中添加以下权限：

```xml
<uses-permission android:name="com.kddi.market.permission.USE_ALML" />
```


### res资源配置

AiriSDK集成了firebase的部分功能，需要在```res/values/google_service_strings.xml```中配置firebase服务参数。

获取参数值请咨询悠星商务人员。

```xml
<string name="default_web_client_id">***</string>
<string name="fcm_fallback_notification_channel_label">****</string>
<string name="firebase_database_url">*****</string>
<string name="gcm_defaultSenderId">*****</string>
<string name="google_api_key">******</string>
<string name="google_app_id">******</string>
<string name="google_crash_reporting_api_key">******</string>
<string name="google_storage_bucket">*****</string>
<string name="project_id">*****</string>
```

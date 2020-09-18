

### 1.AndroidManifeset配置

#### 客服系统

如果需要集成AiHelp作为客服管理工具，打开安卓项目的AndroidManifest.xml。在<application>元素中添加以下 meta-data 标签，配置对应的Helpshift参数。

获取参数值请咨询悠星商务人员。

```xml
<meta-data android:name="aihelp_apiKey" android:value="xxxxxxx" />
<meta-data android:name="aihelp_demain" android:value="xxxxx" />
<meta-data android:name="aihelp_appId" android:value="xxxxxxxxxxx" />
```


#### oneStore支付系统
如果需要集成oneStore支付系统，打开安卓项目的AndroidManifest.xml。在<application>元素中添加以下 meta-data 标签，配置对应的OneStore参数。

获取参数值请咨询悠星商务人员。

```xml
<meta-data android:name="oneStore_publicKey" android:value="xxxxxxx" />
```


### 2.assets资源配置
如果需要集成亚马逊登录,需在app项目的assets目录下创建api_key.txt文件,并把参数填写保存在该文件中；

获取参数值请咨询悠星商务人员。


### 3.res资源配置

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


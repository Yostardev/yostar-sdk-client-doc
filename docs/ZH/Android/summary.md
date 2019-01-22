## 概述

AiriSDK主要用来向第三方应用程序提供方便快捷的、适合海外地区玩家使用的登陆及支付服务。本文主要描述SDK相关接口的使用方法，供使用原生Android进行开发的应用程序提供商直接接入使用。

## 阅读对象
本文档面向具有一定Android开发基础的开发与管理人员。

## 资源导入

在您的项目中，打开 your_app | Gradle Scripts | build.gradle (Project) 并添加以下存储库到 buildscript { repositories {}} 部分，以便从Maven 中央存储库下载 SDK：

```gradle
maven {
    url 'http://123.206.215.231/repository/maven-releases/'
}
```

在您的项目中，打开 your_app | Gradle Scripts | build.gradle (Module: app) 并添加以下一段执行语句至 dependencies{} 部分

```gradle
implementation 'com.airisdk.sdkcall:airisdk:2.1.0'
```

构建项目。

## 编辑您的资源和清单

### 编辑Assets资源

AiriSDK的环境资源和日志开关等参数都是由AiriSDKConf.properties文件中的参数控制，请开发者设置一下参数：

参数值请联系AiriSDK商务进行获取。

| 参数名称 | 参数说明 | 是否必须 |
| ------ | ------ | ------ |
| AIRISDK_URL | 分配的AiriSDK服务器访问地址 | 是 |
| AIRISDK_PAYSTOREID | 游戏支持的支付方式，默认为googleplay | 是 |
| AIRISDK_SHOWDEBUGLOG | AiriSDK日志打印，默认为false，不打印 | 是 |
| AIRISDK_NEWDEVICE | 是否将当前机器当作全新的机器使用，默认为false | 是 |

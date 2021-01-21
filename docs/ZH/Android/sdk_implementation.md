1:在您的项目中，打开根目录下的```build.gradle```文件并添加以下存储库到 ```allprojects { repositories {}}```以便从Maven中央存储库下载SDK:

```gradle
maven { url 'http://nexus.yo-star.com/repository/maven-releases/' }
```

2:在您的项目中，打开app目录下的```build.gradle```文件并添加以下一段执行语句至 ```dependencies{}```部分:

```gradle
implementation 'com.airisdk.sdk:network:2.1.47'
implementation 'com.twitter.sdk.android.core:twitter:2.1.47'
implementation 'com.samsung.android.sdk:iap6:2.1.47'
implementation 'com.airisdk.sdk:core:2.1.47'
```

构建项目.

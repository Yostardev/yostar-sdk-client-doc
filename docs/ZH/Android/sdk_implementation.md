在您的项目中，打开 ```your_app | Gradle Scripts | build.gradle (Project)``` 并添加以下存储库到 ```buildscript { repositories {}}```以便从Maven中央存储库下载SDK:

```gradle
maven { url 'http://nexus.yo-star.com/repository/maven-releases/' }
```

在您的项目中，打开 ```your_app | Gradle Scripts | build.gradle (Module: app)``` 并添加以下一段执行语句至 ```dependencies{}```部分:

```gradle
implementation 'com.airisdk.sdkcall:airisdk:2.3.1'
```
构建项目.

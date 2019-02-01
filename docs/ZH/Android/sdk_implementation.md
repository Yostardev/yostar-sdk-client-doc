

In order to download the SDK from central repository of Maven, you need to open ```your_app | Gradle Scripts | build.gradle (Project)``` in your project and add the following repository to ```buildscript { repositories {}}```:

```gradle
maven { url 'http://nexus.yo-star.com/repository/maven-releases/' }
```

In your project, please open ```your_app | Gradle Scripts | build.gradle (Module: app)``` and add the following line to ```dependencies{}```:

```gradle
implementation 'com.airisdk.sdkcall:airisdk:2.1.0'
```
Build project.

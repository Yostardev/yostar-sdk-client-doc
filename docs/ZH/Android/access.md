### 1. void onResume()

游戏需要在Launcher Activity和Main Activity的onResume方法中调用此接口

+ 调用API
```java
void SDKOnResume() ;
```
+ 调用实例
```java
AiriSDKInstance.getInstance().SDKOnResume()
```
### 2. void onPause()

游戏需要在Launcher Activity和Main Activity的onPause方法中调用此接口

+ 调用API
```java
void SDKOnPause() ;
```
+ 调用实例
```java
AiriSDKInstance.getInstance().SDKOnPause()
```

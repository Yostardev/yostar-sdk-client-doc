### Download resource files

[AiriSDK.unitypackage](https://sdkresources.oss-cn-shanghai.aliyuncs.com/YostarSDK/2.1.0/AiriSDK_2.1.39.unitypackage)

### Import resource files into the project

After opening the game project with Unity editor, you could import all the files needed by double-clicking the downloaded resource files. Please note the import and overwrite of AndroidManifest.xml when importing the files. If there is a Manifest file already in use, please read for more details in "Configuring Project Parameters".

#### Confirm the content of the Plugins folder and update

![logo](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/plugin210.png)

Above is everything you need to know about unitypackage. When updating files, you could delete all the files above except AndroidManifest.xml and then import the files again.

### BundleID(package name) Specification

You could get to know the package name for your application in Google Play, iTunes Store and other channels(e.g. AU) from the staff of the AiriSDK platform. You can set the corresponding package name in the Android and iOS settings in Unity's PlayerSettings.

![BundleId](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/bundleid_unity.png)



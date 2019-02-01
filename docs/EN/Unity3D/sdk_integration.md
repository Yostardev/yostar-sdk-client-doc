

### Download the SDK package

[AiriSDK.unitypackage](https://github.com/Yostardev/yostarsdk/edit/master/docs/ZH/Unity3D/)

### Import the SDK to your project

Open your project from Unity, then double click the downloaded SDK package to import it to your project.
While importing the package, beware of the file named "AndroidManifest.xml". Make sure it overwrites your current "AndroidManifest.xml" if it is from AiriSDK. However, if your current "AndroidManifest.xml" is not from AiriSDK, please discard the overwriting and go find your help in "Edit Project Setting Values"

#### Update AiriSDK

![logo](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/plugin.png)

All unitypackage contents of AiriSDK are listed in the image above. While updating the SDK, please first delete all files except "AndroidManifest.xml", then install the latest version of AiriSDK.

### BundleID 

Through the Yostar, you can acquire the BundleID(for iOS) or Package Name(for Android) of your application on Google Play, App Store and other platforms (e.g. AU). Then you need to put the BundleID and Package Name in Android/iOS section in "PlayerSettings" on your Unity.

![BundleId](https://raw.githubusercontent.com/Yostardev/yostarsdk/master/docs/_media/bundleid_unity.png)

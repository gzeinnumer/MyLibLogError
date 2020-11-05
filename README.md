<p align="center">
  <img src="https://dafunda.com/wp-content/uploads/2019/10/Aplikasi-sering-force-close-min.jpg" width="400"/>
</p>

<h1 align="center">
MyLibLogError
</h1>

<div align="center">
    <a><img src="https://img.shields.io/badge/Version-0.0.3-brightgreen.svg?style=flat"></a>
    <a><img src="https://img.shields.io/badge/ID-gzeinnumer-blue.svg?style=flat"></a>
    <a><img src="https://img.shields.io/badge/Java-Suport-green?logo=java&style=flat"></a>
    <a><img src="https://img.shields.io/badge/Koltin-Suport-green?logo=kotlin&style=flat"></a>
    <a href="https://github.com/gzeinnumer"><img src="https://img.shields.io/github/followers/gzeinnumer?label=follow&style=social"></a>
    <br>
    <p>Function to make Logs File if your app get <b>Force Close</b>, so you can track if error happen to your app in production.</p>
</div>

---
## Download
Minimum Android SDK Version 16
Add maven `jitpack.io` and `dependencies` in build.gradle (Project) :
```gradle
// build.gradle project
allprojects {
  repositories {
    google()
    jcenter()
    maven { url 'https://jitpack.io' }
  }
}

// build.gradle app/module
dependencies {
  ...
  implementation 'com.github.gzeinnumer:MyLibLogError:versi'
}
```

## Feature List
- [x] **Make Log File** like logcat in **Android Studio**.

## Tech stack and 3rd library
- File ([docs](https://developer.android.com/reference/java/io/File))
- MultiPermission ([docs](https://github.com/gzeinnumer/MultiPermition))

## Function Log Error
> Example : MBUtilsLogError.initFileLogError(valueString);

| Name               | Return    | Parameter                            | Desc    |
| ------------------ | --------- | ------------------------------------ | ------------- |
| `initFileLogError` | `void`    | `String appName, String logLocation` | Function to make Logs File if your app get `Force Close` and you can put file in external. |

---

## Use
**This library need permission. You can use your own way to get permition, or you can use my repo, here is my repository ([MultiPermission](https://github.com/gzeinnumer/MultiPermition)) (Follow Step 1 - Step 9)** :

### DEBUG.
If you find trouble and this library doesn't work, you can trace error with this log in logcat.
|![](https://github.com/gzeinnumer/MyLibLogError/blob/master/assets/debug.jpg)|
|--|

#
#### Step 1.
If you has get permission, you can run function `onSuccessCheckPermitions` inside `onRequestPermissionsResult`.  
**Remember : You only need use this function 1 TIME in your FirstActivity(on Manifest) or Activity that you use to request permission**:

```java
public class MainActivity extends AppCompatActivity {

    ...

    private void onSuccessCheckPermitions() {
        //   /storage/emulated/0/MyLibsTesting
        String appName = getResources().getString(R.string.app_name);
        //   /storage/emulated/0/MyLibsTesting/logs
        String logLocation = "/logs";
        MBUtilsLogError.initFileLogError(appName, logLocation);
    }

    ...

}
```

#
#### Step 2.
**[FullCode](https://github.com/gzeinnumer/MyLibLogError/blob/master/example/MainActivity.java)**

Preview :
|![](https://github.com/gzeinnumer/MyLibLogError/blob/master/assets/example1.jpg)|![](https://github.com/gzeinnumer/MyLibLogError/blob/master/assets/example2.jpg)|![](https://github.com/gzeinnumer/MyLibLogError/blob/master/assets/example3.jpg)|
|--|--|--|
|Request Permission|If `Force Close` happen|Folder `MyLibsTesting` created|

|![](https://github.com/gzeinnumer/MyLibLogError/blob/master/assets/example4.jpg)|![](https://github.com/gzeinnumer/MyLibLogError/blob/master/assets/example5.jpg)|
|--|--|
|Folder `Logs` created inside `MyLibsTesting`|File log created(if your app `Force Close`)|

|![](https://github.com/gzeinnumer/MyLibLogError/blob/master/assets/example6.jpg)|
|--|
|Looks like logcat on Android Studio|

---

```
Copyright 2020 M. Fadli Zein
```

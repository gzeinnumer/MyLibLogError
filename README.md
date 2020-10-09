<p align="center">
  <img src="https://github.com/gzeinnumer/MyLibUtils/blob/master/preview/bg.jpg" width="400"/>
</p>

<h1 align="center">
MyLibLogError
</h1>

<div align="center">
    <a><img src="https://img.shields.io/badge/Version-0.0.2-brightgreen.svg?style=flat"></a>
    <a><img src="https://img.shields.io/badge/ID-gzeinnumer-blue.svg?style=flat"></a>
    <a href="https://github.com/gzeinnumer"><img src="https://img.shields.io/github/followers/gzeinnumer?label=follow&style=social"></a>
    <a><img src="https://img.shields.io/badge/Java-Suport-green?logo=java&style=flat"></a>
    <a><img src="https://img.shields.io/badge/Koltin-Suport-green?logo=kotlin&style=flat"></a>
    <br>
    <p>Function to make Logs File if your app get `Force Close`, so you can track if error happen to your app in production.</p>
</div>

---

### Feature List
- [x] **Make Log File** like logcat in android Studio.

### Tech stack and 3rd library
- File ([docs](https://developer.android.com/reference/java/io/File))
- MultiPermition ([docs](https://github.com/gzeinnumer/MultiPermition))

### Function Log Error
> Example : MBUtilsLogError.initFileLogError(valueString);

| Name               | Return    | Parameter                            | Keterangan    | 
| ------------------ | --------- | ------------------------------------ | ------------- |
| `initFileLogError` | `void`    | `String appName, String logLocation` | Function to make Logs File if your app get `Force Close` and you can put file in external. |

---
## Download
Minimum Android SDK Version 16
#### Gradle
Add maven `jitpack.io` and `depedencies` in build.gradle (Project) :
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

---

## Function Log Error
**Library ini membutuhkan permition terlebih dahulu. kamu bisa pakai cara kamu, atau kamu bisa pakai cara yang selalu Zein pakai**.
\
**Contoh Multi Check Permissions. Kamu bisa lihat contohnya disini MultiPermition ([docs](https://github.com/gzeinnumer/MultiPermition)) (Ikuti Step 1 - Step 9)** :
\
**DEBUG.** Jika kamu menemukan masalah pada sistem, kamu bisa debug dengan cara sperti ini.
|![](https://github.com/gzeinnumer/MyLibLogError/blob/master/assets/debug.jpg)|
|--|

#
**Step 1.**
\
Jika sudah mengikuti cara **MultiPermition ([docs](https://github.com/gzeinnumer/MultiPermition)) (Ikuti Step 1 - Step 9)** dan `onRequestPermissionsResult` sudah mendapat permition yang dibutuhkan, maka kita akan membuat dan menjalankan function `onSuccessCheckPermitions` di dalam `onRequestPermissionsResult`. **Cukup 1 kali penggunaan saja di FirstActivity(Activity yang pertama berjalan)**:

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
**Step 2.**
\
FullCode akan tampak seperti ini ([example](https://github.com/gzeinnumer/MyLibLogError/blob/master/example/MainActivity.java))
\
Jika sukses maka akan tampil seperti ini :
|![](https://github.com/gzeinnumer/MyLibLogError/blob/master/assets/example1.jpg)|![](https://github.com/gzeinnumer/MyLibLogError/blob/master/assets/example2.jpg)|![](https://github.com/gzeinnumer/MyLibLogError/blob/master/assets/example3.jpg)|
|--|--|--|
|Request Permition|Jika ada error Force Close|Folder `MyLibsTesting` sudah terbuat|

|![](https://github.com/gzeinnumer/MyLibLogError/blob/master/assets/example4.jpg)|![](https://github.com/gzeinnumer/MyLibLogError/blob/master/assets/example5.jpg)|
|--|--|
|Folder `Logs` sudah terbuat didalam `MyLibsTesting`|File log yang terbuat(Jika Terjadi `Force Close`)|

|![](https://github.com/gzeinnumer/MyLibLogError/blob/master/assets/example6.jpg)|
|--|
|Log yang sama dengan Logcat yang ada di Android Studio|

---

```
Copyright 2020 M. Fadli Zein
```

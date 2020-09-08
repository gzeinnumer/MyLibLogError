<h1 align="center">
MyLibLogError
</h1>

<div align="center">
 <a><img src="https://img.shields.io/badge/Version-0.0.1-brightgreen.svg?style=flat"></a>
 <a><img src="https://img.shields.io/badge/ID-gzeinnumer-blue.svg?style=flat"></a>
 <a href="https://github.com/gzeinnumer"><img src="https://img.shields.io/github/followers/gzeinnumer?label=follow&style=social"></a>
 <p>Function untuk membuat log file jika ada error, jadi kamu bisa dengan mudah cari errorya dimana jika user mengalami error, dokumen ini dibuat berdasarkan pengalaman saya, kasih masukan kalau ada yang kurang. terimakasih karna sudah berkunjung</p>
</div>

---

### Feature List
- [x] Menyimpan error report ke file txt

### Tech stack and 3rd library
- File ([docs](https://developer.android.com/reference/java/io/File))
- MultiPermition ([docs](https://github.com/gzeinnumer/MultiPermition))

### Function Log Error
> Example : MyBaseUtilsLogError.initFileLogError(valueString);

| Name               | Return    | Parameter                            | Keterangan    | 
| ------------------ | --------- | ------------------------------------ | ------------- |
| `initFileLogError` | `void`    | `String appName, String logLocation` | Function membuat file yang akan menyimpan log error jika ada Force Close ke lokasi yang sudah kamu set |

---

<p align="end"><b><i>Download</i></b></p>

## Download

Minimum Android SDK Version 16

#### Gradle
**Step 1.** tambahkan maven jitpack.io ke build.gradle (Project) :
```gradle
allprojects {
  repositories {
    google()
    jcenter()
    maven { url 'https://jitpack.io' }
  }
}
```

**Step 2.** tambahkan depedensi ke build.gradle (Module) :
```gradle
dependencies {
  implementation 'com.github.gzeinnumer:MyLibLogError:versi'
}
```

---

## Function Log Error
Librari ini membutuhkan permition terlbih dahulu. kamu bisa pakai cara kamu, atau kamu bisa pakai cara yang selalu saya pakai.
**Contoh Multi Check Permissions.** Kamu bisa lihat contohnya disini MultiPermition ([docs](https://github.com/gzeinnumer/MultiPermition)) :

\
**DEBUG.** Jika kamu menemukan masalah pada sistem, kamu bisa debug dengan cara sperti ini.
|![](https://github.com/gzeinnumer/MyLibLogError/blob/master/assets/debug.jpg)|
|--|

#
**Step 1.**
\
Jika `onRequestPermissionsResult` sudah mendapat permition yang dibutuhkan, maka kita akan membuat dan menjalankan function `onSuccessCheckPermitions`. **Cukup 1 kali penggunaan saja di FirstActivity(Acctivity yang pertama berjalan)**:

```java
public class MainActivity extends AppCompatActivity {

    //<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    //<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
    
    //berikan izin diatas agar function bisa berjalan, pastikan kamu menggunakan 
    //`onRequestPermissionsResult`, jika sudah diberikan izin yang diperlukan 
    //maka panggil function `onSuccessCheckPermitions` didalam `onRequestPermissionsResult` 
    //untuk bagian diatas ini kamu bisa ukuti cara yang sudah saya buat di repo saya yang lain. 
    // cari `Contoh Multi Check Permition` diatas : https://github.com/gzeinnumer/MultiPermition
    ...

    private void onSuccessCheckPermitions() {
        //   /storage/emulated/0/MyLibsTesting
        String appName = getResources().getString(R.string.app_name);
        //   /storage/emulated/0/MyLibsTesting/logs
        String logLocation = "/logs";
        MyBaseUtilsLogError.initFileLogError(appName, logLocation);
    }

}
```

#
**Step 2.**
\
Jika sukses maka akan tampil seperti ini :
|![](https://github.com/gzeinnumer/MyLibLogError/blob/master/assets/example1.jpg)|![](https://github.com/gzeinnumer/MyLibLogError/blob/master/assets/example2.jpg)|![](https://github.com/gzeinnumer/MyLibLogError/blob/master/assets/example3.jpg)|
|--|--|--|
|Request Permition|Jika ada error Force Close|Folder `MyLibsTesting` sudah terbuat|

|![](https://github.com/gzeinnumer/MyLibLogError/blob/master/assets/example4.jpg)|![](https://github.com/gzeinnumer/MyLibLogError/blob/master/assets/example5.jpg)|
|--|--|
|Folder `Logs` sudah terbuat didalam `MyLibsTesting`|File log yang terbuat|

|![](https://github.com/gzeinnumer/MyLibLogError/blob/master/assets/example6.jpg)|
|--|
|Log yang sama dengan Logcat yang ada di Android Studio|

---

```
Copyright 2020 M. Fadli Zein
```
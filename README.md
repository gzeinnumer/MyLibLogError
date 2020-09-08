<h1 align="center">
MyLibLogError
</h1>

<p align="center">
<img src="https://i.ibb.co/YdvBMMG/hiya.gif"/>
</p>

<div align="center">
 <a><img src="https://img.shields.io/badge/Version-0.0.1-brightgreen.svg?style=flat"></a>
 <a><img src="https://img.shields.io/badge/ID-gzeinnumer-blue.svg?style=flat"></a>
 <a href="https://github.com/gzeinnumer"><img src="https://img.shields.io/github/followers/gzeinnumer?label=follow&style=social"></a>
 <p>Function untuk membuat log file jika ada error, jadi kamu bisa dengan mudah cari errorya dimana jika user mengalami error, dokumen ini dibuat berdasarkan pengalaman saya, kasih masukan kalau ada yang kurang. terimakasih karna sudah berkunjung</p>
</div>

---

### Feature List
- [x] Ada
- [ ] Tidak ada

### Tech stack and 3rd library
- File ([docs](https://developer.android.com/reference/java/io/File))

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

## Function Global Directory
**Contoh Multi Check Permissions.** Request permition secara bersamaan, Zein sarankan untuk requestnya dijalankan di activity yang pertama aktif, disini Zein masukan ke MainActivity :

**Manifest.** Tambahkan permition ke file manifest. Zein sarankan untuk menambahkan requestLegacyExternalStorage=true jika android kamu sudah android 10.

```xml
<manifest >

    <uses-permission
        android:name="android.permission.READ_LOGS"
        tools:ignore="ProtectedPermissions" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />

    <application
        android:requestLegacyExternalStorage="true">

    </application>

</manifest>
```

\
**DEBUG.** Jika kamu menemukan masalah pada sistem, kamu bisa debug dengan cara sperti ini.
|![](https://github.com/gzeinnumer/MyLibDirectory/blob/master/assets/debug.jpg)|
|--|


#
**Step 1.**
 
\
Tambahkan array permition yang dibutuhkan : \
**First Activity.** letakan permition pada saat awal activity dimulai, disini Zein meletakannya di `MainActivity`.

```java
public class MainActivity extends AppCompatActivity {

    String[] permissions = new String[]{
        Manifest.permission.READ_EXTERNAL_STORAGE,
        Manifest.permission.WRITE_EXTERNAL_STORAGE
    };
    
    ...

}
```

#
**Step 2.** 
\
Tambahkan function untuk mengecek permition apps apakah semua permition sudah diberikan izin, Jika belum diberikan izin maka akan keluar popup. Silahkan berikan izin dengan menekan `allow` :

```java
public class MainActivity extends AppCompatActivity {
    
    ...

    int MULTIPLE_PERMISSIONS = 1;
    private boolean checkPermissions() {
        int result;
        List<String> listPermissionsNeeded = new ArrayList<>();

        for (String p : permissions) {
            result = ContextCompat.checkSelfPermission(getApplicationContext(), p);
            if (result != PackageManager.PERMISSION_GRANTED) {
                listPermissionsNeeded.add(p);
            }
        }
        if (!listPermissionsNeeded.isEmpty()) {
            ActivityCompat.requestPermissions(this, listPermissionsNeeded.toArray(new String[0]), MULTIPLE_PERMISSIONS);
            return false;
        }
        return true;
    }
    
    ...

}
```

#
**Step 3.**
\
Jika semua akses sudah diberikan maka aplikasi dapat menjalankan proses untuk membuat directory :

```java
public class MainActivity extends AppCompatActivity {
    
    ...

    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
        if (requestCode == MULTIPLE_PERMISSIONS) {
            if (grantResults.length > 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED) {

                //Do Someting ...
                //aksi setelah semua permition diberikan

            } else {
                StringBuilder perStr = new StringBuilder();
                for (String per : permissions) {
                    perStr.append("\n").append(per);
                }
            }
        }
    }
    
    ...

}
```

#
**Step 4.** 
\
Buat dan panggil function `onSuccessCheckPermitions` untuk membuat folder :

```java
public class MainActivity extends AppCompatActivity {
    
    ...

    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
        if (requestCode == MULTIPLE_PERMISSIONS) {
            if (grantResults.length > 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                //tambahkan ini
                onSuccessCheckPermitions();
            } else {
                StringBuilder perStr = new StringBuilder();
                for (String per : permissions) {
                    perStr.append("\n").append(per);
                }
            }
        }
    }
    
    ...

}
```

#
**Step 5.** Create Folder
\
Jika `onRequestPermissionsResult` sudah mendapat permition yang dibutuhkan, maka kita akan membuat dan menjalankan function `onSuccessCheckPermitions`:

```java
public class MainActivity extends AppCompatActivity {
    
    ...

    private void onSuccessCheckPermitions() {
        String appName = getResources().getString(R.string.app_name);
        String logLocation = "/logs";
        MyBaseUtilsLogError.initFileLogError(appName, logLocation);
    }

}
```

**notes.** 
  - `appName` adalah nama folder  yang akan dibuat didalam penyimpanan kamu.
  - `logLocation` adalah nama folder yang akan dibuat didalam `appName` penyimpanan kamu untuk menyimpan file log yang akan dibuat.
  
#
**Step 6.**
\
Tambahkan function `checkPermissions` di `onCreate` agar setiap activity dijalankan maka akan selalu mengecek apakah izin sudah diberikan :

```java
public class MainActivity extends AppCompatActivity {

    ...

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        
        ...

        if (checkPermissions()) {
            Toast.makeText(this, "Izin sudah diberikan", Toast.LENGTH_SHORT).show();
            onSuccessCheckPermitions();
        } else {
            Toast.makeText(this, "Berikan izin untuk membuat folder terlebih dahulu", Toast.LENGTH_SHORT).show();
        }
    }
    
    ...

}
```

#
**Step 7.**
\
Fullcode akan tampak seperti ini :

```java
public class MainActivity extends AppCompatActivity {

    String[] permissions = new String[]{
        Manifest.permission.READ_EXTERNAL_STORAGE,
        Manifest.permission.WRITE_EXTERNAL_STORAGE
    };

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        if (checkPermissions()) {
            Toast.makeText(this, "Izin sudah diberikan", Toast.LENGTH_SHORT).show();
            onSuccessCheckPermitions();
        } else {
            Toast.makeText(this, "Berikan izin untuk membuat folder terlebih dahulu", Toast.LENGTH_SHORT).show();
        }
    }

    int MULTIPLE_PERMISSIONS = 1;
    private boolean checkPermissions() {
        int result;
        List<String> listPermissionsNeeded = new ArrayList<>();

        for (String p : permissions) {
            result = ContextCompat.checkSelfPermission(getApplicationContext(), p);
            if (result != PackageManager.PERMISSION_GRANTED) {
                listPermissionsNeeded.add(p);
            }
        }
        if (!listPermissionsNeeded.isEmpty()) {
            ActivityCompat.requestPermissions(this, listPermissionsNeeded.toArray(new String[0]), MULTIPLE_PERMISSIONS);
            return false;
        }
        return true;
    }

    @Override
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
        if (requestCode == MULTIPLE_PERMISSIONS) {
            if (grantResults.length > 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                onSuccessCheckPermitions();
            } else {
                StringBuilder perStr = new StringBuilder();
                for (String per : permissions) {
                    perStr.append("\n").append(per);
                }
            }
        }
    }

    private void onSuccessCheckPermitions() {
        String appName = getResources().getString(R.string.app_name);
        String logLocation = "/logs";
        MyBaseUtilsLogError.initFileLogError(appName, logLocation);
    }
}
```

#
**Step 8.**
\
Jika sukses maka akan tampil seperti ini :
|![](https://github.com/gzeinnumer/MyLibDirectory/blob/master/assets/example1.jpg)|![](https://github.com/gzeinnumer/MyLibDirectory/blob/master/assets/example2.jpg)|![](https://github.com/gzeinnumer/MyLibDirectory/blob/master/assets/example3.jpg)|![](https://github.com/gzeinnumer/MyLibDirectory/blob/master/assets/example4.jpg)|
|--|--|--|--|
|Request Permition |Folder MyLibsTesting sudah dibuat|`folder1` dan `folder2` sudah terbuat|`folder1_1` yang berada didalam `folder1` sudah dibuat|

---

```
Copyright 2020 M. Fadli Zein
```
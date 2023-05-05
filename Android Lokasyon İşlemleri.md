# Android Lokasyon işlemleri
![Konum](https://user-images.githubusercontent.com/101557027/236537218-397a8299-5674-455c-8087-49f683d633b9.gif)
* MainActivity
```
package com.example.konumkullanimi;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;

import android.annotation.SuppressLint;
import android.content.pm.PackageManager;
import android.location.Location;
import android.os.Bundle;
import android.widget.Toast;
import android.Manifest;

import com.example.konumkullanimi.databinding.ActivityMainBinding;
import com.google.android.gms.location.FusedLocationProviderClient;
import com.google.android.gms.location.LocationServices;
import com.google.android.gms.tasks.Task;

public class MainActivity extends AppCompatActivity {
    private ActivityMainBinding tasarim;
    private int izinKontrol = 0;
    private FusedLocationProviderClient flpc;
    private Task<Location> locationTask;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        tasarim = ActivityMainBinding.inflate(getLayoutInflater());
        setContentView(tasarim.getRoot());

        flpc = LocationServices.getFusedLocationProviderClient(this);

        tasarim.buttonKonumAl.setOnClickListener(view -> {
            izinKontrol = ContextCompat.checkSelfPermission(this,Manifest.permission.ACCESS_FINE_LOCATION);

            if(izinKontrol != PackageManager.PERMISSION_GRANTED){
                ActivityCompat.requestPermissions(this,new String[]{Manifest.permission.ACCESS_FINE_LOCATION},100);
            }else {// izin onaylanmışsa
                locationTask = flpc.getLastLocation();
                konumBilgisiAl();
            }
        });
    }

    public void konumBilgisiAl(){
        locationTask.addOnSuccessListener(location -> {

           if (location != null) {
               tasarim.textViewEnlem.setText("Enlem : "+location.getLatitude());
               tasarim.textViewBoylam.setText("Boylam : "+location.getLongitude());
           }else {
               tasarim.textViewEnlem.setText("Enlem : Alınamadı");
               tasarim.textViewBoylam.setText("Boylam : Alınamadı");
           }
        });
    }

    @Override
    @SuppressLint("MissingSuperCall")
    public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {

        izinKontrol = ContextCompat.checkSelfPermission(this,Manifest.permission.ACCESS_FINE_LOCATION);

        if (requestCode == 100) {
            if (grantResults.length>0 && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
                Toast.makeText(getApplicationContext(),"izin kabul edildi",Toast.LENGTH_SHORT).show();
                locationTask = flpc.getLastLocation();
                konumBilgisiAl();
            }else {
                Toast.makeText(getApplicationContext(),"izin reddedildi",Toast.LENGTH_SHORT).show();
            }
        }
    }
}
```
* AndroidManifest.xml
```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:supportsRtl="true"
        android:theme="@style/Theme.KonumKullanimi"
        tools:targetApi="31">
        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```
* build.gradle
```
plugins {
    id 'com.android.application'
}
android {
    namespace 'com.example.konumkullanimi'
    compileSdk 33

    buildFeatures {
        viewBinding = true
    }

    defaultConfig {
        applicationId "com.example.konumkullanimi"
        minSdk 24
        targetSdk 33
        versionCode 1
        versionName "1.0"

        testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
    }

    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
        }
    }
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
}
dependencies {

    implementation 'androidx.appcompat:appcompat:1.6.1'
    implementation 'com.google.android.material:material:1.8.0'
    implementation 'androidx.constraintlayout:constraintlayout:2.1.4'
    testImplementation 'junit:junit:4.13.2'
    androidTestImplementation 'androidx.test.ext:junit:1.1.5'
    androidTestImplementation 'androidx.test.espresso:espresso-core:3.5.1'

    implementation 'com.google.android.gms:play-services-location:21.0.1'
}
```
* activity_main.xml
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/textViewEnlem"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Enlem : Alınamadı"
        android:textSize="34sp"
        app:layout_constraintBottom_toTopOf="@+id/textViewBoylam"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <TextView
        android:id="@+id/textViewBoylam"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Boylam : Alınamadı"
        android:textSize="34sp"
        app:layout_constraintBottom_toTopOf="@+id/buttonKonumAl"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textViewEnlem" />

    <Button
        android:id="@+id/buttonKonumAl"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Konum Al"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textViewBoylam" />
</androidx.constraintlayout.widget.ConstraintLayout>
```

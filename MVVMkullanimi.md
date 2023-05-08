# MVVM Kullanımı
![MVVM uygulama](https://user-images.githubusercontent.com/101557027/236748557-f4cda61e-11f9-44a7-991d-e5b6334e89d3.gif)
![MVVM MODEL VİEW VİEWMODEL MİMARİ SÜRECİ](https://user-images.githubusercontent.com/101557027/236748711-2315bf33-c383-4ebc-9361-1ff6326fe434.png)
![DataBinding](https://user-images.githubusercontent.com/101557027/236748910-14796309-06c2-493b-85c4-2ca6ded59019.png)
![DataBinding ile Tasarıma ErişimActivity](https://user-images.githubusercontent.com/101557027/236749056-960695e8-92b9-4dfe-8416-0bf8401df669.png)
![DataBinding ile Tasarıma Erişim(Fragment) ](https://user-images.githubusercontent.com/101557027/236749172-9994b521-2a14-4637-9eab-fb6dbc70984b.png)
![Event Handle1](https://user-images.githubusercontent.com/101557027/236749261-41c1b41e-cae7-44cb-9478-b771e67bd6cf.png)
![a](https://user-images.githubusercontent.com/101557027/236749794-662ab161-cfbf-453c-b921-82527284dfed.png)
![Tasarım Alanında Parantez icine Kodlama Yapma1](https://user-images.githubusercontent.com/101557027/236749893-44103327-9d34-491e-95a7-04595c9d34ca.png)
![ViewModel1](https://user-images.githubusercontent.com/101557027/236750045-0faed65c-9274-48f1-9568-f0c844f37594.png)
![ViewModelFragment İçinde Kullanımı1](https://user-images.githubusercontent.com/101557027/236750191-7d7cd5d9-b806-4426-8f68-a072f64fc2f8.png)
![LİveData1](https://user-images.githubusercontent.com/101557027/236750329-625de8c0-06ae-49e2-91e2-df4a5cb8ea46.png)
* MainActivity
```
package com.example.mvvmkullanimi;

import androidx.appcompat.app.AppCompatActivity;
import androidx.databinding.DataBindingUtil;
import androidx.lifecycle.Observer;
import androidx.lifecycle.ViewModelProvider;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;

import com.example.mvvmkullanimi.databinding.ActivityMainBinding;

public class MainActivity extends AppCompatActivity {
    private ActivityMainBinding tasarim;
    private MainActivityViewModel viewModel;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        tasarim = DataBindingUtil.setContentView(this,R.layout.activity_main);
        viewModel = new ViewModelProvider(this).get(MainActivityViewModel.class);
        tasarim.setMainACtivityNesnesi(this);

        viewModel.getSonuc().observe(this, new Observer<String>() {
            @Override
            public void onChanged(String s) {
                tasarim.setHesaplamaSonucu(s);
            }
        });

    }

    public void buttonToplamaTikla(String alinanSayi1,String alinanSayi2){
        viewModel.toplamaYap(alinanSayi1,alinanSayi2);
    }

    public void buttonCarpmaTikla(String alinanSayi1,String alinanSayi2) {
        viewModel.CarpmaYap(alinanSayi1,alinanSayi2);
    }
}
```
* MatematikRepository.java
```
package com.example.mvvmkullanimi;

import androidx.lifecycle.MutableLiveData;

public class MatematikRepository {

    private MutableLiveData<String> matematikselSonuc;

    public MatematikRepository() {
        matematikselSonuc = new MutableLiveData<String>("0");
    }

    public MutableLiveData<String> getMatematikselSonuc() {
        return matematikselSonuc;
    }

    public void topla(String alinanSayi1,String alinanSayi2){
        int sayi1 = Integer.parseInt(alinanSayi1);
        int sayi2 = Integer.parseInt(alinanSayi2);
        int Toplam = sayi1+sayi2;
        matematikselSonuc.setValue(String.valueOf(Toplam));
    }

    public void carp(String alinanSayi1,String alinanSayi2) {
        int sayi1 = Integer.parseInt(alinanSayi1);
        int sayi2 = Integer.parseInt(alinanSayi2);
        int Carpma = sayi1*sayi2;
        matematikselSonuc.setValue(String.valueOf(Carpma));
    }
}
```
* MainActivityViewModel.java
```
package com.example.mvvmkullanimi;

import androidx.annotation.NonNull;
import androidx.lifecycle.MutableLiveData;
import androidx.lifecycle.ViewModel;

import java.io.Closeable;

public class MainActivityViewModel extends ViewModel {
    private MutableLiveData<String> Sonuc;
    private MatematikRepository mrepo = new MatematikRepository();

    public MainActivityViewModel() {
        Sonuc = mrepo.getMatematikselSonuc();
    }

    public MutableLiveData<String> getSonuc() {
        return Sonuc;
    }

    public void toplamaYap(String alinanSayi1,String alinanSayi2){
        mrepo.topla(alinanSayi1,alinanSayi2);
    }

    public void CarpmaYap(String alinanSayi1,String alinanSayi2) {
        mrepo.carp(alinanSayi1,alinanSayi2);
    }
}
```
* activity_main.xml
```
<?xml version="1.0" encoding="utf-8"?>
<layout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools">

    <data>
        <variable
            name="mainACtivityNesnesi"
            type="com.example.mvvmkullanimi.MainActivity" />
        <variable
            name="hesaplamaSonucu"
            type="String" />
        <import type="android.view.View"/>
    </data>

<androidx.constraintlayout.widget.ConstraintLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:id="@+id/textViewSonuc"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="32dp"
        android:text="@{hesaplamaSonucu}"
        android:textColor="@{Integer.parseInt(hesaplamaSonucu) > 10 ? @color/purple_700 : @color/teal_700}"
        android:visibility="@{Integer.parseInt(hesaplamaSonucu) > 20 ? View.INVISIBLE : View.VISIBLE}"
        android:textSize="24sp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <EditText
        android:id="@+id/editTextSayi2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="32dp"
        android:ems="10"
        android:hint="Sayı 2"
        android:inputType="textPersonName"
        android:textSize="20sp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/editTextSayi1" />

    <EditText
        android:id="@+id/editTextSayi1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="32dp"
        android:ems="10"
        android:hint="Sayı 1"
        android:inputType="textPersonName"
        android:textSize="20sp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textViewSonuc" />

    <Button
        android:id="@+id/buttonToplama"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="32dp"
        android:text="Toplama"
        android:onClick="@{() -> mainACtivityNesnesi.buttonToplamaTikla(editTextSayi1.getText().toString(),editTextSayi2.getText().toString())}"
        app:layout_constraintEnd_toStartOf="@+id/buttonCarpma"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/editTextSayi2" />

    <Button
        android:id="@+id/buttonCarpma"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="32dp"
        android:text="Çarpma"
        android:onClick="@{() -> mainACtivityNesnesi.buttonCarpmaTikla(editTextSayi1.getText().toString(),editTextSayi2.getText().toString())}"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toEndOf="@+id/buttonToplama"
        app:layout_constraintTop_toBottomOf="@+id/editTextSayi2" />
</androidx.constraintlayout.widget.ConstraintLayout>
</layout>
```
* build.gradle
```
plugins {
    id 'com.android.application'
}

android {
    namespace 'com.example.mvvmkullanimi'
    compileSdk 33

    buildFeatures {
        dataBinding true
    }

    defaultConfig {
        applicationId "com.example.mvvmkullanimi"
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
    def lifecycle_version = "2.5.1"
    // ViewModel
    implementation "androidx.lifecycle:lifecycle-viewmodel:$lifecycle_version"
    // LiveData
    implementation "androidx.lifecycle:lifecycle-livedata:$lifecycle_version"
}
```

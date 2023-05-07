# Room Kütüphanesi
![Room Kutuphanesi temel yapıları](https://user-images.githubusercontent.com/101557027/236676844-c7297501-e42b-4871-b8b8-97654dafae01.png)
![Veritabanı Asset dosyası aktarma](https://user-images.githubusercontent.com/101557027/236676870-133fea17-59e2-4a58-bbd2-33068f34808d.png)
-----------
* MainActivity
```
package com.example.roomkullanimi;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.util.Log;

import java.util.List;

import io.reactivex.CompletableObserver;
import io.reactivex.SingleObserver;
import io.reactivex.android.schedulers.AndroidSchedulers;
import io.reactivex.disposables.Disposable;
import io.reactivex.schedulers.Schedulers;

public class MainActivity extends AppCompatActivity {
    private Veritabani vt;
    private KisilerDao kdao;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        vt = Veritabani.veritabaniErisim(this);
        kdao = vt.getKisilerDao();

        //kisileriEkle();
        //kisileriGuncelle();
        //kisileriSil();
        //kisileriYukle();
        //rastgele();
        //kisileriAra();
        //kisiGetir();
        kisiKontrol();
    }

    public void kisileriYukle() {
        kdao.tumKisiler().subscribeOn(Schedulers.io())
                .observeOn(AndroidSchedulers.mainThread())
                .subscribe(new SingleObserver<List<Kisiler>>() {
            @Override
            public void onSubscribe(Disposable d) {
            }
            @Override
            public void onSuccess(List<Kisiler> kisilers) {
                for(Kisiler k:kisilers) {
                    Log.e("Kişi id",String.valueOf(k.getKisi_id()));
                    Log.e("Kişi ad",k.getKisi_ad());
                    Log.e("Kişi yas",String.valueOf(k.getKisi_yas()));
                }
            }
            @Override
            public void onError(Throwable e) {
            }
        });
    }

    public void kisileriEkle() {
        Kisiler yeniKisi = new Kisiler(0,"Fatih",31);

        kdao.kisiEkle(yeniKisi).subscribeOn(Schedulers.io())
                .observeOn(AndroidSchedulers.mainThread())
                .subscribe(new CompletableObserver() {
                    @Override
                    public void onSubscribe(Disposable d) {
                    }
                    @Override
                    public void onComplete() {
                    }
                    @Override
                    public void onError(Throwable e) {
                    }
                });
    }

    public void kisileriGuncelle() {
        Kisiler guncellenenKisi = new Kisiler(1,"Yeni Zeynep",22);

        kdao.kisiGuncelle(guncellenenKisi).subscribeOn(Schedulers.io())
                .observeOn(AndroidSchedulers.mainThread())
                .subscribe(new CompletableObserver() {
                    @Override
                    public void onSubscribe(Disposable d) {
                    }
                    @Override
                    public void onComplete() {
                    }
                    @Override
                    public void onError(Throwable e) {
                    }
                });
    }

    public void kisileriSil() {
        Kisiler silinenKisi = new Kisiler(1,"Yeni Zeynep",22);

        kdao.kisiSil(silinenKisi).subscribeOn(Schedulers.io())
                .observeOn(AndroidSchedulers.mainThread())
                .subscribe(new CompletableObserver() {
                    @Override
                    public void onSubscribe(Disposable d) {
                    }
                    @Override
                    public void onComplete() {
                    }
                    @Override
                    public void onError(Throwable e) {
                    }
                });
    }

    public void rastgele() {
        kdao.rastgeleKisiGetir().subscribeOn(Schedulers.io())
                .observeOn(AndroidSchedulers.mainThread())
                .subscribe(new SingleObserver<List<Kisiler>>() {
                    @Override
                    public void onSubscribe(Disposable d) {
                    }
                    @Override
                    public void onSuccess(List<Kisiler> kisilers) {
                        for(Kisiler k:kisilers) {
                            Log.e("Kişi id",String.valueOf(k.getKisi_id()));
                            Log.e("Kişi ad",k.getKisi_ad());
                            Log.e("Kişi yas",String.valueOf(k.getKisi_yas()));
                        }
                    }
                    @Override
                    public void onError(Throwable e) {
                    }
                });
    }

    public void kisileriAra() {
        kdao.kisiAra("f").subscribeOn(Schedulers.io())
                .observeOn(AndroidSchedulers.mainThread())
                .subscribe(new SingleObserver<List<Kisiler>>() {
                    @Override
                    public void onSubscribe(Disposable d) {
                    }
                    @Override
                    public void onSuccess(List<Kisiler> kisilers) {
                        for(Kisiler k:kisilers) {
                            Log.e("Kişi id",String.valueOf(k.getKisi_id()));
                            Log.e("Kişi ad",k.getKisi_ad());
                            Log.e("Kişi yas",String.valueOf(k.getKisi_yas()));
                        }
                    }
                    @Override
                    public void onError(Throwable e) {
                    }
                });
    }

    public void kisiGetir() {
        kdao.kisiGetir(3).subscribeOn(Schedulers.io())
                .observeOn(AndroidSchedulers.mainThread())
                .subscribe(new SingleObserver<Kisiler>() {
                    @Override
                    public void onSubscribe(Disposable d) {
                    }
                    @Override
                    public void onSuccess(Kisiler kisiler) {
                        Log.e("Kişi id",String.valueOf(kisiler.getKisi_id()));
                        Log.e("Kişi ad",kisiler.getKisi_ad());
                        Log.e("Kişi yas",String.valueOf(kisiler.getKisi_yas()));
                    }
                    @Override
                    public void onError(Throwable e) {
                    }
                });
    }

    public void kisiKontrol() {
        kdao.kayitKontrol("Ece").subscribeOn(Schedulers.io())
                .observeOn(AndroidSchedulers.mainThread())
                .subscribe(new SingleObserver<Integer>() {
                    @Override
                    public void onSubscribe(Disposable d) {
                    }
                    @Override
                    public void onSuccess(Integer integer) {
                        Log.e("Kişi kayıt kontrol",String.valueOf(integer));
                    }
                    @Override
                    public void onError(Throwable e) {
                    }
                });

    }
}
```
* Kisiler.java
```
package com.example.roomkullanimi;

import androidx.annotation.NonNull;
import androidx.room.ColumnInfo;
import androidx.room.Entity;
import androidx.room.PrimaryKey;

@Entity(tableName = "kisiler")
public class Kisiler {
    @PrimaryKey(autoGenerate = true)
    @ColumnInfo(name = "kisi_id")
    @NonNull
    private int kisi_id;
    @ColumnInfo(name = "kisi_ad")
    @NonNull
    private String kisi_ad;
    @ColumnInfo(name = "kisi_yas")
    @NonNull
    private int kisi_yas;

    public Kisiler() {
    }

    public Kisiler(int kisi_id, @NonNull String kisi_ad, int kisi_yas) {
        this.kisi_id = kisi_id;
        this.kisi_ad = kisi_ad;
        this.kisi_yas = kisi_yas;
    }

    public int getKisi_id() {
        return kisi_id;
    }

    public void setKisi_id(int kisi_id) {
        this.kisi_id = kisi_id;
    }

    @NonNull
    public String getKisi_ad() {
        return kisi_ad;
    }

    public void setKisi_ad(@NonNull String kisi_ad) {
        this.kisi_ad = kisi_ad;
    }

    public int getKisi_yas() {
        return kisi_yas;
    }

    public void setKisi_yas(int kisi_yas) {
        this.kisi_yas = kisi_yas;
    }
}
```
* KisilerDaointerface.java
```
package com.example.roomkullanimi;

import androidx.room.Dao;
import androidx.room.Delete;
import androidx.room.Insert;
import androidx.room.Query;
import androidx.room.Update;

import java.util.List;

import io.reactivex.Completable;
import io.reactivex.Single;

@Dao
public interface KisilerDao {
    @Query("SELECT * FROM kisiler")
    Single<List<Kisiler>> tumKisiler();

    @Insert
    Completable kisiEkle(Kisiler kisi);

    @Update
    Completable kisiGuncelle(Kisiler kisi);

    @Delete
    Completable kisiSil(Kisiler kisi);

    @Query("SELECT * FROM kisiler ORDER BY RANDOM() LIMIT 1")
    Single<List<Kisiler>> rastgeleKisiGetir();

    @Query("SELECT * FROM kisiler WHERE kisi_ad like '%' || :aramaKelimesi || '%'")
    Single<List<Kisiler>> kisiAra(String aramaKelimesi);

    @Query("SELECT * FROM kisiler WHERE kisi_id=:kisi_id")
    Single<Kisiler> kisiGetir(int kisi_id);

    @Query("SELECT count(*) FROM kisiler WHERE kisi_ad=:kisi_ad")
    Single<Integer> kayitKontrol(String kisi_ad);
}
```
* Veritabani.java
```
package com.example.roomkullanimi;

import android.content.Context;

import androidx.room.Database;
import androidx.room.Room;
import androidx.room.RoomDatabase;

@Database(entities = {Kisiler.class},version = 1)
public abstract class Veritabani extends RoomDatabase {
    public abstract KisilerDao getKisilerDao();

    private static Veritabani INSTANCE;

    public static Veritabani veritabaniErisim(Context context) {
        if(INSTANCE == null) {
            synchronized (Veritabani.class) {
                INSTANCE = Room.databaseBuilder(context.getApplicationContext()
                        ,Veritabani.class
                        ,"REHBER.sqlite")
                        .createFromAsset("REHBER.sqlite").build();
            }
        }
        return INSTANCE;
    }
}
```
* REHBER.sqlite
```
CREATE TABLE "kisiler" (
	"kisi_id"	INTEGER NOT NULL,
	"kisi_ad"	TEXT NOT NULL,
	"kisi_yas"	INTEGER NOT NULL,
	PRIMARY KEY("kisi_id" AUTOINCREMENT)
);
```
* build.gradle
```
plugins {
    id 'com.android.application'
}

android {
    namespace 'com.example.roomkullanimi'
    compileSdk 33

    defaultConfig {
        applicationId "com.example.roomkullanimi"
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
    implementation 'com.google.android.material:material:1.9.0'
    implementation 'androidx.constraintlayout:constraintlayout:2.1.4'
    testImplementation 'junit:junit:4.13.2'
    androidTestImplementation 'androidx.test.ext:junit:1.1.5'
    androidTestImplementation 'androidx.test.espresso:espresso-core:3.5.1'
    def room_version = "2.5.1"

    implementation "androidx.room:room-runtime:$room_version"
    annotationProcessor "androidx.room:room-compiler:$room_version"
    // optional - RxJava2 support for Room
    implementation "androidx.room:room-rxjava2:$room_version"
    implementation 'io.reactivex.rxjava2:rxandroid:2.0.1'
}
```

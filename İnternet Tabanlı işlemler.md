# Volley Kütüphanesi ile Select Update Insert Delete işlemleri
* MainActivity
```
package com.example.volleycalismasi;

import androidx.annotation.Nullable;
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.util.Log;

import com.android.volley.AuthFailureError;
import com.android.volley.Request;
import com.android.volley.Response;
import com.android.volley.VolleyError;
import com.android.volley.toolbox.StringRequest;
import com.android.volley.toolbox.Volley;

import org.json.JSONArray;
import org.json.JSONException;
import org.json.JSONObject;

import java.util.HashMap;
import java.util.Map;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        //kisiEkle();
        //kisiGuncelle();
        //kisiSil();
        //tumKisiler();
        kisiArama();
    }

    public void kisiEkle() {
        String url = "https://snowpiercer.store/bayrakquiz/insert_kisiler.php";

        StringRequest istek = new StringRequest(Request.Method.POST, url, new Response.Listener<String>() {
            @Override
            public void onResponse(String response) {
                Log.e("Cevap", response);
            }
        }, new Response.ErrorListener() {
            @Override
            public void onErrorResponse(VolleyError error) {

            }
        }){
            @Nullable
            @Override
            protected Map<String, String> getParams() throws AuthFailureError {

                Map<String,String> params = new HashMap<>();

                    params.put("kisi_ad","Mehmet");
                    params.put("kisi_tel","0523425325");

                return params;
            }
        };

        Volley.newRequestQueue(this).add(istek);
    }

    public void kisiGuncelle() {
        String url = "https://snowpiercer.store/bayrakquiz/update_kisiler.php";

        StringRequest istek = new StringRequest(Request.Method.POST, url, new Response.Listener<String>() {
            @Override
            public void onResponse(String response) {
                Log.e("Cevap", response);
            }
        }, new Response.ErrorListener() {
            @Override
            public void onErrorResponse(VolleyError error) {

            }
        }){
            @Nullable
            @Override
            protected Map<String, String> getParams() throws AuthFailureError {

                Map<String,String> params = new HashMap<>();

                params.put("kisi_id","2");
                params.put("kisi_ad","Mehmetxx");
                params.put("kisi_tel","0523425325qq");

                return params;
            }
        };

        Volley.newRequestQueue(this).add(istek);
    }

    public void kisiSil() {
        String url = "https://snowpiercer.store/bayrakquiz/delete_kisiler.php";

        StringRequest istek = new StringRequest(Request.Method.POST, url, new Response.Listener<String>() {
            @Override
            public void onResponse(String response) {
                Log.e("Cevap", response);
            }
        }, new Response.ErrorListener() {
            @Override
            public void onErrorResponse(VolleyError error) {

            }
        }){
            @Nullable
            @Override
            protected Map<String, String> getParams() throws AuthFailureError {

                Map<String,String> params = new HashMap<>();

                params.put("kisi_id","2");


                return params;
            }
        };

        Volley.newRequestQueue(this).add(istek);
    }

    public void tumKisiler() {

        String url = "https://snowpiercer.store/bayrakquiz/tum_kisiler.php";

        StringRequest istek = new StringRequest(Request.Method.GET, url, new Response.Listener<String>() {
            @Override
            public void onResponse(String response) {
                Log.e("Cevap",response);

                try {
                    JSONObject jsonObject = new JSONObject(response);

                    JSONArray kisilerListe = jsonObject.getJSONArray("kisiler");

                    for(int i =0; i<kisilerListe.length();i++) {
                        JSONObject k = kisilerListe.getJSONObject(i);

                        int kisi_id = k.getInt("kisi_id");
                        String kisi_ad = k.getString("kisi_ad");
                        String kisi_tel = k.getString("kisi_tel");

                        Log.e("kisi_id",String.valueOf(kisi_id));
                        Log.e("kisi_ad",kisi_ad);
                        Log.e("kisi_tel",kisi_tel);
                        Log.e("********","********");
                    }

                } catch (JSONException e) {
                    throw new RuntimeException(e);
                }

            }
        }, new Response.ErrorListener() {
            @Override
            public void onErrorResponse(VolleyError error) {

            }
        });

        Volley.newRequestQueue(this).add(istek);
    }

    public void kisiArama() {

        String url = "https://snowpiercer.store/bayrakquiz/tum_kisiler_arama.php";

        StringRequest istek = new StringRequest(Request.Method.POST, url, new Response.Listener<String>() {
            @Override
            public void onResponse(String response) {
                Log.e("Cevap",response);

                try {
                    JSONObject jsonObject = new JSONObject(response);

                    JSONArray kisilerListe = jsonObject.getJSONArray("kisiler");

                    for(int i =0; i<kisilerListe.length();i++) {
                        JSONObject k = kisilerListe.getJSONObject(i);

                        int kisi_id = k.getInt("kisi_id");
                        String kisi_ad = k.getString("kisi_ad");
                        String kisi_tel = k.getString("kisi_tel");

                        Log.e("kisi_id",String.valueOf(kisi_id));
                        Log.e("kisi_ad",kisi_ad);
                        Log.e("kisi_tel",kisi_tel);
                        Log.e("********","********");
                    }

                } catch (JSONException e) {
                    throw new RuntimeException(e);
                }

            }
        }, new Response.ErrorListener() {
            @Override
            public void onErrorResponse(VolleyError error) {

            }
        }){
            @Nullable
            @Override
            protected Map<String, String> getParams() throws AuthFailureError {

                Map<String,String> params = new HashMap<>();

                params.put("kisi_ad","p");

                return params;
            }
        };

        Volley.newRequestQueue(this).add(istek);
    }
}
```
* AndroidManifest.xml
```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">
    
    <uses-permission android:name="android.permission.INTERNET"/>

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:supportsRtl="true"
        android:theme="@style/Theme.VolleyCalismasi"
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
# Retrofit Kütüphanesi Kurulumu ve CRUD işlemi
* MainActivity
```
package com.example.retrofitcalismasi;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.util.Log;

import java.util.List;

import retrofit2.Call;
import retrofit2.Callback;
import retrofit2.Response;

public class MainActivity extends AppCompatActivity {
    private KisilerDaoInterface kisilerDIF;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        kisilerDIF = ApiUtils.getKisilerDaoInterface();
        tumKisiler();
        //tumKisiAra();
        //kisiSil();
        //kisiEkle();
        //kisiGuncelle();
    }

    public void tumKisiler() {

        kisilerDIF.tumKisiler().enqueue(new Callback<KisilerCevap>() {
            @Override
            public void onResponse(Call<KisilerCevap> call, Response<KisilerCevap> response) {
                List<Kisiler> kisilerList = response.body().getKisiler();

                for (Kisiler k: kisilerList) {
                    Log.e("Kişi id",k.getKisiId());
                    Log.e("Kişi ad",k.getKisiAd());
                    Log.e("Kişi tel",k.getKisiTel());
                    Log.e("*******","********");
                }
            }

            @Override
            public void onFailure(Call<KisilerCevap> call, Throwable t) {

            }
        });

    }

    public void tumKisiAra() {

        kisilerDIF.kisiAra("p").enqueue(new Callback<KisilerCevap>() {
            @Override
            public void onResponse(Call<KisilerCevap> call, Response<KisilerCevap> response) {
                List<Kisiler> kisilerList = response.body().getKisiler();

                for (Kisiler k: kisilerList) {
                    Log.e("Kişi id", k.getKisiId());
                    Log.e("Kişi ad", k.getKisiAd());
                    Log.e("Kişi tel", k.getKisiTel());
                    Log.e("*******", "********");
                }
            }

            @Override
            public void onFailure(Call<KisilerCevap> call, Throwable t) {

            }
        });
    }

    public void kisiSil() {

        kisilerDIF.kisiSil(3).enqueue(new Callback<CRUDCevap>() {
            @Override
            public void onResponse(Call<CRUDCevap> call, Response<CRUDCevap> response) {
                Log.e("Başarı",response.body().getSuccess().toString());
                Log.e("Mesaj",response.body().getMessage().toString());
            }

            @Override
            public void onFailure(Call<CRUDCevap> call, Throwable t) {

            }
        });
    }

    public void kisiEkle(){
        kisilerDIF.kisiEkle("pelin","05234235").enqueue(new Callback<CRUDCevap>() {
            @Override
            public void onResponse(Call<CRUDCevap> call, Response<CRUDCevap> response) {
                Log.e("Başarı",response.body().getSuccess().toString());
                Log.e("Mesaj",response.body().getMessage().toString());
            }

            @Override
            public void onFailure(Call<CRUDCevap> call, Throwable t) {

            }
        });
    }

    public void kisiGuncelle(){
        kisilerDIF.kisiGuncelle(5,"Hazal","05235234").enqueue(new Callback<CRUDCevap>() {
            @Override
            public void onResponse(Call<CRUDCevap> call, Response<CRUDCevap> response) {
                Log.e("Başarı",response.body().getSuccess().toString());
                Log.e("Mesaj",response.body().getMessage().toString());
            }

            @Override
            public void onFailure(Call<CRUDCevap> call, Throwable t) {

            }
        });
    }
}
```
* ApiUtils
```
package com.example.retrofitcalismasi;

public class ApiUtils {
    public static final String BASE_URL = "https://snowpiercer.store/";

    public static KisilerDaoInterface getKisilerDaoInterface() {
        return RetrofitClient.getClient(BASE_URL).create(KisilerDaoInterface.class);
    }

}
```
* CRUDcevap
```

package com.example.retrofitcalismasi;

import com.google.gson.annotations.Expose;
import com.google.gson.annotations.SerializedName;

public class CRUDCevap {

    @SerializedName("success")
    @Expose
    private Integer success;
    @SerializedName("message")
    @Expose
    private String message;

    public Integer getSuccess() {
        return success;
    }

    public void setSuccess(Integer success) {
        this.success = success;
    }

    public String getMessage() {
        return message;
    }

    public void setMessage(String message) {
        this.message = message;
    }

}
```
* Kisiler
```

package com.example.retrofitcalismasi;

import com.google.gson.annotations.Expose;
import com.google.gson.annotations.SerializedName;

public class Kisiler {

    @SerializedName("kisi_id")
    @Expose
    private String kisiId;
    @SerializedName("kisi_ad")
    @Expose
    private String kisiAd;
    @SerializedName("kisi_tel")
    @Expose
    private String kisiTel;

    public String getKisiId() {
        return kisiId;
    }

    public void setKisiId(String kisiId) {
        this.kisiId = kisiId;
    }

    public String getKisiAd() {
        return kisiAd;
    }

    public void setKisiAd(String kisiAd) {
        this.kisiAd = kisiAd;
    }

    public String getKisiTel() {
        return kisiTel;
    }

    public void setKisiTel(String kisiTel) {
        this.kisiTel = kisiTel;
    }

}
```
* KisilerCevap
```

package com.example.retrofitcalismasi;

import java.util.List;
import com.google.gson.annotations.Expose;
import com.google.gson.annotations.SerializedName;

public class KisilerCevap {

    @SerializedName("kisiler")
    @Expose
    private List<Kisiler> kisiler;
    @SerializedName("success")
    @Expose
    private Integer success;

    public List<Kisiler> getKisiler() {
        return kisiler;
    }

    public void setKisiler(List<Kisiler> kisiler) {
        this.kisiler = kisiler;
    }

    public Integer getSuccess() {
        return success;
    }

    public void setSuccess(Integer success) {
        this.success = success;
    }

}
```
* KisilerDAOinterface
```
package com.example.retrofitcalismasi;


import retrofit2.Call;
import retrofit2.http.Field;
import retrofit2.http.FormUrlEncoded;
import retrofit2.http.GET;
import retrofit2.http.POST;

public interface KisilerDaoInterface {

    @GET("bayrakquiz/tum_kisiler.php")
    Call<KisilerCevap> tumKisiler();

    @POST("bayrakquiz/tum_kisiler_arama.php")
    @FormUrlEncoded
    Call<KisilerCevap> kisiAra(@Field("kisi_ad") String kisi_ad);

    @POST("bayrakquiz/delete_kisiler.php")
    @FormUrlEncoded
    Call<CRUDCevap> kisiSil(@Field("kisi_id") int kisi_id);

    @POST("bayrakquiz/insert_kisiler.php")
    @FormUrlEncoded
    Call<CRUDCevap> kisiEkle(@Field("kisi_ad") String kisi_ad
                            ,@Field("kisi_tel") String kisi_tel);

    @POST("bayrakquiz/update_kisiler.php")
    @FormUrlEncoded
    Call<CRUDCevap> kisiGuncelle(@Field("kisi_id") int kisi_id
            ,@Field("kisi_ad") String kisi_ad
            ,@Field("kisi_tel") String kisi_tel);

}
```
* RetrofitClient
```
package com.example.retrofitcalismasi;

import java.sql.PreparedStatement;

import retrofit2.Retrofit;
import retrofit2.converter.gson.GsonConverterFactory;

public class RetrofitClient {

    private static Retrofit retrofit = null;

    public static Retrofit getClient(String baseUrl) {
        if(retrofit == null) {
            retrofit = new Retrofit.Builder()
                    .baseUrl(baseUrl)
                    .addConverterFactory(GsonConverterFactory.create())
                    .build();
        }

        return retrofit;
    }
}
```
* build.gradle
```
plugins {
    id 'com.android.application'
}

android {
    namespace 'com.example.retrofitcalismasi'
    compileSdk 33

    defaultConfig {
        applicationId "com.example.retrofitcalismasi"
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
    implementation'com.google.code.gson:gson:2.6.2'
    implementation'com.squareup.retrofit2:retrofit:2.0.2'
    implementation'com.squareup.retrofit2:converter-gson:2.0.2'
}
```
* AndroidManifest.xml
```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <uses-permission android:name="android.permission.INTERNET"/>

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:supportsRtl="true"
        android:theme="@style/Theme.RetrofitCalismasi"
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

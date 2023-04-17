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

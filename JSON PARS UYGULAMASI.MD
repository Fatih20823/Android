# mainActivity
```
package com.example.jsonparseuygulamas;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.util.Log;

import org.json.JSONArray;
import org.json.JSONException;
import org.json.JSONObject;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        String jsonVeri = "{\"bayrakquiz\":[{\"bayrak_id\":\"1\",\"bayrak_ad\":\"T\\u00fcrkiye\",\"bayrak_resim\":\"turk\\u0131ye\"},{\"bayrak_id\":\"2\",\"bayrak_ad\":\"Almanya\",\"bayrak_resim\":\"almanya\"},{\"bayrak_id\":\"3\",\"bayrak_ad\":\"\\u0130talya\",\"bayrak_resim\":\"italya\"},{\"bayrak_id\":\"4\",\"bayrak_ad\":\"Fransa\",\"bayrak_resim\":\"fransa\"},{\"bayrak_id\":\"5\",\"bayrak_ad\":\"Hollanda\",\"bayrak_resim\":\"hollanda\"},{\"bayrak_id\":\"6\",\"bayrak_ad\":\"\\u0130spanya\",\"bayrak_resim\":\"ispanya\"},{\"bayrak_id\":\"7\",\"bayrak_ad\":\"Slovenya\",\"bayrak_resim\":\"slovenya\"},{\"bayrak_id\":\"8\",\"bayrak_ad\":\"Slovakya\",\"bayrak_resim\":\"slovakya\"},{\"bayrak_id\":\"9\",\"bayrak_ad\":\"Estonya\",\"bayrak_resim\":\"estonya\"},{\"bayrak_id\":\"10\",\"bayrak_ad\":\"Rusya\",\"bayrak_resim\":\"rusya\"},{\"bayrak_id\":\"11\",\"bayrak_ad\":\"Bulgaristan\",\"bayrak_resim\":\"bulgaristan\"},{\"bayrak_id\":\"12\",\"bayrak_ad\":\"Romanya\",\"bayrak_resim\":\"romanya\"},{\"bayrak_id\":\"13\",\"bayrak_ad\":\"Norve\\u00e7\",\"bayrak_resim\":\"norvec\"},{\"bayrak_id\":\"14\",\"bayrak_ad\":\"Yunanistan\",\"bayrak_resim\":\"yunanistan\"},{\"bayrak_id\":\"15\",\"bayrak_ad\":\"Bosna Hersek\",\"bayrak_resim\":\"bosnahersek\"}],\"success\":1}";

        try {
            JSONObject jsonObject = new JSONObject(jsonVeri);

            JSONArray bayraklarListe = jsonObject.getJSONArray("bayrakquiz");

            for(int i=0; i<bayraklarListe.length();i++) {
                 JSONObject b = bayraklarListe.getJSONObject(i);

                 int bayrak_id = b.getInt("bayrak_id");
                 String bayrak_ad = b.getString("bayrak_ad");
                 String bayrak_resim = b.getString("bayrak_resim");

                Log.e("************","**********");
                Log.e("bayrak_id",String.valueOf(bayrak_id));
                Log.e("bayrak_ad",bayrak_ad);
                Log.e("bayrak_resim",bayrak_resim);
                Log.e("************","**********");

            }

        } catch (JSONException e) {
            throw new RuntimeException(e);
        }
    }
}
```

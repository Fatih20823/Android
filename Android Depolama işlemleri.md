# Shared Preferences
![SharedPreferences](https://user-images.githubusercontent.com/101557027/228895659-b32ae9c9-323c-4fe3-ba0f-aa5efcc4f240.gif)
* MainActivity
```
import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.content.SharedPreferences;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;

import java.util.HashSet;
import java.util.Set;

public class MainActivity extends AppCompatActivity {
    private Button buttonKaydet;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        buttonKaydet = findViewById(R.id.buttonKaydet);

        buttonKaydet.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {

                SharedPreferences sp = getSharedPreferences("KisiselBilgiler",MODE_PRIVATE);

                SharedPreferences.Editor e = sp.edit();

                e.putString("ad","ahmet");
                e.putInt("yas",18);
                e.putFloat("boy",1.78f);
                e.putBoolean("bekar",true);

                Set<String> arkadasListesi = new HashSet<>();

                arkadasListesi.add("zeynep");
                arkadasListesi.add("kadir");

                e.putStringSet("arkadasListesi",arkadasListesi);

                e.commit();

                startActivity(new Intent(MainActivity.this,SecondActivity.class));
            }
        });
    }
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

    <Button
        android:id="@+id/buttonKaydet"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Kaydet"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.5" />
</androidx.constraintlayout.widget.ConstraintLayout>
```
* SecondActivity
```
import androidx.appcompat.app.AppCompatActivity;

import android.content.SharedPreferences;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

import java.util.Set;

public class SecondActivity extends AppCompatActivity {
    private Button buttonSil,buttonGuncelle;
    private TextView textViewCikti;
    private SharedPreferences sp;
    private SharedPreferences.Editor e;
    private String ad;
    private int yas;
    private float boy;
    private boolean bekar;
    private Set<String> arkadasListesi;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_second);

        buttonSil = findViewById(R.id.buttonSil);
        buttonGuncelle = findViewById(R.id.buttonGuncelle);
        textViewCikti = findViewById(R.id.textViewCikti);

        sp = getSharedPreferences("KisiselBilgiler",MODE_PRIVATE);
        e = sp.edit();

        ad = sp.getString("ad","isim yok");
        yas = sp.getInt("yas",0);
        boy = sp.getFloat("boy",0.0f);
        bekar = sp.getBoolean("bekar",false);
        arkadasListesi = sp.getStringSet("arkadasListesi",null);

        final StringBuilder sb = new StringBuilder();

        for (String s:arkadasListesi) {
            sb.append(s+" ");
        }

        textViewCikti.setText("AD :"+ad+" Yaş :"+yas+" Boy :"+boy+" Bekar :"+bekar+" Arkadaşlar :"+sb.toString());

        buttonSil.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                e.remove("ad");
                e.commit();

                ad = sp.getString("ad","isim yok");
                textViewCikti.setText("AD :"+ad+" Yaş :"+yas+" Boy :"+boy+" Bekar :"+bekar+" Arkadaşlar :"+sb.toString());
            }
        });

        buttonGuncelle.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                e.putInt("yas",400);
                e.commit();

                yas = sp.getInt("yas",0);
                textViewCikti.setText("AD :"+ad+" Yaş :"+yas+" Boy :"+boy+" Bekar :"+bekar+" Arkadaşlar :"+sb.toString());
            }
        });
    }
}
```
* activity_second.xml
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".SecondActivity">

    <TextView
        android:id="@+id/textViewCikti"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="133dp"
        android:text="TextView"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <Button
        android:id="@+id/buttonSil"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="145dp"
        android:text="Sil"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toStartOf="@+id/buttonGuncelle"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent" />

    <Button
        android:id="@+id/buttonGuncelle"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="145dp"
        android:text="Güncelle"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toEndOf="@+id/buttonSil" />
</androidx.constraintlayout.widget.ConstraintLayout>
```
------------------
# Shared Preferences Giriş Sayaç Uygulası
![SPGirişSayacUygulaması](https://user-images.githubusercontent.com/101557027/228894749-a993cb46-0ac4-4d03-a284-ef00da66800e.gif)
------
* MainActivity
```
import androidx.appcompat.app.AppCompatActivity;

import android.content.SharedPreferences;
import android.os.Bundle;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {
    private TextView textViewSayac;
    private SharedPreferences sp;
    private SharedPreferences.Editor editor;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        textViewSayac = findViewById(R.id.textViewSayac);

        sp = getSharedPreferences("GirisSayac",MODE_PRIVATE);
        editor = sp.edit();

        int sayac = sp.getInt("sayac",0);

        editor.putInt("sayac",++sayac);

        editor.commit();

        textViewSayac.setText("Sayaç :"+String.valueOf(sayac));
    }
}
```
-----------
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
        android:id="@+id/textViewSayac"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="SAYAÇ : 0"
        android:textSize="34sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
```


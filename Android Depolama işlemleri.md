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
# Shared Preferences Login Ekranı Uygulama
![spLoginEkrani](https://user-images.githubusercontent.com/101557027/229049257-adcb2652-540b-4462-a90b-e21b98a8095e.gif)
-------
* MainActivity
```
import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.content.SharedPreferences;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {

    private EditText editTextUsername,editTextPassword;
    private Button buttonGiris;
    private SharedPreferences sp;
    private SharedPreferences.Editor editor;
    private String username;
    private String password;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        editTextUsername = findViewById(R.id.editTextUsername);
        editTextPassword = findViewById(R.id.editTextPassword);
        buttonGiris = findViewById(R.id.buttonGiris);

        sp = getSharedPreferences("GirisBilgi",MODE_PRIVATE);
        editor = sp.edit();

        username = sp.getString("username","kullnıcı adı yok !");
        password = sp.getString("password","şifre yok !");

        if (username.equals("admin") && password.equals("123")){
            startActivity(new Intent(MainActivity.this,AnaEkranActivity.class));
            finish();
        }

        buttonGiris.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if (editTextUsername.getText().toString().equals("admin") && editTextPassword.getText().toString().equals("123")) {

                    editor.putString("username",editTextUsername.getText().toString());
                    editor.putString("password",editTextPassword.getText().toString());
                    editor.commit();

                    startActivity(new Intent(MainActivity.this,AnaEkranActivity.class));
                    finish();
                }else {
                    Toast.makeText(getApplicationContext(),"Giriş Hatalı !",Toast.LENGTH_SHORT).show();
                }
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

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="92dp"
        android:text="Login Ekranı"
        android:textSize="34sp"
        android:textStyle="bold"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <EditText
        android:id="@+id/editTextUsername"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="81dp"
        android:ems="10"
        android:hint="Username"
        android:inputType="text"
        android:textSize="24sp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textView" />

    <EditText
        android:id="@+id/editTextPassword"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="101dp"
        android:ems="10"
        android:hint="Password"
        android:inputType="numberPassword"
        android:textSize="24sp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/editTextUsername" />

    <Button
        android:id="@+id/buttonGiris"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="88dp"
        android:layout_marginBottom="58dp"
        android:text="Giriş"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/editTextPassword" />

</androidx.constraintlayout.widget.ConstraintLayout>
```
* AnaEkranActivity
```
import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.content.SharedPreferences;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

public class AnaEkranActivity extends AppCompatActivity {

    private Button buttonCikisYap;
    private TextView textViewCikti;
    private SharedPreferences sp;
    private SharedPreferences.Editor editor;
    private String username;
    private String password;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_ana_ekran);

        buttonCikisYap = (Button) findViewById(R.id.buttonCikisYap);
        textViewCikti = (TextView) findViewById(R.id.textViewCikti);

        sp = getSharedPreferences("GirisBilgi",MODE_PRIVATE);
        editor = sp.edit();

        username = sp.getString("username","kullanıcı adı yok !");
        password = sp.getString("password","şifre yok !");

        textViewCikti.setText("Username : "+username+" Password : "+password);

        buttonCikisYap.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {

                editor.remove("username");
                editor.remove("password");
                editor.commit();

                startActivity(new Intent(AnaEkranActivity.this,MainActivity.class));
                finish();
            }
        });
    }
}
```
* activity_ana_ekran.xml
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".AnaEkranActivity">

    <TextView
        android:id="@+id/textViewCikti"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="130dp"
        android:text="Username:. Password:"
        android:textSize="20sp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <Button
        android:id="@+id/buttonCikisYap"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="177dp"
        android:text="ÇIKIŞ YAP"
        android:textSize="14sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.498"
        app:layout_constraintStart_toStartOf="parent" />
</androidx.constraintlayout.widget.ConstraintLayout>
```
# Harici Depolama External Storage
![Harici-Depolama](https://user-images.githubusercontent.com/101557027/229277716-0fc3131f-dbc9-4cce-b6f1-abd8f8ea3ff0.gif)
----------
# MainActivity
```
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.os.Environment;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.File;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;

public class MainActivity extends AppCompatActivity {
    private EditText editTextGirdi;
    private Button buttonYaz,buttonOku,buttonSil;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        editTextGirdi = findViewById(R.id.editTextGirdi);
        buttonYaz = findViewById(R.id.buttonYaz);
        buttonOku = findViewById(R.id.buttonOku);
        buttonSil = findViewById(R.id.buttonSil);

        buttonYaz.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                hariciYaz();

            }
        });

        buttonOku.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                hariciOku();
            }
        });

        buttonSil.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                hariciSil();
            }
        });
    }

    public void hariciYaz() {
      try {

          File dosyaYolu = Environment.getExternalStorageDirectory();

          File dosya = new File(dosyaYolu, "dosyam.txt");

          if (!dosya.exists()) {
              dosya.createNewFile();
          }

          FileWriter fw = new FileWriter(dosya);

          BufferedWriter yazici = new BufferedWriter(fw);

          yazici.write(editTextGirdi.getText().toString());

          yazici.flush();
          yazici.close();
          fw.close();

          editTextGirdi.setText("");
      }catch (IOException e) {
          e.printStackTrace();
      }
    }

    public void hariciOku() {
        try {

            File dosyaYolu = Environment.getExternalStorageDirectory();

            File dosya = new File(dosyaYolu, "dosyam.txt");

            FileReader fr = new FileReader(dosya);

            BufferedReader okuyucu = new BufferedReader(fr);

            StringBuilder sb = new StringBuilder();

            String satir = "";

            while ((satir = okuyucu.readLine()) != null){
                sb.append(satir+"\n");
            }

            okuyucu.close();

            editTextGirdi.setText(sb.toString());
        }catch (IOException e) {
            e.printStackTrace();
        }
    }

    public void hariciSil() {

            File dosyaYolu = Environment.getExternalStorageDirectory();

            File dosya = new File(dosyaYolu, "dosyam.txt");

            dosya.delete();
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

    <EditText
        android:id="@+id/editTextGirdi"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="106dp"
        android:ems="10"
        android:hint="Veri giriniz"
        android:inputType="textPersonName"
        android:textColor="#070707"
        android:textSize="20sp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <Button
        android:id="@+id/buttonYaz"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="93dp"
        android:text="YAZ"
        app:layout_constraintEnd_toStartOf="@+id/buttonOku"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/editTextGirdi" />

    <Button
        android:id="@+id/buttonOku"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="93dp"
        android:text="Oku"
        app:layout_constraintEnd_toStartOf="@+id/buttonSil"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toEndOf="@+id/buttonYaz"
        app:layout_constraintTop_toBottomOf="@+id/editTextGirdi" />

    <Button
        android:id="@+id/buttonSil"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="93dp"
        android:text="Sil"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toEndOf="@+id/buttonOku"
        app:layout_constraintTop_toBottomOf="@+id/editTextGirdi" />
</androidx.constraintlayout.widget.ConstraintLayout>
```
# Dahili Depolama Internal Storage
![Untitleddahili](https://user-images.githubusercontent.com/101557027/229277674-2183bf65-b5dd-480f-93ee-2a26c41818df.gif)
-------
* MainActivity
```
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.os.Environment;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.File;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.OutputStreamWriter;

public class MainActivity extends AppCompatActivity {
    private EditText editTextGirdi;
    private Button buttonYaz,buttonOku,buttonSil;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        editTextGirdi = findViewById(R.id.editTextGirdi);
        buttonYaz = findViewById(R.id.buttonYaz);
        buttonOku = findViewById(R.id.buttonOku);
        buttonSil = findViewById(R.id.buttonSil);

        buttonYaz.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                //hariciYaz();
                dahiliYaz();

            }
        });

        buttonOku.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {

                //hariciOku();
                dahilıOku();
            }
        });

        buttonSil.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {

                //hariciSil();
                dahiliSil();
            }
        });
    }
    public void dahiliYaz() {

        try {
            FileOutputStream fos = openFileOutput("dosyam.txt",MODE_PRIVATE);

            OutputStreamWriter yazici = new OutputStreamWriter(fos);

            yazici.write(editTextGirdi.getText().toString());

            yazici.close();

            editTextGirdi.setText("");
        }catch (Exception e) {
            e.printStackTrace();
        }
    }

    public void dahilıOku(){
         try {
             FileInputStream fis = openFileInput("dosyam.txt");

             InputStreamReader isr = new InputStreamReader(fis);

             BufferedReader okuyucu = new BufferedReader(isr);

             StringBuilder sb = new StringBuilder();

             String satir = "";

             while(((satir = okuyucu.readLine()) != null)) {
                 sb.append(satir+"\n");
             }

             okuyucu.close();

             editTextGirdi.setText(sb.toString());
         }catch (Exception e) {
             e.printStackTrace();
         }
    }

    public void dahiliSil() {
        File yol = getFilesDir();

        File file = new File(yol,"dosyam.txt");

        editTextGirdi.setText(String.valueOf(file.delete()));

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

    <EditText
        android:id="@+id/editTextGirdi"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="106dp"
        android:ems="10"
        android:hint="Veri giriniz"
        android:inputType="textPersonName"
        android:textColor="#070707"
        android:textSize="20sp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <Button
        android:id="@+id/buttonYaz"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="93dp"
        android:text="YAZ"
        app:layout_constraintEnd_toStartOf="@+id/buttonOku"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/editTextGirdi" />

    <Button
        android:id="@+id/buttonOku"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="93dp"
        android:text="Oku"
        app:layout_constraintEnd_toStartOf="@+id/buttonSil"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toEndOf="@+id/buttonYaz"
        app:layout_constraintTop_toBottomOf="@+id/editTextGirdi" />

    <Button
        android:id="@+id/buttonSil"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="93dp"
        android:text="Sil"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toEndOf="@+id/buttonOku"
        app:layout_constraintTop_toBottomOf="@+id/editTextGirdi" />
</androidx.constraintlayout.widget.ConstraintLayout>
```
--------
# Veri Tabanı Sozluk Uygulaması

* MainActivity
```
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.util.Log;

import java.util.ArrayList;

public class MainActivity extends AppCompatActivity {

    private VeritabaniYardimcisi vt;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        vt = new VeritabaniYardimcisi(this);

        /*new Kelimelerdao().kelimeEkle(vt,"door","kapı");
        new Kelimelerdao().kelimeEkle(vt,"window","pencere");
        new Kelimelerdao().kelimeEkle(vt,"sea","deniz");
        new Kelimelerdao().kelimeEkle(vt,"table","masa");
        new Kelimelerdao().kelimeEkle(vt,"pencil","kalem");*/

        //new Kelimelerdao().kelimeSil(vt,5);

        //new Kelimelerdao().kelimeGuncelle(vt,4,"seaxxxxx","denizxxxxx");

       // int sonuc =new Kelimelerdao().kayitKontrol(vt);
       // Log.e("Veri sayısı",String.valueOf(sonuc));

       //Kelimeler kelime = new Kelimelerdao().kelimeGetir(vt,2);

       //Log.e("Kelime",kelime.getKelime_id()+" - "+kelime.getIngilizce()+" - "+kelime.getTurkce());

        ArrayList<Kelimeler> gelenKelimelerListesi = new Kelimelerdao().kelimeAra(vt,"ea");

        for (Kelimeler k: gelenKelimelerListesi) {
            Log.e(String.valueOf(k.getKelime_id()),k.getIngilizce()+"-"+k.getTurkce());
        }
    }
}
```
* Kelimeler
```
public class Kelimeler {

    private int kelime_id;
    private String ingilizce;
    private String turkce;

    public Kelimeler() {
    }

    public Kelimeler(int kelime_id, String ingilizce, String turkce) {
        this.kelime_id = kelime_id;
        this.ingilizce = ingilizce;
        this.turkce = turkce;
    }

    public int getKelime_id() {
        return kelime_id;
    }

    public void setKelime_id(int kelime_id) {
        this.kelime_id = kelime_id;
    }

    public String getIngilizce() {
        return ingilizce;
    }

    public void setIngilizce(String ingilizce) {
        this.ingilizce = ingilizce;
    }

    public String getTurkce() {
        return turkce;
    }

    public void setTurkce(String turkce) {
        this.turkce = turkce;
    }
}
```
* KelimelerDao
```
import android.annotation.SuppressLint;
import android.content.ContentValues;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;

import java.util.ArrayList;

public class Kelimelerdao {

    public void kelimeEkle(VeritabaniYardimcisi vt, String ingilizce,String turkce) {
        SQLiteDatabase dbx = vt.getWritableDatabase();
        ContentValues degerler = new ContentValues();

        degerler.put("ingilizce",ingilizce);
        degerler.put("turkce",turkce);

        dbx.insertOrThrow("kelimeler",null,degerler);
        dbx.close();
    }

    public ArrayList<Kelimeler> tumkelimeler(VeritabaniYardimcisi vt) {
        ArrayList<Kelimeler> kelimelerArrayList = new ArrayList<>();
        SQLiteDatabase dbx = vt.getWritableDatabase();

        Cursor c = dbx.rawQuery("SELECT * FROM kelimeler",null);

        while(c.moveToNext()){
            @SuppressLint("Range") Kelimeler kelime = new Kelimeler(c.getInt(c.getColumnIndex("kelime_id"))
                        ,c.getString(c.getColumnIndex("ingilizce"))
                        ,c.getString(c.getColumnIndex("turkce")));
            kelimelerArrayList.add(kelime);
        }

        return kelimelerArrayList;
    }

    public void kelimeSil(VeritabaniYardimcisi vt, int kelime_id){
        SQLiteDatabase dbx = vt.getWritableDatabase();
        dbx.delete("kelimeler","kelime_id=?",new String[]{String.valueOf(kelime_id)});
        dbx.close();
    }

    public void kelimeGuncelle(VeritabaniYardimcisi vt,int kelime_id, String ingilizce,String turkce) {
        SQLiteDatabase dbx = vt.getWritableDatabase();
        ContentValues degerler = new ContentValues();

        degerler.put("ingilizce",ingilizce);
        degerler.put("turkce",turkce);

        dbx.update("kelimeler",degerler,"kelime_id=?",new String[]{String.valueOf(kelime_id)});
        dbx.close();
    }

    @SuppressLint("Range")
    public int kayitKontrol(VeritabaniYardimcisi vt){
        int sonuc= 0;
        SQLiteDatabase dbx = vt.getWritableDatabase();

        Cursor c = dbx.rawQuery("SELECT count(*) as sonuc FROM kelimeler",null);

        while (c.moveToNext()) {
            sonuc = c.getInt(c.getColumnIndex("sonuc"));
        }
        return sonuc;
    }

    public Kelimeler kelimeGetir(VeritabaniYardimcisi vt, int kelime_id){
        Kelimeler kelime = new Kelimeler();
        SQLiteDatabase dbx = vt.getWritableDatabase();

        Cursor c = dbx.rawQuery("SELECT * FROM kelimeler WHERE kelime_id="+kelime_id,null);

        while (c.moveToNext()) {
            @SuppressLint("Range") Kelimeler k = new Kelimeler(c.getInt(c.getColumnIndex("kelime_id"))
                        ,c.getString(c.getColumnIndex("ingilizce"))
                        ,c.getString(c.getColumnIndex("turkce")));
            kelime = k;
        }

        return kelime;
    }

    public ArrayList<Kelimeler> tumkelimelerRasgele4(VeritabaniYardimcisi vt) {
        ArrayList<Kelimeler> kelimelerArrayList = new ArrayList<>();
        SQLiteDatabase dbx = vt.getWritableDatabase();

        Cursor c = dbx.rawQuery("SELECT * FROM kelimeler ORDER BY RANDOM () LIMIT 2",null);

        while(c.moveToNext()){
            @SuppressLint("Range") Kelimeler kelime = new Kelimeler(c.getInt(c.getColumnIndex("kelime_id"))
                    ,c.getString(c.getColumnIndex("ingilizce"))
                    ,c.getString(c.getColumnIndex("turkce")));
            kelimelerArrayList.add(kelime);
        }

        return kelimelerArrayList;
    }
    public ArrayList<Kelimeler> kelimeAra(VeritabaniYardimcisi vt,String keyword) {
        ArrayList<Kelimeler> kelimelerArrayList = new ArrayList<>();
        SQLiteDatabase dbx = vt.getWritableDatabase();

        Cursor c = dbx.rawQuery("SELECT * FROM kelimeler WHERE ingilizce like '%"+keyword+"%'",null);

        while(c.moveToNext()){
            @SuppressLint("Range") Kelimeler kelime = new Kelimeler(c.getInt(c.getColumnIndex("kelime_id"))
                    ,c.getString(c.getColumnIndex("ingilizce"))
                    ,c.getString(c.getColumnIndex("turkce")));
            kelimelerArrayList.add(kelime);
        }

        return kelimelerArrayList;
    }
}
```
* VeritabaniYardimcisi
```
import android.content.Context;
import android.database.sqlite.SQLiteDatabase;
import android.database.sqlite.SQLiteOpenHelper;

import androidx.annotation.Nullable;

public class VeritabaniYardimcisi extends SQLiteOpenHelper {

    public VeritabaniYardimcisi(@Nullable Context context) {
        super(context,"sozluk",null,1);
    }

    @Override
    public void onCreate(SQLiteDatabase db) {
        db.execSQL("CREATE TABLE \"kelimeler\" (\n" +
                "\t\"kelime_id\"\tINTEGER,\n" +
                "\t\"ingilizce\"\tTEXT,\n" +
                "\t\"turkce\"\tTEXT,\n" +
                "\tPRIMARY KEY(\"kelime_id\" AUTOINCREMENT)\n" +
                ");");
    }

    @Override
    public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {
        db.execSQL("DROP TABLE IF EXISTS kelimeler");
            onCreate(db);

    }
}
```

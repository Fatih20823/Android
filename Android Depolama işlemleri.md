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
# Sözlük Uygulaması
![sozluk](https://user-images.githubusercontent.com/101557027/230627171-e72584cd-f463-4f79-8a29-134345d4f799.gif)
* MainActivity
```
package com.example.szlkuygulamas;

import androidx.appcompat.app.AppCompatActivity;
import androidx.appcompat.widget.SearchView;
import androidx.appcompat.widget.Toolbar;
import androidx.recyclerview.widget.LinearLayoutManager;
import androidx.recyclerview.widget.RecyclerView;

import android.os.Bundle;
import android.os.ParcelUuid;
import android.util.Log;
import android.view.Menu;
import android.view.MenuItem;

import java.io.IOException;
import java.util.ArrayList;


public class MainActivity extends AppCompatActivity implements SearchView.OnQueryTextListener {
    private Toolbar toolbar;
    private RecyclerView rv;
    private ArrayList<Kelimeler> kelimelerListe;
    private KelimelerAdapter adapter;

    private Veritabani vt;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        toolbar = findViewById(R.id.toolbar);
        rv = findViewById(R.id.rv);

        toolbar.setTitle("Sözlük Uygulaması");
        setSupportActionBar(toolbar);

        vt = new Veritabani(this);

        veritabaniKopyala();

        rv.setHasFixedSize(true);
        rv.setLayoutManager(new LinearLayoutManager(this));

        kelimelerListe = new kelimelerDao().tumKelimeler(vt);

        adapter = new KelimelerAdapter(this,kelimelerListe);
        rv.setAdapter(adapter);
    }

    @Override //Arama çubuğu kodu
    public boolean onCreateOptionsMenu(Menu menu) {
        getMenuInflater().inflate(R.menu.toolbarmenu,menu);

        MenuItem item = menu.findItem(R.id.action_ara);

        SearchView searchView = (SearchView) item.getActionView();

        searchView.setOnQueryTextListener(this);

        return super.onCreateOptionsMenu(menu);
    }

    @Override //Arama çubuğu kodu
    public boolean onQueryTextSubmit(String query) {
        Log.e("Gönderilen Arama",query);
        aramaYap(query);
        return false;
    }

    @Override //Arama çubuğu kodu
    public boolean onQueryTextChange(String newText) {
        Log.e("Harf Girdikçe",newText);
        aramaYap(newText);
        return false;
    }

    public void veritabaniKopyala() {
        DatabaseCopyHelper databaseCopyHelper = new DatabaseCopyHelper(this);

        try {
            databaseCopyHelper.createDataBase();
        } catch (IOException e) {
            throw new RuntimeException(e);
        }

        databaseCopyHelper.openDataBase();
    }

    public void aramaYap(String aramaKelime) {

        kelimelerListe = new kelimelerDao().kelimeAra(vt,aramaKelime);

        adapter = new KelimelerAdapter(this,kelimelerListe);

        rv.setAdapter(adapter);
    }

}
```
* Kelimeler
```
package com.example.szlkuygulamas;

import java.io.Serializable;

public class Kelimeler implements Serializable {
    private int kelime_id;
    private String ingilizce;
    private String turkce;

    public Kelimeler () {
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
* KelimelerAdapter
```
package com.example.szlkuygulamas;

import android.content.Context;
import android.content.Intent;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.TextView;
import android.widget.Toast;

import androidx.annotation.NonNull;
import androidx.cardview.widget.CardView;
import androidx.recyclerview.widget.RecyclerView;

import java.util.List;

public class KelimelerAdapter extends RecyclerView.Adapter<KelimelerAdapter.CardTasarimTutucu> {
    private Context mContext;
    private List<Kelimeler>kelimelerList;

    public KelimelerAdapter() {
    }

    @NonNull
    @Override
    public CardTasarimTutucu onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        View view = LayoutInflater.from(parent.getContext()).inflate(R.layout.card_tasarim,parent,false);

        return new CardTasarimTutucu(view);
    }

    @Override
    public void onBindViewHolder(@NonNull CardTasarimTutucu holder, int position) {
        Kelimeler kelime = kelimelerList.get(position);

        holder.textViewingilizce.setText(kelime.getIngilizce());
        holder.textViewTurkce.setText(kelime.getTurkce());

        holder.kelime_card.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {

                Intent intent = new Intent(mContext,DetayActivity.class);

                intent.putExtra("nesne",kelime);

                mContext.startActivity(intent);
            }
        });

    }

    @Override
    public int getItemCount() {
        return kelimelerList.size();
    }

    public KelimelerAdapter(Context mContext, List<Kelimeler> kelimelerList) {
        this.mContext = mContext;
        this.kelimelerList = kelimelerList;
    }

    public class CardTasarimTutucu extends RecyclerView.ViewHolder {
        private TextView textViewTurkce;
        private TextView textViewingilizce;
        private CardView kelime_card;

        public CardTasarimTutucu(@NonNull View itemView) {
            super(itemView);
            textViewTurkce = itemView.findViewById(R.id.textViewTurkce);
            textViewingilizce = itemView.findViewById(R.id.textViewIngilizce);
            kelime_card = itemView.findViewById(R.id.kelime_card);
        }
    }

}
```
* kelimelerDao
```
package com.example.szlkuygulamas;

import android.annotation.SuppressLint;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;

import java.util.ArrayList;

public class kelimelerDao {

    public ArrayList<Kelimeler> tumKelimeler(Veritabani vt) {
        ArrayList<Kelimeler> kelimelerArrayList = new ArrayList<>();

        SQLiteDatabase db = vt.getWritableDatabase();

        Cursor c = db.rawQuery("SELECT * FROM kelimeler", null);

        while (c.moveToNext()) {
            @SuppressLint("Range") Kelimeler k = new Kelimeler(c.getInt(c.getColumnIndex("kelime_id"))
                    ,c.getString(c.getColumnIndex("ingilizce"))
                    ,c.getString(c.getColumnIndex("turkce")));

            kelimelerArrayList.add(k);
        }

        return kelimelerArrayList;

    }

    public ArrayList<Kelimeler> kelimeAra(Veritabani vt,String aramaKelime) {
        ArrayList<Kelimeler> kelimelerArrayList = new ArrayList<>();

        SQLiteDatabase db = vt.getWritableDatabase();

        Cursor c = db.rawQuery("SELECT * FROM kelimeler WHERE ingilizce like '%"+aramaKelime+"%'", null);

        while (c.moveToNext()) {
            @SuppressLint("Range") Kelimeler k = new Kelimeler(c.getInt(c.getColumnIndex("kelime_id"))
                    ,c.getString(c.getColumnIndex("ingilizce"))
                    ,c.getString(c.getColumnIndex("turkce")));

            kelimelerArrayList.add(k);
        }

        return kelimelerArrayList;

    }
}
```
* Veritabani
```
package com.example.szlkuygulamas;

import android.content.Context;
import android.database.sqlite.SQLiteDatabase;
import android.database.sqlite.SQLiteOpenHelper;

import androidx.annotation.Nullable;

public class Veritabani extends SQLiteOpenHelper {


    public Veritabani(@Nullable Context context) {
        super(context, "sozluk.sqlite", null, 1);
    }

    @Override
    public void onCreate(SQLiteDatabase db) {

        db.execSQL("CREATE TABLE IF NOT EXISTS `kelimeler` (\n" +
                "\t`kelime_id`\tINTEGER PRIMARY KEY AUTOINCREMENT,\n" +
                "\t`ingilizce`\tTEXT,\n" +
                "\t`turkce`\tTEXT\n" +
                ")");

    }

    @Override
    public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {
        db.execSQL("DROP TABLE IF EXISTS kelimeler");
        onCreate(db);
    }
}
```
* DetayActivity
```
package com.example.szlkuygulamas;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.widget.TextView;

public class DetayActivity extends AppCompatActivity {
    private TextView textTurkce,textingilizce;
    private Kelimeler kelime;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_detay);

        textingilizce = findViewById(R.id.textViewingilizce);
        textTurkce = findViewById(R.id.textViewturkce);

        kelime = (Kelimeler) getIntent().getSerializableExtra("nesne");

        textingilizce.setText(kelime.getIngilizce());
        textTurkce.setText(kelime.getTurkce());

    }
}
```
* DatabaseCopyHelper
```
package com.example.szlkuygulamas;

import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;

import android.content.Context;
import android.database.SQLException;
import android.database.sqlite.SQLiteDatabase;
import android.database.sqlite.SQLiteException;
import android.database.sqlite.SQLiteOpenHelper;

public class DatabaseCopyHelper extends SQLiteOpenHelper  {


	//The Android's default system path of your application database.
    String DB_PATH =null;

    private static String DB_NAME = "sozluk.sqlite";

    private SQLiteDatabase myDataBase;

    private final Context myContext;

    /**
     * Constructor
     * Takes and keeps a reference of the passed context in order to access to the application assets and resources.
     * @param context
     */
    public DatabaseCopyHelper(Context context) {

    	super(context, DB_NAME, null, 1);
        this.myContext = context;
        DB_PATH="/data/data/"+context.getPackageName()+"/"+"databases/";

    }

  /**
     * Creates a empty database on the system and rewrites it with your own database.
     * */
    public void createDataBase() throws IOException{

    	boolean dbExist = checkDataBase();

    	if(dbExist){
    		//do nothing - database already exist
    	}else{

    		//By calling this method and empty database will be created into the default system path
               //of your application so we are gonna be able to overwrite that database with our database.
        	this.getReadableDatabase();

        	try {

    			copyDataBase();

    		} catch (IOException e) {

        		throw new Error("Error copying database");

        	}
    	}

    }

    /**
     * Check if the database already exist to avoid re-copying the file each time you open the application.
     * @return true if it exists, false if it doesn't
     */
    private boolean checkDataBase(){

    	SQLiteDatabase checkDB = null;

    	try{
    		String myPath = DB_PATH + DB_NAME;
    		checkDB = SQLiteDatabase.openDatabase(myPath, null, SQLiteDatabase.OPEN_READONLY);

    	}catch(SQLiteException e){

    		//database does't exist yet.

    	}

    	if(checkDB != null){

    		checkDB.close();

    	}

    	return checkDB != null ? true : false;
    }

    /**
     * Copies your database from your local assets-folder to the just created empty database in the
     * system folder, from where it can be accessed and handled.
     * This is done by transfering bytestream.
     * */
    private void copyDataBase() throws IOException{

    	//Open your local db as the input stream
    	InputStream myInput = myContext.getAssets().open(DB_NAME);


    	// Path to the just created empty db
    	String outFileName = DB_PATH + DB_NAME;

    	//Open the empty db as the output stream
    	OutputStream myOutput = new FileOutputStream(outFileName);

    	//transfer bytes from the inputfile to the outputfile
    	byte[] buffer = new byte[1024];
    	int length;
    	while ((length = myInput.read(buffer))>0){
    		myOutput.write(buffer, 0, length);
    	}

    	//Close the streams
    	myOutput.flush();
    	myOutput.close();
    	myInput.close();

    }

    public void openDataBase() throws SQLException{

    	//Open the database
        String myPath = DB_PATH + DB_NAME;
    	myDataBase = SQLiteDatabase.openDatabase(myPath, null, SQLiteDatabase.OPEN_READONLY);


    }

    @Override
	public synchronized void close() {

    	    if(myDataBase != null)
    		    myDataBase.close();

    	    super.close();

	}



	@Override
	public void onCreate(SQLiteDatabase db) {

	}

	@Override
	public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {

	}

	@Override
	public void onOpen(SQLiteDatabase db) {
		super.onOpen(db);
		db.disableWriteAheadLogging();
	}
 //return cursor

}
```
* activity_detay.xml
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".DetayActivity">

    <TextView
        android:id="@+id/textViewingilizce"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="186dp"
        android:text="İngilizce"
        android:textSize="40sp"
        android:textStyle="bold"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <TextView
        android:id="@+id/textViewturkce"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginBottom="276dp"
        android:text="Türkçe"
        android:textSize="40sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent" />
</androidx.constraintlayout.widget.ConstraintLayout>
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

    <androidx.appcompat.widget.Toolbar
        android:id="@+id/toolbar"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:background="?attr/colorPrimary"
        android:minHeight="?attr/actionBarSize"
        android:theme="?attr/actionBarTheme"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/rv"
        android:layout_width="0dp"
        android:layout_height="0dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/toolbar" />
</androidx.constraintlayout.widget.ConstraintLayout>
```
* card_tasarim.xml
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="wrap_content">

    <androidx.cardview.widget.CardView
        android:id="@+id/kelime_card"
        android:layout_width="match_parent"
        android:layout_height="50dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" >

        <androidx.constraintlayout.widget.ConstraintLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent">

            <TextView
                android:id="@+id/textViewIngilizce"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="İngilizce"
                android:textStyle="bold"
                app:layout_constraintBottom_toBottomOf="parent"
                app:layout_constraintEnd_toStartOf="@+id/textViewTurkce"
                app:layout_constraintHorizontal_bias="0.5"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toTopOf="parent"
                app:layout_constraintVertical_bias="0.5" />

            <TextView
                android:id="@+id/textViewTurkce"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:rotationY="0"
                android:text="Türkçe"
                app:layout_constraintBottom_toBottomOf="parent"
                app:layout_constraintEnd_toEndOf="parent"
                app:layout_constraintHorizontal_bias="0.5"
                app:layout_constraintStart_toEndOf="@+id/textViewIngilizce"
                app:layout_constraintTop_toTopOf="parent"
                app:layout_constraintVertical_bias="0.5" />
        </androidx.constraintlayout.widget.ConstraintLayout>
    </androidx.cardview.widget.CardView>
</androidx.constraintlayout.widget.ConstraintLayout>
```
* toolbar_menu.xml
```
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:android="http://schemas.android.com/apk/res/android">

    <item
        android:id="@+id/action_ara"
        android:icon="@drawable/baseline_search_24"
        android:title="Ara"
        app:actionViewClass="androidx.appcompat.widget.SearchView"
        app:showAsAction="always|collapseActionView" />
</menu>
```
# Bayrak Uygulaması
![Bayrak](https://user-images.githubusercontent.com/101557027/230773535-ce5d53c4-0065-45c9-854c-4c796fc437c5.gif)
* MainActivity
```
package com.example.bayrakuygulamasi;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;

import java.io.IOException;

public class MainActivity extends AppCompatActivity {
    private Button buttonBasla;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        buttonBasla = findViewById(R.id.buttonBasla);

        veritabaniKopyala();

        buttonBasla.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                startActivity(new Intent(MainActivity.this,QuizActivity.class));
            }
        });
    }

    public void veritabaniKopyala() {
        DatabaseCopyHelper helper = new DatabaseCopyHelper(this);

        try {
            helper.createDataBase();
        } catch (IOException e) {
            e.printStackTrace();
        }

        helper.openDataBase();
    }
}
```
* Bayraklar
```
package com.example.bayrakuygulamasi;

public class Bayraklar {
    private int bayrak_id;
    private String bayrak_ad;
    private String bayrak_resim;

    public Bayraklar() {
    }

    public Bayraklar(int bayrak_id, String bayrak_ad, String bayrak_resim) {
        this.bayrak_id = bayrak_id;
        this.bayrak_ad = bayrak_ad;
        this.bayrak_resim = bayrak_resim;
    }

    public int getBayrak_id() {
        return bayrak_id;
    }

    public void setBayrak_id(int bayrak_id) {
        this.bayrak_id = bayrak_id;
    }

    public String getBayrak_ad() {
        return bayrak_ad;
    }

    public void setBayrak_ad(String bayrak_ad) {
        this.bayrak_ad = bayrak_ad;
    }

    public String getBayrak_resim() {
        return bayrak_resim;
    }

    public void setBayrak_resim(String bayrak_resim) {
        this.bayrak_resim = bayrak_resim;
    }
}

```
* BayraklarDao
```
package com.example.bayrakuygulamasi;

import android.annotation.SuppressLint;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;

import java.util.ArrayList;

public class BayraklarDao {

    public ArrayList<Bayraklar> rasgele5Getir(Veritabani vt) {
        ArrayList<Bayraklar> bayraklarArrayList = new ArrayList<>();
        SQLiteDatabase db = vt.getWritableDatabase();
        Cursor c = db.rawQuery("SELECT * FROM bayraklar ORDER BY RANDOM() LIMIT 5", null);

        while (c.moveToNext()) {
            @SuppressLint("Range") Bayraklar b = new Bayraklar(c.getInt(c.getColumnIndex("bayrak_id"))
                    ,c.getString(c.getColumnIndex("bayrak_ad"))
                    ,c.getString(c.getColumnIndex("bayrak_resim")));

            bayraklarArrayList.add(b);
        }

        return bayraklarArrayList;
    }

    public ArrayList<Bayraklar> rasgele3YanlisSecenekGetir(Veritabani vt,int bayrak_id) {
        ArrayList<Bayraklar> bayraklarArrayList = new ArrayList<>();
        SQLiteDatabase db = vt.getWritableDatabase();
        Cursor c = db.rawQuery("SELECT * FROM bayraklar WHERE bayrak_id != "+bayrak_id+" ORDER BY RANDOM() LIMIT 3", null);

        while (c.moveToNext()) {
            @SuppressLint("Range") Bayraklar b = new Bayraklar(c.getInt(c.getColumnIndex("bayrak_id"))
                    ,c.getString(c.getColumnIndex("bayrak_ad"))
                    ,c.getString(c.getColumnIndex("bayrak_resim")));

            bayraklarArrayList.add(b);
        }

        return bayraklarArrayList;
    }
}
```
* DatabaseCopyHelper
```
package com.example.bayrakuygulamasi;

import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;

import android.content.Context;
import android.database.SQLException;
import android.database.sqlite.SQLiteDatabase;
import android.database.sqlite.SQLiteException;
import android.database.sqlite.SQLiteOpenHelper;

public class DatabaseCopyHelper extends SQLiteOpenHelper  {


	//The Android's default system path of your application database.
	String DB_PATH =null;

	private static String DB_NAME = "bayrakquiz.sqlite";

	private SQLiteDatabase myDataBase;

	private final Context myContext;

	/**
	 * Constructor
	 * Takes and keeps a reference of the passed context in order to access to the application assets and resources.
	 * @param context
	 */
	public DatabaseCopyHelper(Context context) {

		super(context, DB_NAME, null, 1);
		this.myContext = context;
		DB_PATH="/data/data/"+context.getPackageName()+"/"+"databases/";

	}

	/**
	 * Creates a empty database on the system and rewrites it with your own database.
	 * */
	public void createDataBase() throws IOException{

		boolean dbExist = checkDataBase();

		if(dbExist){
			//do nothing - database already exist
		}else{

			//By calling this method and empty database will be created into the default system path
			//of your application so we are gonna be able to overwrite that database with our database.
			this.getReadableDatabase();

			try {

				copyDataBase();

			} catch (IOException e) {

				throw new Error("Error copying database");

			}
		}

	}

	/**
	 * Check if the database already exist to avoid re-copying the file each time you open the application.
	 * @return true if it exists, false if it doesn't
	 */
	private boolean checkDataBase(){

		SQLiteDatabase checkDB = null;

		try{
			String myPath = DB_PATH + DB_NAME;
			checkDB = SQLiteDatabase.openDatabase(myPath, null, SQLiteDatabase.OPEN_READONLY);

		}catch(SQLiteException e){

			//database does't exist yet.

		}

		if(checkDB != null){

			checkDB.close();

		}

		return checkDB != null ? true : false;
	}

	/**
	 * Copies your database from your local assets-folder to the just created empty database in the
	 * system folder, from where it can be accessed and handled.
	 * This is done by transfering bytestream.
	 * */
	private void copyDataBase() throws IOException{

		//Open your local db as the input stream
		InputStream myInput = myContext.getAssets().open(DB_NAME);


		// Path to the just created empty db
		String outFileName = DB_PATH + DB_NAME;

		//Open the empty db as the output stream
		OutputStream myOutput = new FileOutputStream(outFileName);

		//transfer bytes from the inputfile to the outputfile
		byte[] buffer = new byte[1024];
		int length;
		while ((length = myInput.read(buffer))>0){
			myOutput.write(buffer, 0, length);
		}

		//Close the streams
		myOutput.flush();
		myOutput.close();
		myInput.close();

	}

	public void openDataBase() throws SQLException{

		//Open the database
		String myPath = DB_PATH + DB_NAME;
		myDataBase = SQLiteDatabase.openDatabase(myPath, null, SQLiteDatabase.OPEN_READONLY);


	}

	@Override
	public synchronized void close() {

		if(myDataBase != null)
			myDataBase.close();

		super.close();

	}



	@Override
	public void onCreate(SQLiteDatabase db) {

	}

	@Override
	public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {

	}

	@Override
	public void onOpen(SQLiteDatabase db) {
		super.onOpen(db);
		db.disableWriteAheadLogging();
	}
	//return cursor

}
```
* QuizActivity
```
package com.example.bayrakuygulamasi;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.os.Bundle;
import android.os.Handler;
import android.view.View;
import android.widget.Button;
import android.widget.ImageView;
import android.widget.TextView;
import android.widget.Toast;

import java.util.ArrayList;
import java.util.HashSet;

public class QuizActivity extends AppCompatActivity {
    private TextView textViewDogru,textViewYanlis,textViewSoruSayisi;
    private ImageView imageViewBayrak;
    private Button buttonA,buttonB,buttonC,buttonD;
    private ArrayList<Bayraklar> sorularListe;
    private ArrayList<Bayraklar> yanlisSeceneklerListe;
    private Bayraklar dogruSoru;
    private Veritabani vt;
    // Sayaç
    private int soruSayac = 0;
    private int yanlisSayac = 0;
    private int dogruSayac = 0;
    //Secenekleri
    private HashSet<Bayraklar> secenekleriKaristirmaListe = new HashSet<>();
    private ArrayList<Bayraklar> seceneklerListe = new ArrayList<>();
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_quiz);

        textViewDogru = findViewById(R.id.textViewDogru);
        textViewYanlis = findViewById(R.id.textViewYanlis);
        textViewSoruSayisi = findViewById(R.id.textViewSoruSayi);
        imageViewBayrak = findViewById(R.id.imageViewBayrak);
        buttonA = findViewById(R.id.buttonA);
        buttonB = findViewById(R.id.buttonB);
        buttonC = findViewById(R.id.buttonC);
        buttonD = findViewById(R.id.buttonD);
        
        vt = new Veritabani(this);
        Handler handler = new Handler();

        sorularListe = new BayraklarDao().rasgele5Getir(vt);

        soruYukle();

        buttonA.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if(dogruSoru.getBayrak_ad() != buttonA.getText()) {
                    Toast.makeText(getApplicationContext(), "Doğru Cevap :" + dogruSoru.getBayrak_ad(), Toast.LENGTH_SHORT).show();
                    handler.postDelayed(new Runnable() {
                        @Override
                        public void run() {
                            dogruKontrol(buttonA);
                            sayacKontrol();
                        }
                    }, 2000);
                } else if (dogruSoru.getBayrak_ad() == buttonA.getText()) {
                    dogruKontrol(buttonA);
                    sayacKontrol();
                }

            }
        });

        buttonB.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if(dogruSoru.getBayrak_ad() != buttonB.getText()) {
                    Toast.makeText(getApplicationContext(), "Doğru Cevap :" + dogruSoru.getBayrak_ad(), Toast.LENGTH_SHORT).show();
                    handler.postDelayed(new Runnable() {
                        @Override
                        public void run() {
                            dogruKontrol(buttonB);
                            sayacKontrol();
                        }
                    }, 2000);
                } else if (dogruSoru.getBayrak_ad() == buttonB.getText()) {
                    dogruKontrol(buttonB);
                    sayacKontrol();
                }
            }
        });

        buttonC.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if(dogruSoru.getBayrak_ad() != buttonC.getText()) {
                    Toast.makeText(getApplicationContext(), "Doğru Cevap :" + dogruSoru.getBayrak_ad(), Toast.LENGTH_SHORT).show();
                    handler.postDelayed(new Runnable() {
                        @Override
                        public void run() {
                            dogruKontrol(buttonC);
                            sayacKontrol();
                        }
                    }, 2000);
                } else if (dogruSoru.getBayrak_ad() == buttonC.getText()) {
                    dogruKontrol(buttonC);
                    sayacKontrol();
                }
            }
        });

        buttonD.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if(dogruSoru.getBayrak_ad() != buttonD.getText()) {
                    Toast.makeText(getApplicationContext(), "Doğru Cevap :" + dogruSoru.getBayrak_ad(), Toast.LENGTH_SHORT).show();
                    handler.postDelayed(new Runnable() {
                        @Override
                        public void run() {
                            dogruKontrol(buttonD);
                            sayacKontrol();
                        }
                    }, 2000);
                } else if (dogruSoru.getBayrak_ad() == buttonD.getText()) {
                    dogruKontrol(buttonD);
                    sayacKontrol();
                }
            }
        });

    }

    public void soruYukle() {

        textViewSoruSayisi.setText((soruSayac+1)+". SORU");

        dogruSoru = sorularListe.get(soruSayac);

        yanlisSeceneklerListe = new BayraklarDao().rasgele3YanlisSecenekGetir(vt,dogruSoru.getBayrak_id());

        imageViewBayrak.setImageResource(getResources().getIdentifier(dogruSoru.getBayrak_resim()
                ,"drawable",getPackageName()));

        secenekleriKaristirmaListe.clear();
        secenekleriKaristirmaListe.add(dogruSoru);
        secenekleriKaristirmaListe.add(yanlisSeceneklerListe.get(0));
        secenekleriKaristirmaListe.add(yanlisSeceneklerListe.get(1));
        secenekleriKaristirmaListe.add(yanlisSeceneklerListe.get(2));

        seceneklerListe.clear();

        for (Bayraklar b: secenekleriKaristirmaListe) {
            seceneklerListe.add(b);
        }

        buttonA.setText(seceneklerListe.get(0).getBayrak_ad());
        buttonB.setText(seceneklerListe.get(1).getBayrak_ad());
        buttonC.setText(seceneklerListe.get(2).getBayrak_ad());
        buttonD.setText(seceneklerListe.get(3).getBayrak_ad());
    }

    public void dogruKontrol (Button button) {

        String buttonYazi = button.getText().toString();
        String dogruCevap = dogruSoru.getBayrak_ad();

        if(buttonYazi.equals(dogruCevap)) {
            dogruSayac++;
        }else {
            yanlisSayac++;
        }

        textViewDogru.setText("Doğru : "+dogruSayac);
        textViewYanlis.setText("Yanlış : "+yanlisSayac);
    }

    public void sayacKontrol(){
        soruSayac++;

        if (soruSayac != 5){
            soruYukle();
        }else {
            Intent intent = new Intent(QuizActivity.this,ResaultActivity.class);
            intent.putExtra("dogruSayac",dogruSayac);
            startActivity(intent);
            finish();





        }
    }
}
```
* ResaultActivity
```
package com.example.bayrakuygulamasi;

import androidx.appcompat.app.AppCompatActivity;

import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;

public class ResaultActivity extends AppCompatActivity {
    private TextView textViewSonuc,textViewYuzdeSonuc;
    private Button buttonTekrar;
    private int dogruSayac;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_resault);

        textViewSonuc = findViewById(R.id.textViewSonuc);
        textViewYuzdeSonuc = findViewById(R.id.textViewYuzdeSonuc);
        buttonTekrar = findViewById(R.id.buttonTekrar);

        dogruSayac = getIntent().getIntExtra("dogruSayac",0);

        textViewSonuc.setText(dogruSayac+ " DOĞRU "+(5-dogruSayac)+" YANLIŞ");
        textViewYuzdeSonuc.setText("% "+(dogruSayac*100)/5+" BAŞARI");

        buttonTekrar.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                startActivity(new Intent(ResaultActivity.this,MainActivity.class));
                finish();
            }
        });
    }
}
```
* Veritabani
```
package com.example.bayrakuygulamasi;

import android.content.Context;
import android.database.sqlite.SQLiteDatabase;
import android.database.sqlite.SQLiteOpenHelper;

import androidx.annotation.Nullable;

public class Veritabani extends SQLiteOpenHelper {
    public Veritabani(@Nullable Context context) {
        super(context,"bayrakquiz.sqlite",null,1);
    }

    @Override
    public void onCreate(SQLiteDatabase db) {
        db.execSQL("CREATE TABLE IF NOT EXISTS \"bayraklar\" (\n" +
                "\t`bayrak_id`\tINTEGER PRIMARY KEY AUTOINCREMENT,\n" +
                "\t`bayrak_ad`\tTEXT,\n" +
                "\t`bayrak_resim`\tTEXT\n" +
                ")");
    }

    @Override
    public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {
        db.execSQL("DROP TABLE IF EXIXTS bayraklar");
        onCreate(db);

    }
}
```
* activity_quiz.xml
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".QuizActivity">

    <TextView
        android:id="@+id/textViewDogru"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginStart="50dp"
        android:layout_marginTop="32dp"
        android:text="Doğru : 0"
        android:textSize="20sp"
        app:layout_constraintEnd_toStartOf="@+id/textViewYanlis"
        app:layout_constraintHorizontal_bias="0.0"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <TextView
        android:id="@+id/textViewYanlis"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="32dp"
        android:layout_marginEnd="50dp"
        android:text="Yanlış : 0"
        android:textSize="20sp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <TextView
        android:id="@+id/textViewSoruSayi"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="10dp"
        android:text="1. Soru"
        android:textSize="34sp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textViewDogru" />

    <ImageView
        android:id="@+id/imageViewBayrak"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="18dp"
        android:layout_marginBottom="15dp"
        app:layout_constraintBottom_toTopOf="@+id/buttonA"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textViewSoruSayi"
        app:srcCompat="@drawable/turkiye" />

    <Button
        android:id="@+id/buttonD"
        android:layout_width="246dp"
        android:layout_height="46dp"
        android:layout_marginBottom="25dp"
        android:text="Japonya"
        android:textAlignment="viewStart"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent" />

    <Button
        android:id="@+id/buttonC"
        android:layout_width="246dp"
        android:layout_height="46dp"
        android:layout_marginBottom="15dp"
        android:text="Almanya"
        android:textAlignment="viewStart"
        app:layout_constraintBottom_toTopOf="@+id/buttonD"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent" />

    <Button
        android:id="@+id/buttonB"
        android:layout_width="246dp"
        android:layout_height="46dp"
        android:layout_marginBottom="15dp"
        android:text="İtalya"
        android:textAlignment="viewStart"
        app:layout_constraintBottom_toTopOf="@+id/buttonC"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent" />

    <Button
        android:id="@+id/buttonA"
        android:layout_width="246dp"
        android:layout_height="46dp"
        android:layout_marginBottom="15dp"
        android:text="Türkiye"
        android:textAlignment="viewStart"
        app:layout_constraintBottom_toTopOf="@+id/buttonB"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
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
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="QUİZ HOŞGELDİNİZ"
        android:textSize="24sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.308" />

    <Button
        android:id="@+id/buttonBasla"
        android:layout_width="173dp"
        android:layout_height="52dp"
        android:layout_marginBottom="180dp"
        android:text="Başla"
        android:textSize="24sp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
```
* activity_resault.xml
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".ResaultActivity">

    <TextView
        android:id="@+id/textViewSonuc"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="154dp"
        android:text=" 5 DOĞRU 1 YANLIŞ"
        android:textSize="30sp"
        android:textStyle="bold"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <TextView
        android:id="@+id/textViewYuzdeSonuc"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="63dp"
        android:text="% 25 BAŞARI"
        android:textColor="#E80505"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textViewSonuc" />

    <Button
        android:id="@+id/buttonTekrar"
        android:layout_width="175dp"
        android:layout_height="49dp"
        android:layout_marginTop="139dp"
        android:text="TEKRAR DENE"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textViewYuzdeSonuc" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

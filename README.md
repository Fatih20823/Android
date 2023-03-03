# Android

# VievBinding
 => build.gradle
 
     buildFeatures {
           viewBinding = true
     }
     
     import androidx.appcompat.app.AppCompatActivity;

import android.app.Activity;
import android.os.Bundle;

import com.example.viewbinding.databinding.ActivityMainBinding;
import com.google.android.material.snackbar.Snackbar;

public class MainActivity extends AppCompatActivity {

    private ActivityMainBinding tasarim;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        tasarim = ActivityMainBinding.inflate(getLayoutInflater());
        setContentView(tasarim.getRoot());

        tasarim.buttonYap.setOnClickListener(view -> {
            Snackbar.make(view,"Merhaba",Snackbar.LENGTH_SHORT).show();
        });
    }
}

# Yasam Dongusu

![Yaşam Döngüsü](https://user-images.githubusercontent.com/101557027/219966294-2fce10c1-9cc7-4d5d-b237-07969716d315.jpg)

 # Sayfalar Arası Geçiş
 ![Intent](https://user-images.githubusercontent.com/101557027/219968962-7d387c21-e9a7-47ac-be7d-bc5aca358c6d.gif)
 
 * Android studioda kod yazarken başka Activity arasında geçişler yapmamız gerekebilir
 * burda dikkat etmeniz gereken nokta ” MainActivity ” yerine sizde hangi activity gözükücek ise onun adını yazmanı gereklidir.

public class MainActivity extends AppCompatActivity {
    private Button buttonGotoB;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        buttonGotoB = findViewById(R.id.buttonGotoB);

        buttonGotoB.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent yeniIntent = new Intent(MainActivity.this,ActivityB.class);

                startActivity(yeniIntent);
            }
        });
    }
}

# Sayfalar Arası Veri Taşıma

![Untitled](https://user-images.githubusercontent.com/101557027/222516961-792b37d9-512c-4b4c-a906-bcb496fab226.gif)
-----------
* MainActivity
public class MainActivity extends AppCompatActivity {
    private Button buttonGotoB;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        buttonGotoB = findViewById(R.id.buttonGotoB);

        buttonGotoB.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {

                Kisiler kisi = new Kisiler(9999,"Ahmet",1.87);

                Intent yeniIntent = new Intent(MainActivity.this,ActivityB.class);

                yeniIntent.putExtra("mesaj","merhaba");
                yeniIntent.putExtra("yas",18);
                yeniIntent.putExtra("boy",1.78);

                yeniIntent.putExtra("nesne",kisi);

                startActivity(yeniIntent);
            }
        });
    }
}

* ActivityB
-----------
public class ActivityB extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_b);

        String gelenMesaj = getIntent().getStringExtra("mesaj");
        int gelenYas = getIntent().getIntExtra("yas",0);
        double gelenBoy = getIntent().getDoubleExtra("boy",0.0);

        Kisiler gelenKisi = (Kisiler) getIntent().getSerializableExtra("nesne");

        Log.e("Gelen Mesaj",gelenMesaj);
        Log.e("Gelen Yas",String.valueOf(gelenYas));
        Log.e("Gelen Boy",String.valueOf(gelenBoy));

        Log.e("Gelen TcNo",String.valueOf(gelenKisi.getTcno()));
        Log.e("Gelen İsim",gelenKisi.getIsim());
        Log.e("Gelen Kisi boy",String.valueOf(gelenKisi.getBoy()));
    }
}
-----------
* KisilerClass
-------
public class Kisiler implements Serializable {
    private int tcno;
    private String isim;
    private double boy;
    public Kisiler() {
    }

    public Kisiler(int tcno, String isim, double boy) {
        this.tcno = tcno;
        this.isim = isim;
        this.boy = boy;
    }

    public int getTcno() {
        return tcno;
    }

    public void setTcno(int tcno) {
        this.tcno = tcno;
    }

    public String getIsim() {
        return isim;
    }

    public void setIsim(String isim) {
        this.isim = isim;
    }

    public double getBoy() {
        return boy;
    }

    public void setBoy(double boy) {
        this.boy = boy;
    }
}
---------

# Veri Taşıma Görsel Nesne

![Veritasıma](https://user-images.githubusercontent.com/101557027/222669576-994507d5-22a3-4d54-94d6-576a4f91a5f8.gif)
-------------------
* MainActivity
------------------
public class MainActivity extends AppCompatActivity {
    private EditText editTextGirdi;
    private Button buttonGonder;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        editTextGirdi = findViewById(R.id.editTextGirdi);
        buttonGonder = findViewById(R.id.buttonGonder);

        buttonGonder.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                String veri = editTextGirdi.getText().toString();

                Intent yeniIntent = new Intent(MainActivity.this,ActivityB.class);
                yeniIntent.putExtra("mesaj",veri);

                startActivity(yeniIntent);
            }
        });
    }
}
---------------
* ActivityB
---------------
public class ActivityB extends AppCompatActivity {
    private TextView textViewCikti;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_b);

        textViewCikti = findViewById(R.id.textViewCikti);

        String gelenVeri = getIntent().getStringExtra("mesaj");

        textViewCikti.setText(gelenVeri);
    }
}

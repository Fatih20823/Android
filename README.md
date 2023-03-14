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

# BackStack Uygulaması

![BackStack](https://user-images.githubusercontent.com/101557027/222724919-8e7e84c6-e8de-4d13-be5c-57eede4ddef9.gif)

Sırayla a, b, c ve d fragmentlarını ekleyerek kullanıcıların detay sayfalarını açmasını sağladık. Fakat kullanıcılar geri butonuna basarak anasayfaya gitmek isteyecektir. Normal şartlarda fragment eklemediğimiz durumda bir Activity den diğer Activity e geçtiğimizde, geri butonuna bastığımızda bir önceki Activity e gitmek yerine uygulama arkaplana atılır. Bu aslında istemediğimiz bir durumdur.

Daha iyi bir kullanıcı deneyimi sağlamak için yardımımıza fragmentlar ve backstack kavramı koşar. Activity state e eklediğiniz fragmentları cacheleyerek(önbellek) yeniden fragment yaratmak yerine hem memory den tasarruf eder, hem de esnek bir kullanıcı arayüzü sağlayabilirsiniz.

* MainActivity
-----------------
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

                startActivity(new Intent(MainActivity.this,ActivityB.class));
            }
        });
    }
}
--------------
* ActivityB
--------------
public class ActivityB extends AppCompatActivity {
    private Button buttonGotoC;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_b);

        buttonGotoC = findViewById(R.id.buttonGotoC);

        buttonGotoC.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {

                startActivity(new Intent(ActivityB.this,ActivityC.class));
            }
        });
    }
}
-------------
* ActivityC
-------------
public class ActivityC extends AppCompatActivity {
    private Button buttonGotoD;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_c);

        buttonGotoD = findViewById(R.id.buttonGotoD);

        buttonGotoD.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                startActivity(new Intent(ActivityC.this,ActivityD.class));
            }
        });
    }
}
------------
* ActivityD
------------
public class ActivityD extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_d);
    }

    @Override
    public void onBackPressed() {

        Intent ıntent = new Intent(ActivityD.this,ActivityB.class);

        ıntent.addFlags(Intent.FLAG_ACTIVITY_CLEAR_TOP);

        startActivity(ıntent);
    }
}
------------
 # finish() Metodu 
* Finish () kodu aktivite içerisinde ne yapmaktadır?
Intent başladıktan sonra aktivitenin ölmesi istenirse finish() metodunu kullanılır.
Gidilen aktiviteden geri dönmek istendiğinde bu aktivite öleceği için çalışmaz.
---------------
![Finish__](https://user-images.githubusercontent.com/101557027/222902373-0fbf209c-26b1-4f49-859d-1ca5c21c0886.gif)
---------------
* ActivityOyunEkranı
----------------
 public class ActivityOyunEkrani extends AppCompatActivity {
    private Button buttonBitir;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_oyun_ekrani);

        buttonBitir = findViewById(R.id.buttonBitir);

        buttonBitir.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                startActivity(new Intent(ActivityOyunEkrani.this,ActivitySonuc.class));
                finish();
            }
        });
    }
}

# Fragment
----------
![Fragment](https://user-images.githubusercontent.com/101557027/225091816-f8949955-65ad-4a45-baae-8edc081a7af3.gif)
* Fragment’ları, Activity üzerine yapıştırılan Post-It’ ler gibi düşünün. Bir Activity’de istediğiniz kadar Fragment kullanabilirsiniz ve dilerseniz üst üste yapıştırılan kağıtlar gibi Fragment üzerine Fragment ekleyebilirsiniz, çıkarabilirsiniz veya başka bir Fragment ile değiştirebilirsiniz. Fragmentler arası veri akışını da gerçekleştirebilirsiniz.
![Fragments](https://user-images.githubusercontent.com/101557027/225094346-888fa52e-fbcb-4acb-9339-68ffea8c8e10.png)
* Activity ile Fragmentlerin Farkı Nedir?
Activity, uygulamanın ön planda görünen ve arka planda çalışan bölümüdür. XML türünde bir layout dosyası ve Java dilinde bir class’dan meydana gelir. Her bir Activty’nin kendine ait bir yaşam döngüsü (life-cycle) vardır.

![yapi](https://user-images.githubusercontent.com/101557027/225094837-83315e98-601e-4c61-b345-bca256f6c6e4.jpg)
* Bir Activity çalıştırılmaya başladığı zaman, ilgili Activity’nin class’ına ait onCreate(), onStart() ve onResume() methodları, sırasıyla çalışmaya başlar ve kapatıldığı zaman, sırasıyla onPause(), onStop() ve onDestroy() methodları çalışır. Dilerseniz bu methodları Override edip yapılmasını istediğiniz işlemleri bu anlarda yaptırabilirsiniz.

* Fragment’lar aynı Activity’ler gibi bir class ve layout dosyasından oluşurlar. Fragment’ların en büyük avantajı çok daha hızlı ve performanslı olmalarıdır ve aynı ekranda iki farklı Activity çalıştırılamazken dilediğiniz kadar Fragment çalışabilir. Fakat bir Fragment tek başına çalıştırılamaz, çalışabilmesi için bir Activity’e ihtiyaç duyar.
-----------------
* MainActivity
-----------------
```
import androidx.appcompat.app.AppCompatActivity;
import androidx.fragment.app.FragmentManager;
import androidx.fragment.app.FragmentTransaction;

import android.os.Bundle;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        FragmentManager fm = getSupportFragmentManager();
        FragmentTransaction ft = fm.beginTransaction();

        ft.add(R.id.fragment_tutucu1,new FragmentBirinci());
        ft.add(R.id.fragment_tutucu2,new Fragmentikinci());

        ft.commit();
    }
}
```

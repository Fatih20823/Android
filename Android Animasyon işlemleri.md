# Animasyon Giriş
![Animgiris2](https://github.com/Fatih20823/Android/assets/101557027/52b61e32-6c1b-4e98-8d5d-05513bc3a968)
* MainActivity
```
package com.example.animasyongiris;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.view.animation.Animation;
import android.view.animation.AnimationUtils;
import android.widget.Button;

public class MainActivity extends AppCompatActivity {
    private Button button;
    private Animation animasyon;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        button = findViewById(R.id.button);

        animasyon = AnimationUtils.loadAnimation(getApplicationContext(),R.anim.animgiris);

        button.setAnimation(animasyon);

        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                button.startAnimation(animasyon);
            }
        });
    }
}
```
* animgiris.xml
```
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android">

    <translate
        android:duration="3000"
        android:fromXDelta="50%"
        android:toXDelta="100%"/>
</set>
```
# Alpha Animasyonu
![Alpha2](https://github.com/Fatih20823/Android/assets/101557027/c3413dbf-4191-4c2d-8f6b-877af721f431)
<h3>Android:fillAfter</h3>

* Animasyon gerçekleştikten sonra önceki durumuna dönecek mi?
* Genelde hareket animasyonlarında kullanılır.'true' yaparsak eski haline dönmez animasyon gerçekleşir ve animasyon sonucunda oluşmuş halinde kalır.
![AlphaFillAfter](https://github.com/Fatih20823/Android/assets/101557027/4fd1951d-f664-4744-927d-df1d736d6365)

* alphacalisma.xml
```
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android"
    android:fillAfter="true">

    <alpha
        android:fromAlpha="1.0"
        android:toAlpha="0.0"
        android:duration="3000"/>
</set>
```
* MainActivity
```
package com.example.animasyonislemleri;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.view.animation.Animation;
import android.view.animation.AnimationUtils;
import android.widget.Button;

public class MainActivity extends AppCompatActivity {
    private Button button2,buttonYap;
    private Animation animation;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        button2 = findViewById(R.id.button2);
        buttonYap = findViewById(R.id.buttonYap);

        animation = AnimationUtils.loadAnimation(getApplicationContext(),R.anim.alphacalisma);

        buttonYap.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                button2.startAnimation(animation);
            }
        });
    }
}
```
# İnterpolator,RepeatMode ve RepeatCount
![İnterpolator](https://github.com/Fatih20823/Android/assets/101557027/45d53c3a-7426-48a5-b2cc-c9b4c05abcf9)
![repeat](https://github.com/Fatih20823/Android/assets/101557027/f9cf3de3-ab12-4ae7-b334-20fc370b1309)
![ınterpolator](https://github.com/Fatih20823/Android/assets/101557027/69185fdb-dc0b-412e-8feb-4fe389505ff7)
![repeatCount](https://github.com/Fatih20823/Android/assets/101557027/a37d3458-d6ec-48d1-9512-55231bfeb43a)
* blinkcalismasi.xml
```
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android">

    <alpha
        android:duration="1000"
        android:fromAlpha="1.0"
        android:toAlpha="0.0"
        android:repeatMode="reverse"
        android:repeatCount="infinite"
        android:interpolator="@android:anim/bounce_interpolator"/>

</set>
```
# Rotate Animasyonu
![Rotate](https://github.com/Fatih20823/Android/assets/101557027/1df66dee-be9f-4b59-b4dd-1e6b4188051a)
![Rotate](https://github.com/Fatih20823/Android/assets/101557027/1b75f32c-c340-460d-b476-ea6851f1afb0)
* MainActivity
```
package com.example.animasyonislemleri;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.view.animation.Animation;
import android.view.animation.AnimationUtils;
import android.widget.Button;

public class MainActivity extends AppCompatActivity {
    private Button button2,buttonYap;
    private Animation animation;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        button2 = findViewById(R.id.button2);
        buttonYap = findViewById(R.id.buttonYap);

        animation = AnimationUtils.loadAnimation(getApplicationContext(),R.anim.rotatecalismasi);

        buttonYap.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                button2.startAnimation(animation);
            }
        });
    }
}
```
* rotatecalismasi.xml
```
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android"
    android:fillAfter="true">

    <rotate
        android:fromDegrees="0"
        android:toDegrees="90"
        android:duration="1000"
        android:pivotY="50%"
        android:pivotX="50%"/>

</set>
```
# Scale Animasyonu
![Scale](https://github.com/Fatih20823/Android/assets/101557027/8ba4841a-2e80-4bba-8a98-2deb42baedf8)
![Desktop Screenshot 2023 05 25 - 16 14 59 100 (2)](https://github.com/Fatih20823/Android/assets/101557027/d9bc7f3b-6415-4f90-b77e-3a9c2b07d537)
* MainActivity
```
package com.example.animasyonislemleri;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.view.animation.Animation;
import android.view.animation.AnimationUtils;
import android.widget.Button;

public class MainActivity extends AppCompatActivity {
    private Button button2,buttonYap;
    private Animation animation;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        button2 = findViewById(R.id.button2);
        buttonYap = findViewById(R.id.buttonYap);

        animation = AnimationUtils.loadAnimation(getApplicationContext(),R.anim.scalecalismasi);

        buttonYap.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                button2.startAnimation(animation);
            }
        });
    }
}
```
* scaleanimasyonu.xml
```
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android"
    android:fillAfter="true">

    <scale
        android:duration="300"
        android:fromXScale="1.0"
        android:toXScale="2.0"
        android:fromYScale="1.0"
        android:toYScale="1.0"
        android:pivotX="50%"
        android:pivotY="50%"/>
</set>
```
# Translate Animasyonu
![translate2 (1)](https://github.com/Fatih20823/Android/assets/101557027/70a5a5d6-dddb-4585-bf76-f2e678868d49)
![translate](https://github.com/Fatih20823/Android/assets/101557027/b51a8a5e-08fb-403a-94c7-991f03a91259)
* Cismin boyutunu referans alarak animasyon '%'
![cisim](https://github.com/Fatih20823/Android/assets/101557027/3140929d-f17c-4733-b4b3-cde352a01104)
* Ekran boyutunu referans alarak animasyon '%p'
![ekran](https://github.com/Fatih20823/Android/assets/101557027/c9af64e9-3d77-4fff-beb7-ee3df255594f)
* MainActivity
```
package com.example.animasyonislemleri;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.view.animation.Animation;
import android.view.animation.AnimationUtils;
import android.widget.Button;

public class MainActivity extends AppCompatActivity {
    private Button button2,buttonYap;
    private Animation animation;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        button2 = findViewById(R.id.button2);
        buttonYap = findViewById(R.id.buttonYap);

        animation = AnimationUtils.loadAnimation(getApplicationContext(),R.anim.translatecalismasi);

        buttonYap.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                button2.startAnimation(animation);
            }
        });
    }
}
```
* translatecalismasi.xml
```
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android"
    android:fillAfter="true">

    <translate
        android:duration="1000"
        android:fromXDelta="-25%p"
        android:toXDelta="50%p"
        android:fromYDelta="25%p"
        android:toYDelta="50%p"/>

</set>
```
# Zamansal İşlemler
![Zamansal](https://github.com/Fatih20823/Android/assets/101557027/ef459ccd-d876-4aea-81f8-ef250eb4b1b9)
![Desktop Screenshot 2023 05 26 - 11 25 25 87 (2)](https://github.com/Fatih20823/Android/assets/101557027/3d1d41bd-91f0-45ea-969f-2b02bcf16fa8)
![Ardışık zamn](https://github.com/Fatih20823/Android/assets/101557027/560fdd69-f8f5-4016-bb23-88a4bcd103db)
* aynianda.xml
```
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android"
    android:fillAfter="true">

    <scale
        android:duration="1000"
        android:fromYScale="1.0"
        android:toYScale="2.0"
        android:fromXScale="1.0"
        android:toXScale="2.0"
        android:pivotX="50%"
        android:pivotY="50%"/>

    <alpha
        android:duration="1000"
        android:fromAlpha="1.0"
        android:toAlpha="0.0"/>

    <translate
        android:duration="1000"
        android:fromYDelta="0%p"
        android:toYDelta="50%p"/>

</set>
```
# Ardışık Animasyon Yapma
![Desktop Screenshot 2023 05 26 - 11 48 00 03 (2)](https://github.com/Fatih20823/Android/assets/101557027/40b2cf3f-13e0-4db3-8bf5-0a793fdfd221)
![Desktop Screenshot 2023 05 26 - 11 47 53 35 (2)](https://github.com/Fatih20823/Android/assets/101557027/bd3dc3da-13c8-4f92-863e-5858450e5326)
![Adsız tasarım (1)](https://github.com/Fatih20823/Android/assets/101557027/693799e4-ff92-4f31-a3a2-08d09990b77a)
* ardisikislem.xml
```
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android"
    android:fillAfter="true">

    <translate
        android:duration="800"
        android:startOffset="300"
        android:fromXDelta="0%"
        android:toXDelta="100%"
        android:fromYDelta="0%"
        android:toYDelta="0%"/>

    <translate
        android:duration="800"
        android:startOffset="1100"
        android:fromXDelta="0%"
        android:toXDelta="0%"
        android:fromYDelta="0%"
        android:toYDelta="100%"/>

    <translate
        android:duration="800"
        android:startOffset="1900"
        android:fromXDelta="0%"
        android:toXDelta="-100%"
        android:fromYDelta="0%"
        android:toYDelta="0%"/>

    <translate
        android:duration="800"
        android:startOffset="2700"
        android:fromXDelta="0%"
        android:toXDelta="0%"
        android:fromYDelta="0%"
        android:toYDelta="-100%"/>

    <rotate
        android:duration="800"
        android:startOffset="3500"
        android:fromDegrees="0"
        android:toDegrees="360"
        android:pivotY="50%"
        android:pivotX="50%"/>

    <scale
        android:duration="800"
        android:startOffset="4300"
        android:fromYScale="1.0"
        android:toYScale="2.0"
        android:fromXScale="1.0"
        android:toXScale="2.0"
        android:pivotY="50%"
        android:pivotX="50%"/>

    <alpha
        android:duration="800"
        android:startOffset="5100"
        android:fromAlpha="1.0"
        android:toAlpha="0.0"/>

</set>
```
# Animasyonlu Float Action Button
![Adsız tasarım (2)](https://github.com/Fatih20823/Android/assets/101557027/dcf0ff3d-8172-4a23-9f50-3eab0c91aae2)
* MainActivity
```
package com.example.animasyonlufab;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.view.animation.Animation;
import android.view.animation.AnimationUtils;

import com.google.android.material.floatingactionbutton.FloatingActionButton;

public class MainActivity extends AppCompatActivity {
    private FloatingActionButton fabMain,fabBirinci,fabikinci;

    private Animation fabacik,fabkapali,geridon,ileridon;

    private Boolean fabDurum = false;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        fabMain = findViewById(R.id.fabMain);
        fabBirinci = findViewById(R.id.fabBirinci);
        fabikinci = findViewById(R.id.fabikinci);


        fabacik = AnimationUtils.loadAnimation(getApplicationContext(),R.anim.fabacik);
        fabkapali = AnimationUtils.loadAnimation(getApplicationContext(),R.anim.fabkapali);
        geridon = AnimationUtils.loadAnimation(getApplicationContext(),R.anim.geridon);
        ileridon = AnimationUtils.loadAnimation(getApplicationContext(),R.anim.ileridon);

        fabMain.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                if(fabDurum){
                    //tıklanıldıgında kapansın
                    fabMain.startAnimation(geridon);
                    fabBirinci.startAnimation(fabkapali);
                    fabikinci.startAnimation(fabkapali);
                    fabBirinci.setClickable(false);
                    fabikinci.setClickable(false);
                    fabDurum = false;

                }else {
                    // tıklanıldıgında acılsın
                    fabMain.startAnimation(ileridon);
                    fabBirinci.startAnimation(fabacik);
                    fabikinci.startAnimation(fabacik);
                    fabBirinci.setClickable(true);
                    fabikinci.setClickable(true);
                    fabDurum = true;


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

    <com.google.android.material.floatingactionbutton.FloatingActionButton
        android:id="@+id/fabMain"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginEnd="16dp"
        android:layout_marginBottom="16dp"
        android:clickable="true"
        app:fabSize="normal"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:srcCompat="@drawable/main_resim" />

    <com.google.android.material.floatingactionbutton.FloatingActionButton
        android:id="@+id/fabBirinci"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginEnd="16dp"
        android:layout_marginBottom="10dp"
        android:clickable="true"
        android:visibility="invisible"
        app:fabSize="mini"
        app:layout_constraintBottom_toTopOf="@+id/fabMain"
        app:layout_constraintEnd_toEndOf="parent"
        app:srcCompat="@drawable/ekle_resim" />

    <com.google.android.material.floatingactionbutton.FloatingActionButton
        android:id="@+id/fabikinci"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginEnd="16dp"
        android:layout_marginBottom="10dp"
        android:clickable="true"
        android:visibility="invisible"
        app:fabSize="mini"
        app:layout_constraintBottom_toTopOf="@+id/fabBirinci"
        app:layout_constraintEnd_toEndOf="parent"
        app:srcCompat="@drawable/foto_resim" />
</androidx.constraintlayout.widget.ConstraintLayout>
```
* fabacik.xml
```
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android"
    android:fillAfter="true">

    <scale
        android:duration="300"
        android:fromXScale="0.0"
        android:toXScale="0.8"
        android:fromYScale="0.0"
        android:toYScale="0.8"
        android:pivotX="50%"
        android:pivotY="50%"/>

    <alpha
        android:duration="300"
        android:fromAlpha="0.0"
        android:toAlpha="1.0"/>

</set>
```
* fabkapali.xml
```
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android"
    android:fillAfter="true">

    <scale
        android:duration="300"
        android:fromXScale="0.8"
        android:toXScale="0.0"
        android:fromYScale="0.8"
        android:toYScale="0.0"
        android:pivotX="50%"
        android:pivotY="50%"/>

    <alpha
        android:duration="300"
        android:fromAlpha="1.0"
        android:toAlpha="0.0"/>

</set>
```
* geridon.xml
```
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android"
    android:fillAfter="true">

    <rotate
        android:duration="300"
        android:fromDegrees="90"
        android:toDegrees="0"
        android:pivotX="50%"
        android:pivotY="50%"/>

</set>
```
* ileridon.xml
```
<?xml version="1.0" encoding="utf-8"?>
<set xmlns:android="http://schemas.android.com/apk/res/android"
    android:fillAfter="true">

    <rotate
        android:duration="300"
        android:fromDegrees="0"
        android:toDegrees="90"
        android:pivotX="50%"
        android:pivotY="50%"/>

</set>
```
# MotionLayout
![Adsız tasarım (3)](https://github.com/Fatih20823/Android/assets/101557027/0a649887-4b16-4fd1-b095-1581c7526960)
MotionLayout nedir?
MotionLayout ConstraintLayout 2.0 versiyonu ile gelen uygulamalarımıza animasyonlar ekleyip ve yönetmemize yardımcı olan bir layout türüdür. Temel görevi kullanıcı etkileşimi ile birlikte UI elemanlarının hareketlendirilmesidir. Button, TextView, ImageView… gibi kullanıcıların etkileşime girdiği UI öğelerini taşımayı, yeniden boyutlandırmayı ve canlandırmayı amaçlamaktadır.

MotionLayout doğrudan sahip olduğu Layoutlar veya Viewler ile çalışır yani iç içe yerleşmiş layout hiyerarşilerini veya ekran geçişlerini desteklemez.
* MainActivity.xml
```
package com.example.motionlayout;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}
```
* activity_main.xml
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.motion.widget.MotionLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:backgroundTint="@color/teal_200"
    app:layoutDescription="@xml/activity_main_scene"
    tools:context=".MainActivity">

    <Button
        android:id="@+id/buttonUst"
        android:layout_width="200dp"
        android:layout_height="100dp"
        android:layout_marginTop="120dp"
        android:backgroundTint="@color/purple_700"
        android:text="Button Üst"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <Button
        android:id="@+id/buttonAlt"
        android:layout_width="200dp"
        android:layout_height="100dp"
        android:layout_marginBottom="120dp"
        android:backgroundTint="@color/teal_200"
        android:text="Button Alt"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent" />
</androidx.constraintlayout.motion.widget.MotionLayout>
```
* activity_main_scene.xml
```
<?xml version="1.0" encoding="utf-8"?>
<MotionScene 
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:motion="http://schemas.android.com/apk/res-auto">

    <Transition
        motion:constraintSetEnd="@+id/end"
        motion:constraintSetStart="@id/start"
        motion:duration="1000">
       <KeyFrameSet>
           <KeyAttribute
               motion:motionTarget="@+id/buttonUst"
               motion:framePosition="50"
               android:alpha="0.5" />
           <KeyAttribute
               motion:motionTarget="@+id/buttonAlt"
               motion:framePosition="50"
               android:alpha="0.5" />
           <KeyAttribute
               motion:motionTarget="@+id/buttonUst"
               motion:framePosition="25"
               android:rotation="45" />
           <KeyAttribute
               motion:motionTarget="@+id/buttonAlt"
               motion:framePosition="75"
               android:rotation="45" />
           <KeyAttribute
               motion:motionTarget="@+id/buttonAlt"
               motion:framePosition="50"
               android:scaleX="0.5" />
           <KeyAttribute
               motion:motionTarget="@+id/buttonUst"
               motion:framePosition="50"
               android:scaleX="0.5" />
           <KeyAttribute
               motion:motionTarget="@+id/buttonUst"
               motion:framePosition="50"
               android:translationX="-100dp" />
           <KeyAttribute
               motion:motionTarget="@+id/buttonAlt"
               motion:framePosition="50"
               android:translationX="100dp" />
       </KeyFrameSet>
        <OnSwipe />
        <OnClick motion:targetId="@+id/buttonUst" />
    </Transition>

    <ConstraintSet android:id="@+id/start">
        <Constraint
            android:layout_height="100dp"
            motion:layout_constraintHorizontal_bias="0.5"
            motion:layout_constraintEnd_toEndOf="parent"
            android:layout_width="200dp"
            motion:layout_constraintStart_toStartOf="parent"
            android:id="@+id/buttonUst"
            motion:layout_constraintBottom_toBottomOf="parent"
            android:layout_marginBottom="128dp" />
        <Constraint
            android:layout_height="100dp"
            motion:layout_constraintHorizontal_bias="0.5"
            motion:layout_constraintEnd_toEndOf="parent"
            android:layout_width="200dp"
            motion:layout_constraintStart_toStartOf="parent"
            android:id="@+id/buttonAlt"
            motion:layout_constraintTop_toTopOf="parent"
            android:layout_marginTop="128dp" />
    </ConstraintSet>

    <ConstraintSet android:id="@+id/end">
    </ConstraintSet>
</MotionScene>
```
# Motion Layout Uygulama
![Adsız tasarım (4)](https://github.com/Fatih20823/Android/assets/101557027/29e8e0b5-3dba-4433-bc54-fcc20e484f0b)
* MainActivity
```
package com.example.motionlayoutuygulama;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}
```
* activity_main.xml
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.motion.widget.MotionLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    app:layoutDescription="@xml/activity_main_scene"
    tools:context=".MainActivity">

    <ImageView
        android:id="@+id/resim"
        android:layout_width="500dp"
        android:layout_height="600dp"
        android:scaleType="centerCrop"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.505"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:srcCompat="@drawable/yemekarkaplan" />

    <androidx.cardview.widget.CardView
        android:id="@+id/cardView"
        android:layout_width="0dp"
        android:layout_height="300dp"
        android:translationY="250dp"
        app:cardCornerRadius="30dp"
        app:layout_constraintBottom_toBottomOf="@+id/resim"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent">

        <androidx.constraintlayout.widget.ConstraintLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent">

            <TextView
                android:id="@+id/textView"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_marginTop="8dp"
                android:text="Izgara Tavuk"
                android:textSize="24sp"
                android:textStyle="bold"
                app:layout_constraintEnd_toEndOf="parent"
                app:layout_constraintHorizontal_bias="0.5"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toTopOf="parent" />

            <TextView
                android:id="@+id/textView2"
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_marginStart="16dp"
                android:layout_marginEnd="16dp"
                android:text="Tavuk ızgara ne demek? Izgara, yiyeceklerin yüzeyine genellikle yukarıdan, aşağıdan veya yandan uygulanan kuru ısıyla pişirme şeklidir. Izgara genellikle önemli miktarda doğrudan, radyan ısı içerir ve et ve sebzeleri hızlı bir şekilde pişirmek için kullanılır."
                app:layout_constraintBottom_toBottomOf="parent"
                app:layout_constraintEnd_toEndOf="parent"
                app:layout_constraintHorizontal_bias="0.5"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toBottomOf="@+id/textView"
                app:layout_constraintVertical_bias="0.5" />
        </androidx.constraintlayout.widget.ConstraintLayout>
    </androidx.cardview.widget.CardView>
</androidx.constraintlayout.motion.widget.MotionLayout>
```
* activity_main_scene.xml
```
<?xml version="1.0" encoding="utf-8"?>
<MotionScene 
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:motion="http://schemas.android.com/apk/res-auto">

    <Transition
        motion:constraintSetEnd="@+id/end"
        motion:constraintSetStart="@id/start"
        motion:duration="1000">
       <KeyFrameSet>
       </KeyFrameSet>
        <OnSwipe />
        <OnClick motion:targetId="@+id/cardView" />
    </Transition>

    <ConstraintSet android:id="@+id/start">
    </ConstraintSet>

    <ConstraintSet android:id="@+id/end">
        <Constraint
            android:id="@+id/cardView"
            motion:layout_constraintEnd_toEndOf="parent"
            android:layout_width="0dp"
            android:layout_height="300dp"
            motion:layout_constraintBottom_toBottomOf="parent"
            android:translationY="50dp"
            motion:layout_constraintStart_toStartOf="parent" />
        <Constraint
            android:id="@+id/resim"
            motion:layout_constraintEnd_toEndOf="parent"
            android:layout_width="500dp"
            android:layout_height="400dp"
            motion:layout_constraintHorizontal_bias="0.505"
            motion:layout_constraintTop_toTopOf="parent"
            motion:layout_constraintStart_toStartOf="parent" />
    </ConstraintSet>
</MotionScene>
```

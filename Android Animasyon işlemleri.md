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

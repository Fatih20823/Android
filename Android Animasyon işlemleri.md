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
* Android:fillAfter
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

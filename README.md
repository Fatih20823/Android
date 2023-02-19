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

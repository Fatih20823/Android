# ToggleBottom-Switch
![widget2](https://user-images.githubusercontent.com/101557027/226090622-86cb7d43-7225-426a-b13e-dbcb726c751e.gif)
* MainActivity
```
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.CompoundButton;
import android.widget.Switch;
import android.widget.ToggleButton;

public class MainActivity extends AppCompatActivity {
    private Switch switch1;
    private ToggleButton toggleButton;
    private Button button;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        switch1 = findViewById(R.id.switch1);
        toggleButton = findViewById(R.id.toggleButton);
        button = findViewById(R.id.button);

        switch1.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener() {
            @Override
            public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {
                if(isChecked){
                    Log.e("Switch","ON");
                }else {
                    Log.e("Switch","OFF");
                }
            }
        });

        toggleButton.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener() {
            @Override
            public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {
                if(isChecked){
                    Log.e("Toggle Button","ON");
                }else {
                    Log.e("Toggle Button","OFF");
                }
            }
        });

        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Boolean switchDurum = switch1.isChecked();
                Boolean toggleButtonDurum = toggleButton.isChecked();

                Log.e("Swicth Durum",String.valueOf(switchDurum));
                Log.e("Toggle Button Durum",String.valueOf(toggleButtonDurum));
            }
        });
    }
}
```
------------
# RadioButton CheckBox
![RadioButton](https://user-images.githubusercontent.com/101557027/226140110-8626452e-c23c-41d6-9cc6-5afbcbc4a642.gif)
* mainActivity
```
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.CheckBox;
import android.widget.CompoundButton;
import android.widget.RadioButton;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {
    private CheckBox checkBoxJava,checkBoxKotlin;
    private RadioButton radioButtonBarcelona, radioButtonRealMadrid;
    private Button button;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        checkBoxJava = findViewById(R.id.checkBoxJava);
        checkBoxKotlin = findViewById(R.id.checkBoxKotlin);
        radioButtonBarcelona = findViewById(R.id.radioButtonBarcelona);
        radioButtonRealMadrid = findViewById(R.id.radioButtonRealMadrid);
        button = findViewById(R.id.button);

        radioButtonBarcelona.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener() {
            @Override
            public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {
                if(isChecked) {
                    Toast.makeText(getApplicationContext(),"Tebrikler :)",Toast.LENGTH_SHORT).show();
                }
            }
        });

        checkBoxJava.setOnCheckedChangeListener(new CompoundButton.OnCheckedChangeListener() {
            @Override
            public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {
                if(isChecked) {
                    Toast.makeText(getApplicationContext(),"Tebrikler Java yı seçtiniz :)",Toast.LENGTH_SHORT).show();
                }
            }
        });

        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Boolean javaDurum = checkBoxJava.isChecked();
                Boolean KotlinDurum = checkBoxKotlin.isChecked();
                Boolean BarcelonaDurum = radioButtonBarcelona.isChecked();
                Boolean RealMadridDurum = radioButtonRealMadrid.isChecked();

                Log.e("Java Durum",String.valueOf(javaDurum));
                Log.e("Kotlin Durum",String.valueOf(KotlinDurum));
                Log.e("Barcelona Durum",String.valueOf(BarcelonaDurum));
                Log.e("Real madrid Durum",String.valueOf(RealMadridDurum));

            }
        });
    }
}
```

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
# Progress Bar Seek Bar Rating Bar
---------
![Prgress](https://user-images.githubusercontent.com/101557027/226155798-4a890290-bf43-46b1-9479-6ac81adf2ee9.gif)
---------
* MainActivity
```
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.ProgressBar;
import android.widget.RatingBar;
import android.widget.SeekBar;
import android.widget.TextView;

public class MainActivity extends AppCompatActivity {
    private Button button,buttonBasla,buttondur;
    private ProgressBar progressBar;
    private TextView textViewSonuc;
    private SeekBar seekBar;
    private RatingBar ratingBar;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        button = findViewById(R.id.button);
        buttonBasla = findViewById(R.id.buttonBasla);
        buttondur = findViewById(R.id.buttonDur);
        progressBar = findViewById(R.id.progressBar);
        textViewSonuc = findViewById(R.id.textViewSon);
        seekBar = findViewById(R.id.seekBar);
        ratingBar = findViewById(R.id.ratingBar);

        buttonBasla.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                progressBar.setVisibility(View.VISIBLE);
            }
        });

        buttondur.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                progressBar.setVisibility(View.INVISIBLE);
            }
        });

        seekBar.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() {
            @Override
            public void onProgressChanged(SeekBar seekBar, int progress, boolean fromUser) {
                textViewSonuc.setText("Sonuç : "+progress);
            }

            @Override
            public void onStartTrackingTouch(SeekBar seekBar) {

            }

            @Override
            public void onStopTrackingTouch(SeekBar seekBar) {

            }
        });

        button.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                float gelenOylama = ratingBar.getRating();
                int gelenIlerme = seekBar.getProgress();

                Log.e("Oylama Sonucu ",String.valueOf(gelenOylama));
                Log.e("Ilerleme Sonucu ",String.valueOf(gelenIlerme));
            }
        });
    }
}
```
# ImageView
-----------
![ImageView](https://user-images.githubusercontent.com/101557027/226176916-fe6a155e-9493-4586-936b-c0df2d9f51ba.gif)
--------
# MainActivity
```
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.ImageView;

public class MainActivity extends AppCompatActivity {
    private ImageView imageView;
    private Button button1,button2;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        imageView = findViewById(R.id.imageView);
        button1 = findViewById(R.id.button1);
        button2 = findViewById(R.id.button2);

        button1.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                imageView.setImageResource(R.drawable.clean1);
            }
        });

        button2.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                imageView.setImageResource(getResources().getIdentifier("resim","drawable",getPackageName()));
            }
        });
    }
}
```
# VideoView
-----------
![VideoView](https://user-images.githubusercontent.com/101557027/226176948-51884d0f-42a3-45f0-a664-7b6a8702dc3f.gif)
------------
# MainActivity
```
import androidx.appcompat.app.AppCompatActivity;

import android.net.Uri;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.VideoView;

public class MainActivity extends AppCompatActivity {
    private VideoView videoView;
    private Button buttonBasla,buttonDurdur;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        videoView = findViewById(R.id.videoView);
        buttonBasla = findViewById(R.id.buttonBasla);
        buttonDurdur = findViewById(R.id.buttonDurdur);

        buttonBasla.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Uri adres = Uri.parse("android.resource://"+getPackageName()+"/"+R.raw.qqq);

                videoView.setVideoURI(adres);
                videoView.start();
            }
        });

        buttonDurdur.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                videoView.stopPlayback();
            }
        });
    }
}
```
# ScrollView
* ScrollView , Sayfa içerisindeki içerik ekran boyutundan daha fazla yer kaplıyorsa aşağı ve yukarı sayfayı hareket ettirmemize yardım eder.
-----------
![Scroll](https://user-images.githubusercontent.com/101557027/226203633-a2aa846e-2fc2-4c25-bc47-51119a047d05.gif)
--------------
# DateTimePicker
![DateTimePicker](https://user-images.githubusercontent.com/101557027/226410300-82cea92b-9a43-4279-acdd-fc318feb9f62.gif)
--------------
* MainActivity
--------------
```
import androidx.appcompat.app.AppCompatActivity;

import android.app.DatePickerDialog;
import android.app.TimePickerDialog;
import android.content.DialogInterface;
import android.os.Bundle;
import android.view.View;
import android.widget.DatePicker;
import android.widget.EditText;
import android.widget.TimePicker;

import java.util.Calendar;

public class MainActivity extends AppCompatActivity {
    private EditText editTextSaat,editTextTarih;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        editTextSaat = findViewById(R.id.editTextSaat);
        editTextTarih = findViewById(R.id.editTextTarih);

        editTextSaat.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Calendar calendar = Calendar.getInstance();
                int saat = calendar.get(Calendar.HOUR_OF_DAY);
                int dakika = calendar.get(calendar.MINUTE);
                TimePickerDialog timePicker;

                timePicker = new TimePickerDialog(MainActivity.this, new TimePickerDialog.OnTimeSetListener() {
                    @Override
                    public void onTimeSet(TimePicker view, int hourOfDay, int minute) {
                        editTextSaat.setText(hourOfDay+" : "+minute);
                    }
                },saat,dakika,true);

                timePicker.setTitle("Saat Seçiniz");
                timePicker.setButton(DialogInterface.BUTTON_POSITIVE,"Ayarla",timePicker);
                timePicker.setButton(DialogInterface.BUTTON_NEGATIVE,"İptal",timePicker);

                timePicker.show();
            }
        });

        editTextTarih.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {

                Calendar calendar = Calendar.getInstance();
                int yil = calendar.get(Calendar.YEAR);
                int ay = calendar.get(Calendar.MONTH);
                int gun = calendar.get(Calendar.DAY_OF_MONTH);
                DatePickerDialog datePicker;

                datePicker = new DatePickerDialog(MainActivity.this, new DatePickerDialog.OnDateSetListener() {
                    @Override
                    public void onDateSet(DatePicker view, int year, int month, int dayOfMonth) {
                        editTextTarih.setText(year+"/"+month+"/"+dayOfMonth);
                    }
                },yil,ay,gun);

                datePicker.setTitle("Tarih Seçiniz");
                datePicker.setButton(DialogInterface.BUTTON_POSITIVE,"Ayarla",datePicker);
                datePicker.setButton(DialogInterface.BUTTON_NEGATIVE,"İptal",datePicker);
                datePicker.show();
            }
        });
    }
}
```
# ListView
![ListViewKul](https://user-images.githubusercontent.com/101557027/226411073-7f2ff400-3d16-451c-9fa9-5d3a66232ff7.gif)
* MainActivity
----------
```
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.widget.AdapterView;
import android.widget.ArrayAdapter;
import android.widget.ListView;
import android.widget.Toast;

import com.example.listviewkullanimi.R;

import java.util.ArrayList;

public class MainActivity extends AppCompatActivity {
    private ListView listView;
    private ArrayList<String> ulkeler = new ArrayList<>();
    private ArrayAdapter<String> veriAdaptoru;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        listView = findViewById(R.id.listView);

        ulkeler.add("Türkiye");
        ulkeler.add("İtalya");
        ulkeler.add("Güney Kore");
        ulkeler.add("Almanya");
        ulkeler.add("Çin");
        ulkeler.add("İspanya");
        ulkeler.add("Portekiz");
        ulkeler.add("Japonya");
        ulkeler.add("Danimarka");

        veriAdaptoru = new ArrayAdapter<>(this, android.R.layout.simple_list_item_1,android.R.id.text1,ulkeler);

        listView.setAdapter(veriAdaptoru);

        listView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            @Override
            public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
                Toast.makeText(getApplicationContext()
                        ,"Seçtiğiniz Ülke : "+ulkeler.get(position)
                        ,Toast.LENGTH_SHORT).show();
            }
        });

    }
}
```
# GridView
![GridViewKul](https://user-images.githubusercontent.com/101557027/226410702-c2dd0847-6c42-445a-88a6-c58116f9849c.gif)
* mainActivity
--------
```
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.widget.AdapterView;
import android.widget.ArrayAdapter;
import android.widget.GridView;
import android.widget.Toast;

import com.example.listviewkullanimi.R;

import java.util.ArrayList;

public class MainActivity extends AppCompatActivity {
    private GridView gridView;
    private ArrayList<String> ulkeler = new ArrayList<>();
    private ArrayAdapter<String> veriAdaptoru;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        gridView = findViewById(R.id.gridView);

        ulkeler.add("Türkiye");
        ulkeler.add("İtalya");
        ulkeler.add("Güney Kore");
        ulkeler.add("Almanya");
        ulkeler.add("Çin");
        ulkeler.add("İspanya");
        ulkeler.add("Portekiz");
        ulkeler.add("Japonya");
        ulkeler.add("Danimarka");

        veriAdaptoru = new ArrayAdapter<>(this, android.R.layout.simple_list_item_1,android.R.id.text1,ulkeler);

        gridView.setAdapter(veriAdaptoru);

        gridView.setOnItemClickListener(new AdapterView.OnItemClickListener() {
            @Override
            public void onItemClick(AdapterView<?> parent, View view, int position, long id) {
                Toast.makeText(getApplicationContext()
                        ,"Seçtiğiniz Ülke : "+ulkeler.get(position)
                        ,Toast.LENGTH_SHORT).show();
            }
        });

    }
}
```

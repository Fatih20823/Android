# PopUpMenu
-----------
![PopUpMenu](https://user-images.githubusercontent.com/101557027/226803791-19bcebc5-5b6e-4548-8f11-e07d00268f92.gif)
-----------
* MainActivity
```
import androidx.appcompat.app.AppCompatActivity;
import androidx.appcompat.widget.PopupMenu;

import android.os.Bundle;
import android.view.MenuItem;
import android.view.View;
import android.widget.Button;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {
    private Button buttonMenuAc;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        buttonMenuAc = findViewById(R.id.buttonMenuAcma);

        buttonMenuAc.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {

                PopupMenu popup = new PopupMenu(MainActivity.this,buttonMenuAc);

                popup.getMenuInflater().inflate(R.menu.popup_menu,popup.getMenu());

                popup.setOnMenuItemClickListener(new PopupMenu.OnMenuItemClickListener() {
                    @Override
                    public boolean onMenuItemClick(MenuItem item) {

                        switch (item.getItemId()){
                            case R.id.action_sil:
                                Toast.makeText(getApplicationContext(),"Sil Seçildi",Toast.LENGTH_SHORT).show();
                                return true;
                            case R.id.action_duzenle:
                                Toast.makeText(getApplicationContext(),"Düzenle Seçildi",Toast.LENGTH_SHORT).show();
                                return true;
                            default:
                                return false;
                        }

                    }
                });

                popup.show();
            }
        });
    }
}
```
# AlertView
-----------
![AlertView](https://user-images.githubusercontent.com/101557027/226811894-9fcf8fea-da15-4f0c-9393-02868d519f7e.gif)
-----------
* MainActivity
```
import androidx.appcompat.app.AlertDialog;
import androidx.appcompat.app.AppCompatActivity;

import android.content.DialogInterface;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {
    private Button buttonNormal,buttonOzel;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        buttonNormal = findViewById(R.id.buttonNormal);
        buttonOzel = findViewById(R.id.buttonOzel);

        buttonNormal.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                AlertDialog.Builder ad = new AlertDialog.Builder(MainActivity.this);

                ad.setMessage("Mesaj");
                ad.setTitle("Başlık");
                ad.setIcon(R.drawable.resim);

                ad.setPositiveButton("Tamam", new DialogInterface.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialog, int which) {
                        Toast.makeText(getApplicationContext(),"Tamam Tıklandı",Toast.LENGTH_SHORT).show();
                    }
                });

                ad.setNegativeButton("iptal", new DialogInterface.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialog, int which) {
                        Toast.makeText(getApplicationContext(),"iptal Tıklandı",Toast.LENGTH_SHORT).show();
                    }
                });

                ad.create().show();
            }
        });

        buttonOzel.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {

                View tasarim = getLayoutInflater().inflate(R.layout.alert_tasarim,null);

                EditText editTextAlert = tasarim.findViewById(R.id.editTextAlert);

                AlertDialog.Builder ad = new AlertDialog.Builder(MainActivity.this);

                ad.setTitle("Başlık");
                ad.setMessage("Mesaj");
                ad.setView(tasarim);

                ad.setPositiveButton("Kaydet", new DialogInterface.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialog, int which) {
                        String gelenVeri = editTextAlert.getText().toString();

                        Toast.makeText(getApplicationContext(),"Alınan Veri"+gelenVeri,Toast.LENGTH_SHORT).show();
                    }
                });

                ad.setNegativeButton("İptal", new DialogInterface.OnClickListener() {
                    @Override
                    public void onClick(DialogInterface dialog, int which) {
                        Toast.makeText(getApplicationContext(),"Özel Veri Seçildi",Toast.LENGTH_SHORT).show();
                    }
                });

                ad.create().show();
            }
        });
    }
}
```

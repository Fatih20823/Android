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

# EditText FloatingLabel
![EdittextFloatingLabelKul](https://user-images.githubusercontent.com/101557027/227474285-27514c96-a6f2-4018-94ff-bb69d030735f.gif)
-----------
* MainActivity
```
import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.Toast;

import com.google.android.material.textfield.TextInputEditText;

public class MainActivity extends AppCompatActivity {
    private TextInputEditText editTextAd,editTextTel;
    private Button buttonYap;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        editTextAd = findViewById(R.id.edittextAd);
        editTextTel = findViewById(R.id.edittextTel);
        buttonYap = findViewById(R.id.buttonYap);

        buttonYap.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {

                String ad = editTextAd.getText().toString();
                String Tel = editTextTel.getText().toString();
                Toast.makeText(getApplicationContext(),"Adınız :"+ad+"  Teliniz :"+Tel,Toast.LENGTH_LONG).show();
            }
        });
    }
}
```
# ToolBar Menu Ve Search
![ToolbarMenuVeSearch](https://user-images.githubusercontent.com/101557027/227916501-2f10d08f-c558-4987-927d-4e64a04c8c16.gif)
--------------
* MainActivity
```
import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.appcompat.widget.SearchView;
import androidx.appcompat.widget.Toolbar;

import android.os.Bundle;
import android.util.Log;
import android.view.Menu;
import android.view.MenuItem;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity implements SearchView.OnQueryTextListener {
    private Toolbar toolbar;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        toolbar = findViewById(R.id.toolbar);

        toolbar.setTitle("Toolbar Menu");
        setSupportActionBar(toolbar);
    }

    @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        getMenuInflater().inflate(R.menu.toolbarmenu,menu);

        MenuItem item = menu.findItem(R.id.action_ara);
        SearchView searchView = (SearchView) item.getActionView();
        searchView.setOnQueryTextListener(this);
        return super.onCreateOptionsMenu(menu);
    }

    @Override
    public boolean onOptionsItemSelected(@NonNull MenuItem item) {

        switch (item.getItemId()){
            case R.id.action_bilgi:
                Toast.makeText(getApplicationContext(),"Bilgi Tıklandı",Toast.LENGTH_SHORT).show();
                return true;
            case R.id.action_ekle:
                Toast.makeText(getApplicationContext(),"Ekle Tıklandı",Toast.LENGTH_SHORT).show();
                return true;
            case R.id.action_ayarlar:
                Toast.makeText(getApplicationContext(),"Ayarlar Tıklandı",Toast.LENGTH_SHORT).show();
                return true;
            case R.id.action_cikis:
                Toast.makeText(getApplicationContext(),"Çıkış Tıklandı",Toast.LENGTH_SHORT).show();
                return true;
            default:
            return super.onOptionsItemSelected(item);
        }

    }

    @Override
    public boolean onQueryTextSubmit(String query) {
        Log.e("Gönderilen Arama Sonucu",query);
        return true;
    }

    @Override
    public boolean onQueryTextChange(String newText) {
        Log.e("Harf Girdikçe Sonucu",newText);
        return true;
    }
}
```

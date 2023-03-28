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
# RecyclerView Kullanımı
![Untitled4](https://user-images.githubusercontent.com/101557027/228341884-2e85d304-9455-4644-a33b-77700008fe15.gif)
![RV-StaggerredGridLayoutManager](https://user-images.githubusercontent.com/101557027/228343659-673c0875-e898-4654-8368-ba949c952fa1.png)
-----------
* MainActivity
```
import androidx.appcompat.app.AppCompatActivity;
import androidx.recyclerview.widget.LinearLayoutManager;
import androidx.recyclerview.widget.RecyclerView;
import androidx.recyclerview.widget.StaggeredGridLayoutManager;

import android.os.Bundle;

import java.util.ArrayList;

public class MainActivity extends AppCompatActivity {
    private RecyclerView rv;
    private ArrayList<String> ulkelerList;
    private BasitRVAdapter adapter;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        rv = findViewById(R.id.rv);
        rv.setHasFixedSize(true);

       // rv.setLayoutManager(new LinearLayoutManager(this));

        rv.setLayoutManager(new StaggeredGridLayoutManager(2,StaggeredGridLayoutManager.VERTICAL));

        ulkelerList = new ArrayList<>();
        ulkelerList.add("Türkiye");
        ulkelerList.add("İtalya");
        ulkelerList.add("Japonya");
        ulkelerList.add("Rusya");
        ulkelerList.add("Türkiye");
        ulkelerList.add("İtalya");
        ulkelerList.add("Japonya");
        ulkelerList.add("Rusya");
        ulkelerList.add("Türkiye");
        ulkelerList.add("İtalya");
        ulkelerList.add("Japonya");
        ulkelerList.add("Rusya");

        adapter = new BasitRVAdapter(this,ulkelerList);

        rv.setAdapter(adapter);
    }
}
```
--------------
![Desktop Screenshot 2023 03 27 - 18 04 18 35](https://user-images.githubusercontent.com/101557027/228343444-c4b26fbf-cb56-4137-b029-cec94abd0a58.png)
* RecyclerViewAdapter
```
import android.content.Context;
import android.view.LayoutInflater;
import android.view.MenuItem;
import android.view.View;
import android.view.ViewGroup;
import android.widget.ImageView;
import android.widget.TextView;
import android.widget.Toast;

import androidx.annotation.NonNull;
import androidx.appcompat.widget.PopupMenu;
import androidx.cardview.widget.CardView;
import androidx.recyclerview.widget.RecyclerView;

import java.util.List;

public class BasitRVAdapter extends RecyclerView.Adapter<BasitRVAdapter.CardViewTasarimNesneleriniTutucu> {
    private Context mContext;
    private List<String> ulkelerDisaridanGelenList;

    public BasitRVAdapter(Context mContext, List<String> ulkelerDisaridanGelenList) {
        this.mContext = mContext;
        this.ulkelerDisaridanGelenList = ulkelerDisaridanGelenList;
    }
    public class CardViewTasarimNesneleriniTutucu extends RecyclerView.ViewHolder {
        public TextView satirYazi;
        public CardView satirCardView;
        private ImageView noktaResim;

        public CardViewTasarimNesneleriniTutucu(View view) {
            super(view);
            satirYazi = view.findViewById(R.id.satirYazi);
            satirCardView = view.findViewById(R.id.satirCardView);
            noktaResim = view.findViewById(R.id.noktaResim);
        }
    }

    @NonNull
    @Override
    public CardViewTasarimNesneleriniTutucu onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
            View itemView = LayoutInflater.from(parent.getContext())
                        .inflate(R.layout.card_tasarim,parent,false);
        return new CardViewTasarimNesneleriniTutucu(itemView);
    }

    @Override
    public void onBindViewHolder(@NonNull CardViewTasarimNesneleriniTutucu holder, int position) {
        String ulke = ulkelerDisaridanGelenList.get(position);

        holder.satirYazi.setText(ulke);

        holder.satirCardView.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Toast.makeText(mContext,"Seçtiğiniz Ülke :"+ulke,Toast.LENGTH_SHORT).show();
            }
        });

        holder.noktaResim.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {

                PopupMenu popupMenu = new PopupMenu(mContext,holder.noktaResim);
                popupMenu.getMenuInflater().inflate(R.menu.card_menu,popupMenu.getMenu());
                popupMenu.show();

                popupMenu.setOnMenuItemClickListener(new PopupMenu.OnMenuItemClickListener() {
                    @Override
                    public boolean onMenuItemClick(MenuItem item) {

                        switch (item.getItemId()){
                            case R.id.action_sil:
                                Toast.makeText(mContext,"Sil Tıklandı !"+ulke,Toast.LENGTH_SHORT).show();
                                return true;
                            case R.id.action_duzenle:
                                Toast.makeText(mContext,"Düzenle Tıklandı !"+ulke,Toast.LENGTH_SHORT).show();
                                return true;
                            default:
                                return false;
                        }

                    }
                });
            }
        });
    }

    @Override
    public int getItemCount() {
        return ulkelerDisaridanGelenList.size();
    }
}
```

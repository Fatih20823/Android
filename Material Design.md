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
# RecyclerView Film Uygulaması
![RecyclerUygulama](https://user-images.githubusercontent.com/101557027/228482696-84bf5054-600b-4205-864f-02680b8c0341.gif)
----------
* MainActivity
```
import androidx.appcompat.app.AppCompatActivity;
import androidx.recyclerview.widget.RecyclerView;
import androidx.recyclerview.widget.StaggeredGridLayoutManager;

import android.os.Bundle;

import java.util.ArrayList;

public class MainActivity extends AppCompatActivity {
    private RecyclerView rv;
    private ArrayList<Filmler> filmlerArrayList;
    private FilmAdapter adapter;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        rv = findViewById(R.id.rv);
        rv.setHasFixedSize(true);

        rv.setLayoutManager(new StaggeredGridLayoutManager(2,StaggeredGridLayoutManager.VERTICAL));

        Filmler f1 = new Filmler(1,"Ayla","ayla",12.99);
        Filmler f2 = new Filmler(2,"The Collection","collection",10.99);
        Filmler f3 = new Filmler(3,"Ev","ev",11.99);
        Filmler f4 = new Filmler(4,"Kapı","kapi",9.99);
        Filmler f5 = new Filmler(5,"Super Hayvanlar","superpets",15.99);
        Filmler f6 = new Filmler(6,"İllüzyonist","illusyonist",7.99);

        filmlerArrayList = new ArrayList<>();
        filmlerArrayList.add(f1);
        filmlerArrayList.add(f2);
        filmlerArrayList.add(f3);
        filmlerArrayList.add(f4);
        filmlerArrayList.add(f5);
        filmlerArrayList.add(f6);

        adapter = new FilmAdapter(this,filmlerArrayList);
        rv.setAdapter(adapter);


    }
}
```
* Filmler
```
package com.example.dataylirecyclerviewkullanimi;

public class Filmler {
    private int film_id;
    private String film_ad;
    private String film_resim_ad;
    private double film_fiyat;

    public Filmler() {
    }

    public Filmler(int film_id, String film_ad, String film_resim_ad, double film_fiyat) {
        this.film_id = film_id;
        this.film_ad = film_ad;
        this.film_resim_ad = film_resim_ad;
        this.film_fiyat = film_fiyat;
    }

    public int getFilm_id() {
        return film_id;
    }

    public void setFilm_id(int film_id) {
        this.film_id = film_id;
    }

    public String getFilm_ad() {
        return film_ad;
    }

    public void setFilm_ad(String film_ad) {
        this.film_ad = film_ad;
    }

    public String getFilm_resim_ad() {
        return film_resim_ad;
    }

    public void setFilm_resim_ad(String film_resim_ad) {
        this.film_resim_ad = film_resim_ad;
    }

    public double getFilm_fiyat() {
        return film_fiyat;
    }

    public void setFilm_fiyat(double film_fiyat) {
        this.film_fiyat = film_fiyat;
    }
}
```
* FilmAdapter
```
import android.content.Context;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.Button;
import android.widget.ImageView;
import android.widget.TextView;
import android.widget.Toast;

import androidx.annotation.NonNull;
import androidx.recyclerview.widget.RecyclerView;

import java.util.List;

public class FilmAdapter extends RecyclerView.Adapter<FilmAdapter.CardViewTasarimNesneleriniTutucu> {
    private Context mContext;
    private List<Filmler> filmlerList;

    public FilmAdapter(Context mContext, List<Filmler> filmlerList) {
        this.mContext = mContext;
        this.filmlerList = filmlerList;
    }
    public class CardViewTasarimNesneleriniTutucu extends RecyclerView.ViewHolder {
        public ImageView imageViewFilmResim;
        public TextView textViewFilmBaslik;
        public TextView textViewFilmFiyat;
        public Button buttonSepeteEkle;

        public CardViewTasarimNesneleriniTutucu(@NonNull View itemView) {
            super(itemView);
            imageViewFilmResim = itemView.findViewById(R.id.imageViewAyla);
            textViewFilmBaslik = itemView.findViewById(R.id.textViewFilmBaslik);
            textViewFilmFiyat = itemView.findViewById(R.id.textViewFilmFiyat);
            buttonSepeteEkle = itemView.findViewById(R.id.buttonSepeteEkle);
        }
    }

    @NonNull
    @Override
    public CardViewTasarimNesneleriniTutucu onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        View itemView = LayoutInflater.from(parent.getContext())
                .inflate(R.layout.card_film_tasarim,parent,false);
        return new CardViewTasarimNesneleriniTutucu(itemView);
    }

    @Override
    public void onBindViewHolder(@NonNull CardViewTasarimNesneleriniTutucu holder, int position) {
        Filmler film = filmlerList.get(position);

        holder.textViewFilmBaslik.setText(film.getFilm_ad());
        holder.textViewFilmFiyat.setText(film.getFilm_fiyat()+" TL");

        holder.imageViewFilmResim.setImageResource(mContext.getResources()
                .getIdentifier(film.getFilm_resim_ad(),"drawable",mContext.getPackageName()));

        holder.buttonSepeteEkle.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Toast.makeText(mContext,film.getFilm_ad()+" sepete eklendi",Toast.LENGTH_SHORT).show();
            }
        });
    }

    @Override
    public int getItemCount() {
        return filmlerList.size();
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

    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/rv"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />
</androidx.constraintlayout.widget.ConstraintLayout>
```
* card_film_tasarim.xml
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:orientation="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <androidx.cardview.widget.CardView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:layout_margin="10dp">

        <androidx.constraintlayout.widget.ConstraintLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent">

            <ImageView
                android:id="@+id/imageViewAyla"
                android:layout_width="200dp"
                android:layout_height="300dp"
                android:layout_marginTop="8dp"
                app:layout_constraintEnd_toEndOf="parent"
                app:layout_constraintHorizontal_bias="0.5"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toTopOf="parent"
                app:srcCompat="@drawable/ayla" />

            <TextView
                android:id="@+id/textViewFilmBaslik"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_marginTop="16dp"
                android:text="Ayla"
                android:textStyle="bold"
                app:layout_constraintEnd_toEndOf="parent"
                app:layout_constraintHorizontal_bias="0.5"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toBottomOf="@+id/imageViewAyla" />

            <TextView
                android:id="@+id/textViewFilmFiyat"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_marginTop="16dp"
                android:text="14.99 TL"
                android:textStyle="bold"
                app:layout_constraintEnd_toEndOf="parent"
                app:layout_constraintHorizontal_bias="0.5"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toBottomOf="@+id/textViewFilmBaslik" />

            <Button
                android:id="@+id/buttonSepeteEkle"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_marginTop="16dp"
                android:text="Sepete ekle"
                app:layout_constraintEnd_toEndOf="parent"
                app:layout_constraintHorizontal_bias="0.5"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toBottomOf="@+id/textViewFilmFiyat" />
        </androidx.constraintlayout.widget.ConstraintLayout>
    </androidx.cardview.widget.CardView>
</LinearLayout>
```
# TabsLayout Uygulama
![TabsLayout](https://user-images.githubusercontent.com/101557027/228714098-f5bd20ff-bc45-4f98-b2aa-708dbe221c14.gif)
--------------
* MainActivity
```
import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import androidx.fragment.app.Fragment;
import androidx.fragment.app.FragmentActivity;
import androidx.viewpager2.adapter.FragmentStateAdapter;
import androidx.viewpager2.widget.ViewPager2;

import android.os.Bundle;

import com.google.android.material.tabs.TabLayout;
import com.google.android.material.tabs.TabLayoutMediator;

import java.util.ArrayList;

public class MainActivity extends AppCompatActivity {

    private TabLayout tablayout;
    private ViewPager2 viewpager2;
    private ArrayList<Fragment> fragmentArrayList = new ArrayList<>();
    private ArrayList<String> fragmentBaslikList = new ArrayList<>();

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        tablayout = findViewById(R.id.tablayout);
        viewpager2 = findViewById(R.id.viewpager2);

        fragmentArrayList.add(new FragmentBirinci());
        fragmentArrayList.add(new Fragmentikinci());
        fragmentArrayList.add(new FragmentUcuncu());

        MyViewPagerAdapter adapter = new MyViewPagerAdapter(this);

        viewpager2.setAdapter(adapter);

        fragmentBaslikList.add("Bir");
        fragmentBaslikList.add("iki");
        fragmentBaslikList.add("Üç");

        new TabLayoutMediator(tablayout,viewpager2,
                (tab, position) ->tab.setText(fragmentBaslikList.get(position))).attach();
            tablayout.getTabAt(0).setIcon(R.drawable.resim);
    }

    private class MyViewPagerAdapter extends FragmentStateAdapter {

        public MyViewPagerAdapter(@NonNull FragmentActivity fragmentActivity) {
            super(fragmentActivity);
        }

        @NonNull
        @Override
        public Fragment createFragment(int position) {
            return fragmentArrayList.get(position);
        }

        @Override
        public int getItemCount() {
            return fragmentArrayList.size();
        }
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

    <com.google.android.material.tabs.TabLayout
        android:id="@+id/tablayout"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:background="#03A9F4"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:tabIconTint="@android:color/holo_orange_dark"
        app:tabIndicatorColor="#DA1212" />

    <androidx.viewpager2.widget.ViewPager2
        android:id="@+id/viewpager2"
        android:layout_width="0dp"
        android:layout_height="0dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/tablayout" />
</androidx.constraintlayout.widget.ConstraintLayout>
--------------------
* FragmentBirinci
```
import android.os.Bundle;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;

import androidx.annotation.NonNull;
import androidx.annotation.Nullable;
import androidx.fragment.app.Fragment;

public class FragmentBirinci extends Fragment {

    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater
                    , @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
        return inflater.inflate(R.layout.fragment_birinci_layout,container,false);
    }
}
```
* fragment_birinci_layout.xml
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:id="@+id/textView3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Birinci Fragment"
        android:textSize="48sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.5" />
</androidx.constraintlayout.widget.ConstraintLayout>
------------------
* Fragmentikinci
```
import android.os.Bundle;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;

import androidx.annotation.NonNull;
import androidx.annotation.Nullable;
import androidx.fragment.app.Fragment;

public class Fragmentikinci extends Fragment {

    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
        return inflater.inflate(R.layout.fragment_ikinci_layout,container,false);
    }
}
```
* fragment_ikinci_layout.xml
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:id="@+id/textView2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="İkinci Fragment"
        android:textSize="48sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.5" />
</androidx.constraintlayout.widget.ConstraintLayout>
```
----------------------
* FragmentUcuncu
```
import android.os.Bundle;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;

import androidx.annotation.NonNull;
import androidx.annotation.Nullable;
import androidx.fragment.app.Fragment;

public class FragmentUcuncu extends Fragment {

    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
        return inflater.inflate(R.layout.fragment_ucuncu_layout,container,false);
    }
}
```
* fragment_ucuncu_layout.xml
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:id="@+id/textView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Üçüncü Fragment"
        android:textSize="48sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.5" />
</androidx.constraintlayout.widget.ConstraintLayout>
```

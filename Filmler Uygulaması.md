# Filmler Uygulaması
![Filmler](https://user-images.githubusercontent.com/101557027/231468131-96403ee7-1a78-4fe0-9000-766b0b630cb5.gif)
* MainActivity
```
package com.example.filmleruygu;

import androidx.appcompat.app.AppCompatActivity;
import androidx.appcompat.widget.Toolbar;
import androidx.recyclerview.widget.LinearLayoutManager;
import androidx.recyclerview.widget.RecyclerView;

import android.os.Bundle;

import java.io.IOException;
import java.util.ArrayList;

public class MainActivity extends AppCompatActivity {
    private Toolbar toolbar;
    private RecyclerView kategoriRv;
    private ArrayList<Kategoriler> kategorilerArrayList;
    private KategoriAdapter adapter;
    private Veritabani vt;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        toolbar = findViewById(R.id.toolbar);
        kategoriRv = findViewById(R.id.kategoriRv);

        veritabaniKopyala();

        vt = new Veritabani(this);

        toolbar.setTitle("Kategoriler");
        setSupportActionBar(toolbar);

        kategoriRv.setHasFixedSize(true);
        kategoriRv.setLayoutManager(new LinearLayoutManager(this));

        kategorilerArrayList = new KategoriDAO().tumKategoriler(vt);

        adapter = new KategoriAdapter(this,kategorilerArrayList);
        kategoriRv.setAdapter(adapter);
    }

    public void veritabaniKopyala() {
        DatabaseCopyHelper helper = new DatabaseCopyHelper(this);

        try {
            helper.createDataBase();
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
        helper.openDataBase();
    }
}
```
* DatabaseCopyHelper
```
package com.example.filmleruygu;

import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;

import android.content.Context;
import android.database.SQLException;
import android.database.sqlite.SQLiteDatabase;
import android.database.sqlite.SQLiteException;
import android.database.sqlite.SQLiteOpenHelper;

public class DatabaseCopyHelper extends SQLiteOpenHelper  {


	//The Android's default system path of your application database.
	String DB_PATH =null;

	private static String DB_NAME = "filmler.sqlite";

	private SQLiteDatabase myDataBase;

	private final Context myContext;

	/**
	 * Constructor
	 * Takes and keeps a reference of the passed context in order to access to the application assets and resources.
	 * @param context
	 */
	public DatabaseCopyHelper(Context context) {

		super(context, DB_NAME, null, 1);
		this.myContext = context;
		DB_PATH="/data/data/"+context.getPackageName()+"/"+"databases/";

	}

	/**
	 * Creates a empty database on the system and rewrites it with your own database.
	 * */
	public void createDataBase() throws IOException{

		boolean dbExist = checkDataBase();

		if(dbExist){
			//do nothing - database already exist
		}else{

			//By calling this method and empty database will be created into the default system path
			//of your application so we are gonna be able to overwrite that database with our database.
			this.getReadableDatabase();

			try {

				copyDataBase();

			} catch (IOException e) {

				throw new Error("Error copying database");

			}
		}

	}

	/**
	 * Check if the database already exist to avoid re-copying the file each time you open the application.
	 * @return true if it exists, false if it doesn't
	 */
	private boolean checkDataBase(){

		SQLiteDatabase checkDB = null;

		try{
			String myPath = DB_PATH + DB_NAME;
			checkDB = SQLiteDatabase.openDatabase(myPath, null, SQLiteDatabase.OPEN_READONLY);

		}catch(SQLiteException e){

			//database does't exist yet.

		}

		if(checkDB != null){

			checkDB.close();

		}

		return checkDB != null ? true : false;
	}

	/**
	 * Copies your database from your local assets-folder to the just created empty database in the
	 * system folder, from where it can be accessed and handled.
	 * This is done by transfering bytestream.
	 * */
	private void copyDataBase() throws IOException{

		//Open your local db as the input stream
		InputStream myInput = myContext.getAssets().open(DB_NAME);


		// Path to the just created empty db
		String outFileName = DB_PATH + DB_NAME;

		//Open the empty db as the output stream
		OutputStream myOutput = new FileOutputStream(outFileName);

		//transfer bytes from the inputfile to the outputfile
		byte[] buffer = new byte[1024];
		int length;
		while ((length = myInput.read(buffer))>0){
			myOutput.write(buffer, 0, length);
		}

		//Close the streams
		myOutput.flush();
		myOutput.close();
		myInput.close();

	}

	public void openDataBase() throws SQLException{

		//Open the database
		String myPath = DB_PATH + DB_NAME;
		myDataBase = SQLiteDatabase.openDatabase(myPath, null, SQLiteDatabase.OPEN_READONLY);


	}

	@Override
	public synchronized void close() {

		if(myDataBase != null)
			myDataBase.close();

		super.close();

	}

	@Override
	public void onCreate(SQLiteDatabase db) {

	}

	@Override
	public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {

	}

	@Override
	public void onOpen(SQLiteDatabase db) {
		super.onOpen(db);
		db.disableWriteAheadLogging();
	}
	//return cursor

}

```
* DetayActivity
```
package com.example.filmleruygu;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.widget.ImageView;
import android.widget.TextView;

public class DetayActivity extends AppCompatActivity {
    private ImageView imageViewResim;
    private TextView textViewFilmAd,textViewFilmYil,textViewFilmYonetmen;
    private Filmler filmler;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_detay);

        imageViewResim = findViewById(R.id.imageViewResim);
        textViewFilmAd = findViewById(R.id.textViewFilmAd);
        textViewFilmYil = findViewById(R.id.textViewFilmYil);
        textViewFilmYonetmen = findViewById(R.id.textViewFilmYonetmen);

        filmler = (Filmler) getIntent().getSerializableExtra("nesne");

        textViewFilmAd.setText(filmler.getFilm_ad());
        textViewFilmYil.setText(String.valueOf(filmler.getFilm_yil()));
        textViewFilmYonetmen.setText(filmler.getYonetmen().getYonetmen_ad());

        imageViewResim.setImageResource(getResources().getIdentifier(filmler.getFilm_resim()
                ,"drawable"
                ,getPackageName()));

    }
}
```
* Filmler
```
package com.example.filmleruygu;

import java.io.Serializable;

public class Filmler implements Serializable {
    private int film_id;
    private String film_ad;
    private int film_yil;
    private String film_resim;
    private Kategoriler kategori;
    private Yonetmenler yonetmen;

    public Filmler() {
    }

    public Filmler(int film_id, String film_ad, int film_yil, String film_resim, Kategoriler kategori, Yonetmenler yonetmen) {
        this.film_id = film_id;
        this.film_ad = film_ad;
        this.film_yil = film_yil;
        this.film_resim = film_resim;
        this.kategori = kategori;
        this.yonetmen = yonetmen;
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

    public int getFilm_yil() {
        return film_yil;
    }

    public void setFilm_yil(int film_yil) {
        this.film_yil = film_yil;
    }

    public String getFilm_resim() {
        return film_resim;
    }

    public void setFilm_resim(String film_resim) {
        this.film_resim = film_resim;
    }

    public Kategoriler getKategori() {
        return kategori;
    }

    public void setKategori(Kategoriler kategori) {
        this.kategori = kategori;
    }

    public Yonetmenler getYonetmen() {
        return yonetmen;
    }

    public void setYonetmen(Yonetmenler yonetmen) {
        this.yonetmen = yonetmen;
    }
}

```
* FilmlerActivity
```
package com.example.filmleruygu;

import androidx.appcompat.app.AppCompatActivity;
import androidx.appcompat.widget.Toolbar;
import androidx.recyclerview.widget.RecyclerView;
import androidx.recyclerview.widget.StaggeredGridLayoutManager;

import android.os.Bundle;

import java.util.ArrayList;

public class FilmlerActivity extends AppCompatActivity {
    private Toolbar toolbar;
    private RecyclerView filmlerRv;
    private ArrayList<Filmler> filmlerArrayList;
    private FilmlerAdapter filmlerAdapter;
    private Kategoriler kategoriler;
    private Veritabani vt;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_filmler);

        toolbar = findViewById(R.id.toolbar);
        filmlerRv = findViewById(R.id.filmlerRv);

        vt = new Veritabani(this);

        kategoriler = (Kategoriler) getIntent().getSerializableExtra("kategori_nesne");

        toolbar.setTitle(kategoriler.getKategori_ad());
        setSupportActionBar(toolbar);

        filmlerArrayList = new FilmlerDao().tumFilmlerByKategoriId(vt,kategoriler.getKategori_id());

        filmlerRv.setHasFixedSize(true);
        filmlerRv.setLayoutManager(new StaggeredGridLayoutManager(2,StaggeredGridLayoutManager.VERTICAL));

        filmlerAdapter = new FilmlerAdapter(this,filmlerArrayList);
        filmlerRv.setAdapter(filmlerAdapter);
    }
}
```
* FilmlerAdapter
```
package com.example.filmleruygu;

import android.content.Context;
import android.content.Intent;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.ImageView;
import android.widget.TextView;

import androidx.annotation.NonNull;
import androidx.cardview.widget.CardView;
import androidx.recyclerview.widget.RecyclerView;

import java.util.List;

public class FilmlerAdapter extends RecyclerView.Adapter<FilmlerAdapter.CardTasarimTutucu> {
    private Context mContext;
    private List<Filmler> filmlerList;

    public FilmlerAdapter(Context mContext, List<Filmler> filmlerList) {
        this.mContext = mContext;
        this.filmlerList = filmlerList;
    }

    @NonNull
    @Override
    public CardTasarimTutucu onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        View view = LayoutInflater.from(parent.getContext()).inflate(R.layout.film_card_tasarim,parent,false);
        return new CardTasarimTutucu(view);
    }

    @Override
    public void onBindViewHolder(@NonNull CardTasarimTutucu holder, int position) {
        Filmler filmler = filmlerList.get(position);

            holder.textViewFilmAd.setText(filmler.getFilm_ad());

        holder.imageFilmResim.setImageResource(mContext.getResources().getIdentifier(filmler.getFilm_resim()
                ,"drawable",mContext.getPackageName()));

        holder.film_card.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(mContext,DetayActivity.class);

                intent.putExtra("nesne",filmler);

                mContext.startActivity(intent);
            }
        });
    }

    @Override
    public int getItemCount() {
        return filmlerList.size();
    }

    public class CardTasarimTutucu extends RecyclerView.ViewHolder {
        private CardView film_card;
        private ImageView imageFilmResim;
        private TextView textViewFilmAd;

        public CardTasarimTutucu(@NonNull View itemView) {
            super(itemView);

            film_card = itemView.findViewById(R.id.film_card);
            imageFilmResim = itemView.findViewById(R.id.imageFilmResim);
            textViewFilmAd = itemView.findViewById(R.id.textViewFilmAdi);
        }
    }
}
```
* FilmlerDao
```
package com.example.filmleruygu;

import android.annotation.SuppressLint;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;

import java.util.ArrayList;

public class FilmlerDao {

    public ArrayList<Filmler> tumFilmlerByKategoriId(Veritabani vt,int kategori_id) {
        ArrayList<Filmler> filmlerArrayList= new ArrayList<>();

        SQLiteDatabase db = vt.getWritableDatabase();

        Cursor c = db.rawQuery("SELECT * FROM kategoriler,filmler,yonetmenler " +
                "WHERE filmler.kategori_id =kategoriler.kategori_id " +
                "and filmler.yonetmen_id =yonetmenler.yonetmen_id " +
                "and filmler.kategori_id="+kategori_id,null);

        while (c.moveToNext()) {
            @SuppressLint("Range") Kategoriler k = new Kategoriler(c.getInt(c.getColumnIndex("kategori_id"))
                    ,c.getString(c.getColumnIndex("kategori_ad")));
            @SuppressLint("Range") Yonetmenler y = new Yonetmenler(c.getInt(c.getColumnIndex("yonetmen_id"))
                    ,c.getString(c.getColumnIndex("yonetmen_ad")));
            @SuppressLint("Range") Filmler f = new Filmler(c.getInt(c.getColumnIndex("film_id"))
                    ,c.getString(c.getColumnIndex("film_ad"))
                    ,c.getInt(c.getColumnIndex("film_yil"))
                    ,c.getString(c.getColumnIndex("film_resim")),k,y);

            filmlerArrayList.add(f);
        }

        return filmlerArrayList;
    }
}
```
* KategoriAdapter
```
package com.example.filmleruygu;

import android.content.Context;
import android.content.Intent;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.TextView;

import androidx.annotation.NonNull;
import androidx.cardview.widget.CardView;
import androidx.recyclerview.widget.RecyclerView;

import java.util.List;

public class KategoriAdapter extends RecyclerView.Adapter<KategoriAdapter.CardTasarimTutucu> {
    private Context mContext;
    private List<Kategoriler> kategorilerList;

    public KategoriAdapter(Context mContext, List<Kategoriler> kategorilerList) {
        this.mContext = mContext;
        this.kategorilerList = kategorilerList;
    }

    @NonNull
    @Override
    public CardTasarimTutucu onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {
        View view = LayoutInflater.from(parent.getContext()).inflate(R.layout.kategori_card_tasarim,parent,false);
        return new CardTasarimTutucu(view);
    }

    @Override
    public void onBindViewHolder(@NonNull CardTasarimTutucu holder, int position) {
        Kategoriler kategori = kategorilerList.get(position);

        holder.textViewKategoriAd.setText(kategori.getKategori_ad());

        holder.kategori_card.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(mContext,FilmlerActivity.class);

                intent.putExtra("kategori_nesne",kategori);

                mContext.startActivity(intent);
            }
        });
    }

    @Override
    public int getItemCount() {
        return kategorilerList.size();
    }

    public class CardTasarimTutucu extends RecyclerView.ViewHolder {
        private CardView kategori_card;
        private TextView textViewKategoriAd;

        public CardTasarimTutucu(@NonNull View itemView) {
            super(itemView);

            kategori_card = itemView.findViewById(R.id.kategori_card);
            textViewKategoriAd = itemView.findViewById(R.id.textViewKategoriAd);
        }
    }
}
```
* KategoriDao
```
package com.example.filmleruygu;

import android.annotation.SuppressLint;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;

import java.util.ArrayList;

public class KategoriDAO {

    public ArrayList<Kategoriler> tumKategoriler(Veritabani vt) {
        ArrayList<Kategoriler> kategorilerArrayList = new ArrayList<>();

        SQLiteDatabase db = vt.getWritableDatabase();

        Cursor c = db.rawQuery("SELECT * FROM kategoriler",null);

        while (c.moveToNext()) {
            @SuppressLint("Range") Kategoriler k = new Kategoriler(c.getInt(c.getColumnIndex("kategori_id"))
                    ,c.getString(c.getColumnIndex("kategori_ad")));

            kategorilerArrayList.add(k);
        }

        return kategorilerArrayList;
    }
}
```
* Kategoriler
```
package com.example.filmleruygu;

import java.io.Serializable;

public class Kategoriler implements Serializable {
    private int kategori_id;
    private String kategori_ad;

    public Kategoriler() {
    }

    public Kategoriler(int kategori_id, String kategori_ad) {
        this.kategori_id = kategori_id;
        this.kategori_ad = kategori_ad;
    }

    public int getKategori_id() {
        return kategori_id;
    }

    public void setKategori_id(int kategori_id) {
        this.kategori_id = kategori_id;
    }

    public String getKategori_ad() {
        return kategori_ad;
    }

    public void setKategori_ad(String kategori_ad) {
        this.kategori_ad = kategori_ad;
    }
}
```
* Veritabani
```
package com.example.filmleruygu;

import android.content.Context;
import android.database.sqlite.SQLiteDatabase;
import android.database.sqlite.SQLiteOpenHelper;

import androidx.annotation.Nullable;

public class Veritabani extends SQLiteOpenHelper {
    public Veritabani(@Nullable Context context) {
        super(context, "filmler.sqlite", null, 1);
    }

    @Override
    public void onCreate(SQLiteDatabase db) {
        db.execSQL("CREATE TABLE IF NOT EXISTS \"filmler\" (\n" +
                "\t`film_id`\tINTEGER PRIMARY KEY AUTOINCREMENT,\n" +
                "\t`film_ad`\tTEXT,\n" +
                "\t`film_yil`\tINTEGER,\n" +
                "\t`film_resim`\tTEXT,\n" +
                "\t`kategori_id`\tINTEGER,\n" +
                "\t`yonetmen_id`\tINTEGER,\n" +
                "\tFOREIGN KEY(`kategori_id`) REFERENCES `kategoriler`(`kategoril_id`),\n" +
                "\tFOREIGN KEY(`yonetmen_id`) REFERENCES `yonetmenler`(`yonetmen_id`)\n" +
                ")");
        db.execSQL("CREATE TABLE IF NOT EXISTS \"kategoriler\"  (\n" +
                "kategori_id INTEGER PRIMARY KEY AUTOINCREMENT,\n" +
                "kategori_ad TEXT\n" +
                ")");
        db.execSQL("CREATE TABLE IF NOT EXISTS \"yonetmenler\"  (\n" +
                "yonetmen_id INTEGER PRIMARY KEY AUTOINCREMENT,\n" +
                "yonetmen_ad TEXT\n" +
                ")");
    }

    @Override
    public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {
        db.execSQL("DROP TABLE IF EXISTS filmler");
        db.execSQL("DROP TABLE IF EXISTS kategoriler");
        db.execSQL("DROP TABLE IF EXISTS yonetmenler");
        onCreate(db);
    }
}
```
* Yonetmenler
```
package com.example.filmleruygu;

import java.io.Serializable;

public class Yonetmenler implements Serializable {
    private int yonetmen_id;
    private String yonetmen_ad;

    public Yonetmenler() {
    }

    public Yonetmenler(int yonetmen_id, String yonetmen_ad) {
        this.yonetmen_id = yonetmen_id;
        this.yonetmen_ad = yonetmen_ad;
    }

    public int getYonetmen_id() {
        return yonetmen_id;
    }

    public void setYonetmen_id(int yonetmen_id) {
        this.yonetmen_id = yonetmen_id;
    }

    public String getYonetmen_ad() {
        return yonetmen_ad;
    }

    public void setYonetmen_ad(String yonetmen_ad) {
        this.yonetmen_ad = yonetmen_ad;
    }
}
```
* activity_detay.xml
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".DetayActivity">

    <ImageView
        android:id="@+id/imageViewResim"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="55dp"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:srcCompat="@drawable/django" />

    <TextView
        android:id="@+id/textViewFilmAd"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="30dp"
        android:text="Django"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/imageViewResim" />

    <TextView
        android:id="@+id/textViewFilmYil"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="30dp"
        android:text="2008"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textViewFilmAd" />

    <TextView
        android:id="@+id/textViewFilmYonetmen"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="30dp"
        android:text="Yonetmen"
        android:textSize="20sp"
        android:textStyle="bold"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.5"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textViewFilmYil" />
</androidx.constraintlayout.widget.ConstraintLayout>
```
* activity_filmler.xml
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".FilmlerActivity">

    <androidx.appcompat.widget.Toolbar
        android:id="@+id/toolbar"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:background="?attr/colorPrimary"
        android:minHeight="?attr/actionBarSize"
        android:theme="?attr/actionBarTheme"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/filmlerRv"
        android:layout_width="0dp"
        android:layout_height="0dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/toolbar" />
</androidx.constraintlayout.widget.ConstraintLayout>
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

    <androidx.appcompat.widget.Toolbar
        android:id="@+id/toolbar"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:background="?attr/colorPrimary"
        android:minHeight="?attr/actionBarSize"
        android:theme="?attr/actionBarTheme"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

    <androidx.recyclerview.widget.RecyclerView
        android:id="@+id/kategoriRv"
        android:layout_width="0dp"
        android:layout_height="0dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/toolbar" />
</androidx.constraintlayout.widget.ConstraintLayout>
```
* film_card_tasarim.xml
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="wrap_content">

    <androidx.cardview.widget.CardView
        android:id="@+id/film_card"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent">

        <androidx.constraintlayout.widget.ConstraintLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent">

            <ImageView
                android:id="@+id/imageFilmResim"
                android:layout_width="150dp"
                android:layout_height="200dp"
                app:layout_constraintBottom_toBottomOf="parent"
                app:layout_constraintEnd_toEndOf="parent"
                app:layout_constraintHorizontal_bias="0.498"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toTopOf="parent"
                app:layout_constraintVertical_bias="0.26"
                app:srcCompat="@drawable/django" />

            <TextView
                android:id="@+id/textViewFilmAdi"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_margin="6dp"
                android:layout_marginTop="16dp"
                android:text="TextView"
                android:textStyle="bold"
                app:layout_constraintBottom_toBottomOf="parent"
                app:layout_constraintEnd_toEndOf="parent"
                app:layout_constraintHorizontal_bias="0.498"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toBottomOf="@+id/imageFilmResim" />
        </androidx.constraintlayout.widget.ConstraintLayout>
    </androidx.cardview.widget.CardView>
</androidx.constraintlayout.widget.ConstraintLayout>
```
* kategori_card_tasarim.xml
```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="wrap_content">

    <androidx.cardview.widget.CardView
        android:id="@+id/kategori_card"
        android:layout_width="match_parent"
        android:layout_height="50dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.5">

        <androidx.constraintlayout.widget.ConstraintLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent">

            <TextView
                android:id="@+id/textViewKategoriAd"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="Drama"
                android:textSize="16sp"
                android:textStyle="bold"
                app:layout_constraintBottom_toBottomOf="parent"
                app:layout_constraintEnd_toEndOf="parent"
                app:layout_constraintHorizontal_bias="0.5"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toTopOf="parent"
                app:layout_constraintVertical_bias="0.5" />
        </androidx.constraintlayout.widget.ConstraintLayout>
    </androidx.cardview.widget.CardView>
</androidx.constraintlayout.widget.ConstraintLayout>
```

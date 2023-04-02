# Filmler Veritabanı Çalısması
![Desktop Screenshot 2023 04 02 - 18 07 43 24](https://user-images.githubusercontent.com/101557027/229361688-2f1132bb-e212-480c-9131-17cb2213839a.png)
---------
* MainActivity
```
import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.util.Log;

import com.example.filmlercalismasi.dao.DatabaseCopyHelper;
import com.example.filmlercalismasi.dao.FilmlerDao;
import com.example.filmlercalismasi.dao.VeriTabaniYardimcisi;
import com.example.filmlercalismasi.objects.Filmler;

import java.io.IOException;
import java.util.ArrayList;

public class MainActivity extends AppCompatActivity {
    private VeriTabaniYardimcisi vt = new VeriTabaniYardimcisi(this);
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        kopyala();

        ArrayList<Filmler> filmlerArrayList = new FilmlerDao().tumFilmler(vt);

        for(Filmler k : filmlerArrayList) {
            Log.e("*******","*******");
            Log.e("Film id",String.valueOf(k.getFilm_id()));
            Log.e("Film ad",k.getFilm_ad());
            Log.e("Film yıl",String.valueOf(k.getFilm_yil()));
            Log.e("Film resim",k.getFilm_resim());
            Log.e("Film kategori",k.getKategori().getKategori_ad());
            Log.e("Film ad",k.getYonetmen().getYonetmen_ad());
            Log.e("*******","*******");
        }
    }

    public void kopyala(){
        DatabaseCopyHelper helper = new DatabaseCopyHelper(this);
        try {
            helper.createDataBase();
        }catch (IOException e){
            e.printStackTrace();
        }

        helper.openDataBase();
    }
}
```
* Package(dao) DatabaseCopyHelper
```
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
* Package(dao) FilmlerDao
```
import android.annotation.SuppressLint;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;

import com.example.filmlercalismasi.objects.Filmler;
import com.example.filmlercalismasi.objects.Kategoriler;
import com.example.filmlercalismasi.objects.Yonetmenler;

import java.util.ArrayList;

public class FilmlerDao {

    public ArrayList<Filmler> tumFilmler(VeriTabaniYardimcisi vt) {
        ArrayList<Filmler> filmlerArrayList = new ArrayList<>();
        SQLiteDatabase db = vt.getWritableDatabase();
        Cursor c = db.rawQuery("SELECT * FROM filmler,kategoriler,yonetmenler " +
                "WHERE filmler.kategori_id = kategoriler.kategori_id " +
                "and filmler.yonetmen_id = yonetmenler.yonetmen_id",null);

        while (c.moveToNext()){
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
* Package(dao) kategorilerDao
```
import android.annotation.SuppressLint;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;

import com.example.filmlercalismasi.objects.Kategoriler;

import java.util.ArrayList;

public class kategorilerDao {

    public ArrayList<Kategoriler> tumKategoriler(VeriTabaniYardimcisi vt) {
        ArrayList<Kategoriler> kategorilerArrayList = new ArrayList<>();
        SQLiteDatabase db = vt.getWritableDatabase();
        Cursor c = db.rawQuery("SELECT * FROM kategoriler",null);

        while (c.moveToNext()){
            @SuppressLint("Range") Kategoriler k = new Kategoriler(c.getInt(c.getColumnIndex("kategori_id"))
                    ,c.getString(c.getColumnIndex("kategori_ad")));

            kategorilerArrayList.add(k);
        }
        return kategorilerArrayList;
    }
}
```
* Package(dao) VeriTabaniYardimcisi
```
import android.content.Context;
import android.database.sqlite.SQLiteDatabase;
import android.database.sqlite.SQLiteOpenHelper;

import androidx.annotation.Nullable;

public class VeriTabaniYardimcisi extends SQLiteOpenHelper {

    public VeriTabaniYardimcisi(@Nullable Context context) {
        super(context,"filmler.sqlite",null,1);
    }

    @Override
    public void onCreate(SQLiteDatabase db) {

        db.execSQL("CREATE TABLE IF NOT EXISTS kategoriler  (\n" +
                "kategori_id INTEGER PRIMARY KEY AUTOINCREMENT,\n" +
                "kategori_ad TEXT\n" +
                ")");
        db.execSQL("CREATE TABLE IF NOT EXISTS yonetmenler  (\n" +
                "yonetmen_id INTEGER PRIMARY KEY AUTOINCREMENT,\n" +
                "yonetmen_ad TEXT\n" +
                ")");
        db.execSQL("CREATE TABLE IF NOT EXISTS \"filmler\" (\n" +
                "\t`film_id`\tINTEGER PRIMARY KEY AUTOINCREMENT,\n" +
                "\t`film_ad`\tTEXT,\n" +
                "\t`film_yil`\tINTEGER,\n" +
                "\t`film_resim`\tTEXT,\n" +
                "\t`kategori_id`\tINTEGER,\n" +
                "\t`yonetmen_id`\tINTEGER,\n" +
                "\tFOREIGN KEY(`kategori_id`) REFERENCES `kategoriler`(`kategori_id`),\n" +
                "\tFOREIGN KEY(`yonetmen_id`) REFERENCES `yonetmenler`(`yonetmen_id`)\n" +
                ")");
    }

    @Override
    public void onUpgrade(SQLiteDatabase db, int oldVersion, int newVersion) {
        db.execSQL("DROP TABLE IF EXISTS kategoriler");
        db.execSQL("DROP TABLE IF EXISTS yonetmenler");
        db.execSQL("DROP TABLE IF EXISTS filmler");
        onCreate(db);

    }
}
```
* Package(objects) Filmler
```
public class Filmler {
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
* Package(objects) Kategoriler
```
public class Kategoriler {
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
* Package(objects) Yonetmenler
```
public class Yonetmenler {
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

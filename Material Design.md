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

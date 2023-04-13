# SMS YAKALAYICI
![Sms-ya](https://user-images.githubusercontent.com/101557027/231814648-eb049975-f5df-42e6-adf6-63d23bc868b2.gif)
* MainActivity
```
package com.example.smsyakalama;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}
```
* SmsYakalayici new -> other -> Broadcast Receiver
```
package com.example.smsyakalama;

import static android.telephony.SmsMessage.createFromPdu;

import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;
import android.os.Bundle;
import android.telephony.SmsManager;
import android.telephony.SmsMessage;
import android.widget.Toast;

public class SmsYakalayici extends BroadcastReceiver {
    SmsManager sms = SmsManager.getDefault();
    @Override
    public void onReceive(Context context, Intent intent) {
        Bundle b = intent.getExtras();

        Object [] pdusObj = (Object[]) b.get("pdus");

        for (int i = 0; i<pdusObj.length; i++) {
            SmsMessage guncelMesaj = createFromPdu((byte[]) pdusObj[i]);

            String telNo = guncelMesaj.getDisplayOriginatingAddress();
            String mesaj = guncelMesaj.getDisplayMessageBody();

            Toast.makeText(context,"Tel No : "+telNo+" Mesaj : "+mesaj,Toast.LENGTH_SHORT).show();
        }
    }
}
```
* AndroidManifest.xml
```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <uses-permission android:name="android.permission.RECEIVE_SMS"/>
    <uses-permission android:name="android.permission.READ_SMS"/>
    <uses-permission android:name="android.permission.SEND_SMS"/>

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:supportsRtl="true"
        android:theme="@style/Theme.SmsYakalama"
        tools:targetApi="31">
        <receiver
            android:name=".SmsYakalayici"
            android:exported="true">
            <intent-filter>
                <action android:name="android.provider.Telephony.SMS_RECEIVED"/>
            </intent-filter>
        </receiver>

        <activity
            android:name=".MainActivity"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
        </activity>
    </application>

</manifest>
```


# Ex.No:4 Create Your Own Content Providers to get Contacts details.


## AIM:

To create your own content providers to get contacts details using Android Studio.

## EQUIPMENTS REQUIRED:

Android Studio(Latest Version)

## ALGORITHM:

Step 1: Open Android Stdio and then click on File -> New -> New project.

Step 2: Then type the Application name as “contentprovider″ and click Next. 

Step 3: Then select the Minimum SDK as shown below and click Next.

Step 4: Then select the Empty Activity and click Next. Finally click Finish.

Step 5: Design layout in activity_main.xml.

Step 6: Get contacts details and Display details give in MainActivity file.

Step 7: Save and run the application.

## PROGRAM:
```txt
Program to print the contact name and phone number using content providers.
Developed by:SURYANARAYANAN T
Registeration Number :212224040341
```
### AndroidManifist.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">
<uses-permission android:name="android.permission.READ_CONTACTS" />
    <uses-permission android:name="android.permission.WRITE_CONTACTS" />

    <application
        android:allowBackup="true"
        android:dataExtractionRules="@xml/data_extraction_rules"
        android:fullBackupContent="@xml/backup_rules"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.ContentProvider">
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
### MainActivity.java
```java
package com.example.contentprovider;

import android.Manifest;
import android.content.ContentResolver;
import android.content.pm.PackageManager;
import android.database.Cursor;
import android.net.Uri;
import android.os.Bundle;
import android.provider.ContactsContract;
import android.util.Log;
import android.view.View;

import androidx.activity.EdgeToEdge;
import androidx.appcompat.app.AppCompatActivity;
import androidx.core.app.ActivityCompat;
import androidx.core.content.ContextCompat;

public class MainActivity extends AppCompatActivity
{

    @Override
    protected void onCreate(Bundle savedInstanceState)
    {
        super.onCreate(savedInstanceState);
        EdgeToEdge.enable(this);
        setContentView(R.layout.activity_main);
    }
    public void btnGetContactPressed(View v)
    {
        getPhoneContacts();
    }

    public void getPhoneContacts()
    {
        if(ContextCompat.checkSelfPermission(this , Manifest.permission.READ_CONTACTS) != PackageManager.PERMISSION_GRANTED)
        {
            ActivityCompat.requestPermissions(this , new String[] {Manifest.permission.READ_CONTACTS} , 1);
            return;
        }

        ContentResolver contentResolver = getContentResolver();
        Uri uri = ContactsContract.CommonDataKinds.Phone.CONTENT_URI;
        try (Cursor cursor = contentResolver.query(uri, null, null, null, null))
        {
            if (cursor != null && cursor.getCount() > 0)
            {
                Log.i("CONTACT_PROVIDER_DEMO",
                        "TOTAL # of Contacts ::: " + cursor.getCount());

                while (cursor.moveToNext())
                {
                    String contactName = cursor.getString(
                            cursor.getColumnIndexOrThrow(ContactsContract.CommonDataKinds.Phone.DISPLAY_NAME));
                    String contactNumber = cursor.getString(
                            cursor.getColumnIndexOrThrow(ContactsContract.CommonDataKinds.Phone.NUMBER));

                    Log.i("CONTACT_PROVIDER_DEMO",
                            "Contact Name ::: " + contactName + " Contact Number ::: " + contactNumber);
                }
            }
            else
            {
                Log.e("CONTACT_PROVIDER_DEMO", "No contacts found or cursor is null");
            }
        }
    }



}
```
### activity_main.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <Button
        android:id="@+id/button"
        android:layout_width="153dp"
        android:layout_height="65dp"
        android:onClick="btnGetContactPressed"
        android:text="Get Contacts"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.588" />

    <TextView
        android:id="@+id/textView"
        android:layout_width="233dp"
        android:layout_height="100dp"
        android:layout_marginTop="152dp"
        android:fontFamily="sans-serif-medium"
        android:text="ContentProvider"
        android:textColor="#673AB7"
        android:textSize="24sp"
        android:typeface="serif"
        app:layout_constraintBottom_toTopOf="@+id/button"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.825"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintVertical_bias="0.8" />
</androidx.constraintlayout.widget.ConstraintLayout>
```
## OUTPUT
### MainActivity.java
<img width="1920" height="1080" alt="Screenshot 2025-09-28 171913" src="https://github.com/user-attachments/assets/430b2c52-6e29-4209-a865-70517683d9c5" /><br>
### AndroidManifist.xml
<img width="1920" height="1080" alt="Screenshot 2025-09-28 171900" src="https://github.com/user-attachments/assets/872207cb-eac3-45c4-acdd-6a82e8f8541a" /><br>
### activity_main.xml
<img width="1920" height="1080" alt="Screenshot 2025-09-28 171851" src="https://github.com/user-attachments/assets/c9cf6874-8d97-4eb2-bdf9-19cb26e8196d" /><br>
### ContentProvider App
<img width="367" height="812" alt="Screenshot 2025-09-28 165948" src="https://github.com/user-attachments/assets/a9aad831-9825-4479-b437-f27d412310f7" /><br>
### Contacts from Mobile Via LogCat
<img width="1920" height="1080" alt="Screenshot 2025-09-28 171133" src="https://github.com/user-attachments/assets/ae44d590-a64f-46b0-b9c9-a41111372a12" /><br>




## RESULT
Thus a Simple Android Application create your own content providers to get contacts details using Android Studio is developed and executed successfully.

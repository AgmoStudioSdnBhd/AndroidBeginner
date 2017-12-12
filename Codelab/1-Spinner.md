# A Simple List View
## Create a ListView layout

1. Create a new Android Studio project

2. Update the layout of your `activity_main.xml` to include `Spinner`.
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="com.agmostudio.myapplication.MainActivity">

    <Spinner
        android:id="@+id/spinner"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"/>
</LinearLayout>
```

## Set array data to your layout
1. Update your `MainActivity` with code below.
  ```java
  import android.os.Bundle;
  import android.support.v7.app.AppCompatActivity;
  import android.widget.ArrayAdapter;
  import android.widget.Spinner;

  public class MainActivity extends AppCompatActivity {

      @Override
      protected void onCreate(Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          setContentView(R.layout.activity_main);

          String[] array = {"Android", "iPhone", "Windows", "Blackberry", "Ubuntu", "Windows7", "macOS"};

          ArrayAdapter adapter = new ArrayAdapter<>(this,
                  android.R.layout.simple_list_item_1, array);

          Spinner spinner = findViewById(R.id.spinner);
          spinner.setAdapter(adapter);
      }
  }
  ```

## Result
![Spinner](https://github.com/AgmoStudioSdnBhd/AndroidBeginner/raw/master/art/spinner.png)

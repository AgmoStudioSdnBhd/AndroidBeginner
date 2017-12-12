# A Custom List View
## Create a ListView layout

1. Create a new Android Studio project

2. Update the layout of your `activity_main.xml` to include `ListView`.
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="com.agmostudio.myapplication.MainActivity">

    <ListView
        android:id="@+id/listview"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>
</LinearLayout>
```
3. Add a new layout file `list_item.xml`
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
              android:layout_width="match_parent"
              android:layout_height="wrap_content"
              android:orientation="vertical"
              android:padding="8dp">

    <TextView
        android:id="@+id/text1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:textSize="16sp"
        android:textStyle="bold"/>

    <TextView
        android:id="@+id/text2"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:textSize="16sp"/>

</LinearLayout>
```

## Set array data to your layout
1. Prepare data for your list view
```java
String[] array = {"Android", "iPhone", "Windows", "Blackberry", "Ubuntu", "Windows7", "macOS"};
String[] subTitleArray = {"Android Sub", "iPhone Sub", "Windows Sub", "Blackberry Sub", "Ubuntu Sub", "Windows7 Sub", "macOS Sub"};
```

2. Add `DynamicAdapter` in your `MainActivity`
```java
class DynamicAdapter extends ArrayAdapter {

    public DynamicAdapter() {
        super(MainActivity.this, R.layout.list_item, array);
    }

    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        View rowView = convertView;
        if (rowView == null) {
            LayoutInflater inflater = (LayoutInflater) getApplicationContext().getSystemService(Context.LAYOUT_INFLATER_SERVICE);
            rowView = inflater.inflate(R.layout.list_item, parent, false);
        }

        TextView label = rowView.findViewById(R.id.text1);
        label.setText(array[position]);

        TextView label2 = rowView.findViewById(R.id.text2);
        label2.setText(subTitleArray[position]);

        return rowView;
    }
}
```
3. Set the adapter to your list view
```java
  ListView listView = findViewById(R.id.listview);
  listView.setAdapter(new DynamicAdapter());
```
4. Your final `MainActivity` should be as below
  ```java
  import android.content.Context;
  import android.os.Bundle;
  import android.support.v7.app.AppCompatActivity;
  import android.view.LayoutInflater;
  import android.view.View;
  import android.view.ViewGroup;
  import android.widget.ArrayAdapter;
  import android.widget.ListView;
  import android.widget.TextView;

  public class MainActivity extends AppCompatActivity {

      String[] array = {"Android", "iPhone", "Windows", "Blackberry", "Ubuntu", "Windows7", "macOS"};
      String[] subTitleArray = {"Android Sub", "iPhone Sub", "Windows Sub", "Blackberry Sub", "Ubuntu Sub", "Windows7 Sub", "macOS Sub"};


      @Override
      protected void onCreate(Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          setContentView(R.layout.activity_main);

          ListView listView = findViewById(R.id.listview);
          listView.setAdapter(new DynamicAdapter());
      }

      class DynamicAdapter extends ArrayAdapter {

          public DynamicAdapter() {
              super(MainActivity.this, R.layout.list_item, array);
          }

          @Override
          public View getView(int position, View convertView, ViewGroup parent) {
              View rowView = convertView;
              if (rowView == null) {
                  LayoutInflater inflater = (LayoutInflater) getApplicationContext().getSystemService(Context.LAYOUT_INFLATER_SERVICE);
                  rowView = inflater.inflate(R.layout.list_item, parent, false);
              }

              TextView label = rowView.findViewById(R.id.text1);
              label.setText(array[position]);

              TextView label2 = rowView.findViewById(R.id.text2);
              label2.setText(subTitleArray[position]);

              return rowView;
          }
      }
  }
  ```

## Trigger OnClick event
1. Update your `getView` method to have an `OnClickListener` with a `Toast` message
  ```java
@Override
public View getView(int position, View convertView, ViewGroup parent) {
    ...

    final String text = array[position];
    rowView.setOnClickListener(new View.OnClickListener() {
        @Override
        public void onClick(View view) {
            Toast.makeText(MainActivity.this, text, Toast.LENGTH_SHORT).show();
        }
    });

    return rowView;
}
```

2. Updated `DynamicAdapter` as below
  ```java
class DynamicAdapter extends ArrayAdapter {

    public DynamicAdapter() {
        super(MainActivity.this, R.layout.list_item, array);
    }

    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        View rowView = convertView;
        if (rowView == null) {
            LayoutInflater inflater = (LayoutInflater) getApplicationContext().getSystemService(Context.LAYOUT_INFLATER_SERVICE);
            rowView = inflater.inflate(R.layout.list_item, parent, false);
        }

        TextView label = rowView.findViewById(R.id.text1);
        label.setText(array[position]);

        TextView label2 = rowView.findViewById(R.id.text2);
        label2.setText(subTitleArray[position]);

        final String text = array[position];
        rowView.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Toast.makeText(MainActivity.this, text, Toast.LENGTH_SHORT).show();
            }
        });

        return rowView;
    }
}
```

## Result
![SimpleList](https://github.com/AgmoStudioSdnBhd/AndroidBeginner/raw/master/art/customlistview.png)

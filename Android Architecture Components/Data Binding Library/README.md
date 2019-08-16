# [Data Binding Library](https://developer.android.com/topic/libraries/data-binding/) 

The Data Binding Library is a support library that allows you to `bind UI components in your layouts to data sources` in your app using a 
declarative format rather than programmatically.

* **Note** - If we use `findViewById` to reference to a view, when we search for a view after it has been created or recreated, Android has to 
traverse the View Hierarchy to find it for us at runtime. For large View Hierarchy, it can slow down the app for the user. 
To fix this there is a techinque called `Data Binding`, that allow us to connect a layout to an activity or fragment at compile time.
The compiler generates a helper class called a `binding class`, when the activity is created, so is an instance of the binding class and 
then we can access the views from the binding class without any extra overhead.

One thing I know about Data binding is that **it gonna make us an offer that we can’t refuse**

### What does it offer us?

 * Make findViewById totally obsolete
 * Encourage to separate UI logic and business logic
 * Make easy to synchronize between data sources and UI elements
 * Provides a way to bind event listener using lambda or method reference from xml
 * Provides a way to bind custom setters method or rename setters method of view’s attributes
 
### How?

## How can we integrate in our Android app

* In build.gradle file, add the following gradle property which enabled data binding,
```
android {
    ...
    dataBinding {
        enabled = true
    }
}
```

* In layout file, generally, we have ViewGroup (E.g. RelativeLayout or LinearLayout) as top in View hierarchy. But here, we will make `<layout>` 
tag as most `parent` tag or `root` tag. After adding it, build system will process it for data binding:

```xml
<?xml version="1.0" encoding="utf-8"?>

<layout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools">

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical"
        android:padding="16dp"
        tools:context="com.androidbytes.databindingdemo.MainActivity">

        <TextView
            android:id="@+id/text_view_name"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textColor="@android:color/black"
            android:textSize="24sp" />

        <TextView
            android:id="@+id/text_view_occupation"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textColor="@android:color/black"
            android:textSize="16sp" />

    </LinearLayout>
</layout>
```

* After above step, `binding class` will be generated based on the same name of layout file (e.g. activity_main’s binding class will be 
generated ActivityMainBinding). We can set setContentView using `DataBindingUtil` like:

```kotlin
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

//        Before Data Binding
//        setContentView(R.layout.activity_main);
//
//        TextView textViewName = (TextView) findViewById(R.id.text_view_name);
//        TextView textViewOccupation = (TextView) findViewById(R.id.text_view_occupation);
//
//        textViewName.setText("Elon Musk");
//        textViewOccupation.setText("Entrepreneur, Engineer, Inventor, Investor");


//        After Data Binding
        ActivityMainBinding binding = DataBindingUtil.setContentView(this, R.layout.activity_main);

        binding.textViewName.setText("Elon Musk");
        binding.textViewOccupation.setText("Entrepreneur, Engineer, Inventor, Investor");
        
//      Also you can use it on ClickListeners
//      binding.btn.setOnClickListener {
//      ------ }
//      Or you can use Kotlin apply{} function for multiple buttons
//      binding.apply {
//        btn1.setOnClickListener { -- }
//        btn2.setOnClickListener { -- }
//        btn3.setOnClickListener { -- }
//      }
    }
}
```

* That’s it. Just run the project and check output. It will exactly the same but with better performance. Now we don’t have to write 
`findViewByIds`.


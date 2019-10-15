# RecyclerView

* ## Add a RecyclerView to the Main Activity

```xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context="com.zeph7.myrecyclerviewapp.MainActivity">


    <android.support.v7.widget.RecyclerView
        android:id="@+id/recyclerView1"
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:layout_marginBottom="8dp"
        android:layout_marginEnd="8dp"
        android:layout_marginStart="8dp"
        android:layout_marginTop="8dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        tools:layout_editor_absoluteX="8dp"
        tools:layout_editor_absoluteY="8dp" />

</android.support.constraint.ConstraintLayout>
```

* ## Create RecyclerView row Layout

Create a new layout file called “item_layout.xml”

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical" android:layout_width="match_parent"
    android:layout_height="wrap_content">

    <android.support.v7.widget.CardView
        android:layout_margin="5dp"
        android:layout_width="match_parent"
        android:layout_height="match_parent" >
        <LinearLayout
            android:padding="10dp"
            android:orientation="vertical"
            android:layout_width="match_parent"
            android:layout_height="wrap_content">
            <TextView
                android:textAppearance="@style/Base.TextAppearance.AppCompat.Large"
                android:id="@+id/txtName"
                android:text="Name"
                android:layout_width="match_parent"
                android:layout_height="wrap_content" />
            <TextView
                android:textAppearance="@style/Base.TextAppearance.AppCompat.Medium"
                android:text="Occupation"
                android:id="@+id/txtTitle"
                android:layout_width="match_parent"
                android:layout_height="wrap_content" />
        </LinearLayout>
    </android.support.v7.widget.CardView>

</LinearLayout>
```

This will be the template / prototype of the row in the RecyclerView

* ## Next, create a User model / Class

```kotlin
package com.zeph7.myrecyclerviewapp

data class User(val name: String, val title: String)
```

* ## Create Data Adapter Class

```kotlin
package com.zeph7.myrecyclerviewapp

import android.support.v7.widget.RecyclerView
import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import android.widget.TextView

class CustomAdapter(val userList: ArrayList<User>): RecyclerView.Adapter<CustomAdapter.ViewHolder>() {

    override fun onCreateViewHolder(parent: ViewGroup, viewType: Int): ViewHolder {
        val view = LayoutInflater.from(parent.context).inflate(R.layout.item_layout, parent, false)
        return ViewHolder(view)
    }

    override fun getItemCount(): Int {
        return userList.size
    }
    
    override fun onBindViewHolder(holder: ViewHolder, position: Int) {
        if (holder != null)
            holder.bindView(userList[position])
    }

    inner class ViewHolder(itemView: View): RecyclerView.ViewHolder(itemView){
        // here, you can instantiate objects of the views of the row item in recycler view
        val txtName = itemView.findViewById<TextView>(R.id.txtName)
        val txtTitle = itemView.findViewById<TextView>(R.id.txtTitle)
        
        fun bindView(user: User) {
            // here, you can bind the data coming from userList to the views of each row item
            txtName.text = user.name
            txtTitle.text = user.title
        }

    }

}
```

* ## Connect RecyclerView to CustomAdapter

```kotlin
package com.zeph7.myrecyclerviewapp

import android.support.v7.app.AppCompatActivity
import android.os.Bundle
import android.support.v7.widget.LinearLayoutManager
import android.support.v7.widget.RecyclerView
import android.widget.LinearLayout

class MainActivity : AppCompatActivity() {
    private lateinit var recyclerView: RecyclerView
    
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        recyclerView = findViewById<RecyclerView>(R.id.recyclerView1)
        recyclerView.layoutManager = LinearLayoutManager(this, LinearLayout.VERTICAL, false)
        
        val users = ArrayList<User>()
        users.add(User("Paul", "Mr"))
        users.add(User("Jane", "Miss"))
        users.add(User("John", "Dr"))
        users.add(User("Amy", "Mrs"))

        var adapter = CustomAdapter(users)
        recyclerView.adapter = adapter
    }
}
```


![](https://miro.medium.com/max/500/1*lVfiPligkFCM7SIVbwcb8Q.png)


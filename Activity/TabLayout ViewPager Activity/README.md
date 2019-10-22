# TabLayout with Viewpager Activity

![](https://i.stack.imgur.com/cc33c.jpg)

* ## Create an Activity layout with TabLayout and ViewPager :

Firstly, drag the TabLayout to the layout file of the Activity.

Now, set a divider or line bottom to the TabLayout to make it seperate from ViewPager

Finally, drag the ViewPager that's gonna hold the Fragments later. Also can create the Fragment for each Tabs

```xml
<?xml version="1.0" encoding="utf-8"?>
<android.support.constraint.ConstraintLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:tools="http://schemas.android.com/tools"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:background="@color/colorMainBackground"
        tools:context=".Activities.MessagesActivity">

    <ImageView
            android:layout_width="24dp"
            android:layout_height="24dp"
            app:srcCompat="@drawable/ic_back"
            android:id="@+id/iconBack"

            app:layout_constraintTop_toTopOf="parent"
            android:layout_marginTop="20dp"
            app:layout_constraintStart_toStartOf="parent"
            android:layout_marginLeft="12dp"
            android:layout_marginStart="12dp"/>

    <TextView
            android:text="Simple Tabs"
            android:textStyle="bold"
            android:textSize="18sp"
            android:lineHeight="21sp"
            android:layout_width="83dp"
            android:layout_height="22dp"
            android:id="@+id/textView"

            app:layout_constraintTop_toTopOf="parent"
            android:layout_marginTop="21dp"
            android:layout_marginLeft="16dp"
            android:layout_marginStart="16dp"
            app:layout_constraintStart_toEndOf="@+id/iconBack"/>


    <!-- for showing Tabs: ONE | TWO | THREE -->
    <android.support.design.widget.TabLayout
            android:id="@+id/mainTabs"
            android:background="@color/colorMainBackground"
            android:layout_width="match_parent"
            android:layout_height="35dp"
            
            app:tabTextAppearance="@style/customTabLayout"    // for setting its custom style
            app:tabMaxWidth="0dp"
            app:tabGravity="center"   // tabGravity : center (makes the tabs set according to its width) | fill (makes the tabs fill entire width)
            app:tabMode="scrollable"    // tabMode : scrollable (makes it scrollable from left) | fixed (makes it fixed)
            app:tabContentStart="25dp"    // to give tabs a left margin

            app:layout_constraintTop_toTopOf="parent"
            android:layout_marginTop="60dp"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintStart_toStartOf="parent"/>

    <!-- for the divider line bottom to the mainTabs and up on the ViewPager -->
    <View
            android:id="@+id/viewId"
            android:layout_below="@+id/mainTabs"
            android:background="@color/colorMessagesViewPagerLine"
            android:layout_width="match_parent"
            android:layout_height="1dp"

            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintHorizontal_bias="0.0"
            app:layout_constraintTop_toBottomOf="@+id/mainTabs"/>

    <!-- for infusing different fragments while selecting corresponding tabs on mainTabs -->
    <android.support.v4.view.ViewPager
            android:id="@+id/sectionViewPagerID"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"

            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintHorizontal_bias="1.0"
            app:layout_constraintTop_toBottomOf="@+id/viewId"/>

</android.support.constraint.ConstraintLayout>
```

```
<!-- Custom TabLayout Style -->
    <style name="customTabLayout" parent="TextAppearance.Design.Tab">
        <item name="textAllCaps">false</item>
        <item name="android:fontFamily">Noto Sans</item>
        <item name="android:textSize">17sp</item>
    </style>
```

* ## Create a SectionPagerAdapter :

This will be the adapter for the ViewPager to show corresponding Fragments. And also you can set here to show the title on the Tabs

```kotlin
class SectionPagerAdapter(fm: FragmentManager) : FragmentPagerAdapter(fm) {
    override fun getItem(position: Int): Fragment {
        when(position) {
            0 -> return OneFragment()
            1 -> return TwoFragment()
            2 -> return ThreeFragment()
        }
        return null!!
    }

    override fun getCount(): Int {
        return 3
    }

    // sets the title on TabLayout for corresponding Tabs
    override fun getPageTitle(position: Int): CharSequence? {
        when(position) {
            0 -> return "ONE"
            1 -> return "TWO"
            2 -> return "THREE"
        }
        return null!!
    }
}
```

* ## MainActivity :

Finally, set the SectionAdapter to the Viewpager. And also connect the TabLayout with the ViewPager

```kotlin
class MessagesActivity : AppCompatActivity() {

    private lateinit var messageSectionAdapter: SectionPagerAdapter

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_messages)

        // sets the SectionPagerAdapter to the ViewPager
        sectionAdapter = SectionPagerAdapter(supportFragmentManager)
        sectionViewPagerID.adapter = sectionAdapter
        
        // connects the TabLayout with the ViewPager
        mainTabs.setupWithViewPager(sectionViewPagerID)
        
        // sets the color of text on tabs : (Normal, Highlight)
        mainTabs.setTabTextColors(Color.GREY, Color.WHITE)

        iconBack.setOnClickListener {
            super.onBackPressed()
        }
    }
}
```


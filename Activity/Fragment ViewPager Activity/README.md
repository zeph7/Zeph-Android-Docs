# ViewPager with sliding Fragments :

![](https://blog.iamsuleiman.com/wp-content/uploads/2015/12/onboarding-android-viewpager-header-720x340.png)

## Create Framents :

First, you need to create fragments that will be sliding on the `ViewPager`

## Use ViewPager code in layout file :

```xml
<com.tbuonomo.viewpagerdotsindicator.DotsIndicator
            android:id="@+id/dotsIndicator"
            android:layout_width="wrap_content"
            android:layout_height="13dp"
            app:dotsColor="@color/colorDots"
            app:dotsCornerRadius="8dp"
            app:dotsSize="8dp"
            app:dotsSpacing="2dp"
            app:dotsWidthFactor="2.5"
            app:selectedDotColor="@color/colorDotsSelected"
            app:progressMode="true"
            android:layout_centerHorizontal="true"/>

<!--Default android ViewPager library-->
    <android.support.v4.view.ViewPager
            android:id="@+id/slideSignupViewPager"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="32dp"
            app:layout_constraintTop_toBottomOf="@+id/dotsIndicator"/>
```

## SlideViewPagerAdapter.kt :

```kotlin
class SlideViewPagerAdapter(fragmentManager: FragmentManager) : FragmentPagerAdapter(fragmentManager) {

    override fun getCount() = 3

    override fun getItem(position: Int): Fragment =
        when (position) {
            0 -> FragmentOne()
            1 -> FragmentSecond()
            2 -> FragmentThird()
            else -> FragmentOne()
        }
}
```

## MainActivity.kt :

```kotlin
class SignupInfoActivity : AppCompatActivity() {

    private lateinit var sliderAdapter: SlideViewPagerpAdapter
    private lateinit var slideViewPager: ViewPager
    private lateinit var dotsIndicator: DotsIndicator

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_signup_info)

        slideViewPager = findViewById(R.id.slideSignupViewPager)

        val fragmentPageAdapter = SlideViewPagerpAdapter(supportFragmentManager)
        slideViewPager.adapter = fragmentPageAdapter

        // to add the bottom indicator dots
        dotsIndicator = findViewById(R.id.dotsIndicator)
        dotsIndicator.setViewPager(slideViewPager)

        // if forward change viewpager fragment by a buttonClick
        nextButton.setOnClickListener {
            slideViewPager.currentItem = slideViewPager.currentItem + 1
        }
        
    // if backward change viewpager fragment by a backButton
    override fun onBackPressed() {
        if (slideViewPager.currentItem == 0) {
            super.onBackPressed()
        } else {
            slideViewPager.currentItem = slideViewPager.currentItem - 1
        }
    }
 }
 ```
 
 



# Onboarding Activity

![](https://cdn.dribbble.com/users/1145294/screenshots/3238301/3screens_2.png)

Example ^

## Create a new activity :

Create a new activity and add the default android ViewPager dependency which will be the sliding ViewPager, inside of which you can add any 
number of widgets. And add the [Material View Pager Dots Indicator](https://github.com/tommybuonomo/dotsindicator) library for showing the 
bottom dots with effects.
</br>

* ### activity_onboard.xml :

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:tools="http://schemas.android.com/tools"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:background="@color/colorBackground"
        tools:context=".OnboardActivity">

    <!--Default android ViewPager library-->
    <android.support.v4.view.ViewPager
            android:id="@+id/slideViewPager"
            android:layout_width="match_parent"
            android:layout_height="500dp">

    </android.support.v4.view.ViewPager>

    <!--Material View Pager Dots Indicator library-->
    <com.tbuonomo.viewpagerdotsindicator.DotsIndicator
            android:id="@+id/dotsIndicator"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            app:dotsColor="@color/colorDots"
            app:dotsCornerRadius="8dp"
            app:dotsSize="8dp"
            app:dotsSpacing="2dp"
            app:dotsWidthFactor="2.5"
            app:selectedDotColor="@color/colorButton"
            app:progressMode="true"
            android:layout_centerHorizontal="true"
            android:layout_marginTop="500dp"/>
            
    <Button
            android:id="@+id/buttonID"
            android:text="@string/button_text"
            android:visibility="gone"
            android:textColor="@color/colorBackground"
            android:textSize="16sp"
            android:layout_width="match_parent"
            android:layout_height="48dp"
            android:layout_alignParentBottom="true"
            android:layout_marginBottom="16dp"
            android:layout_centerHorizontal="true"
            android:layout_marginLeft="16dp"
            android:layout_marginRight="16dp"/>

</RelativeLayout>
```
</br>

* ### slide_onboard_layout :

Create a layout file for individual screen of sliding ViewPager. Here, I have added only 2 items ImageView and a TextView but, can add more.

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
                xmlns:app="http://schemas.android.com/apk/res-auto" android:layout_width="match_parent"
                android:background="@color/colorBackground"
                android:layout_height="match_parent">


    <ImageView
            android:id="@+id/slide_image"
            android:layout_width="280dp"
            android:layout_height="280dp"
            app:srcCompat="@drawable/onboard_img1"
            android:layout_marginTop="24dp"
            android:layout_centerHorizontal="true"/>

    <TextView
            android:id="@+id/slide_text"
            android:text="@string/onboard_text"
            android:layout_width="280dp"
            android:layout_height="44dp"
            android:lineHeight="22sp"
            android:textSize="16sp"
            android:textColor="#000000"
            android:gravity="center"
            android:lineSpacingExtra="3sp"
            android:layout_below="@+id/slide_image"
            android:layout_marginTop="64dp"
            android:layout_centerHorizontal="true"/>

</RelativeLayout>
```
</br>

* ### SlideAdapter.kt :

Create a slide adapter that contain the data to be shown on different widgets (ImageView, TextView) on different screens and also how to 
initialize and destroy the sliding screens.

```kotlin
class SliderAdapter(private var context: Context) : PagerAdapter() {

    private lateinit var layoutInflater: LayoutInflater


    // arrays containing the data to be shown on the onBoard
    private var slideImages = arrayOf(
        R.drawable.onboard_img1,
        R.drawable.onboard_img2,
        R.drawable.onboard_img3)

    private var slideTexts = arrayOf(
        "onboard_text1",
        "onboard_text2",
        "onboard_text3")



    // to get the item count of the onBoard screens
    override fun getCount(): Int {
        return slideTexts.size
    }

    override fun isViewFromObject(view: View, o: Any): Boolean {
        return view == o
    }



    // to initialize the items in the onBoard
    override fun instantiateItem(container: ViewGroup, position: Int): Any {

        layoutInflater = context.getSystemService(Context.LAYOUT_INFLATER_SERVICE) as LayoutInflater
        val view: View = layoutInflater.inflate(R.layout.slide_onboard_layout, null)

        val slideImageView: ImageView = view.findViewById(R.id.slide_image)
        val slideTextView: TextView = view.findViewById(R.id.slide_text)

        slideImageView.setImageResource(slideImages[position])
        slideTextView.text = slideTexts[position]

        container.addView(view)

        return view
    }

    // to remove/destroy the items in the onBoard
    override fun destroyItem(container: ViewGroup, position: Int, `object`: Any) {
        container.removeView(`object` as RelativeLayout)
    }

}
```
</br>

* ### OnboardActivity.kt :

```kotlin
class OnboardActivity : AppCompatActivity() {

    private lateinit var sliderAdapter: SliderAdapter
    private lateinit var slideViewPager: ViewPager
    private lateinit var dotsIndicator: DotsIndicator

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_onboard)

        slideViewPager = findViewById(R.id.slideViewPager)

        sliderAdapter = SliderAdapter(this)
        slideViewPager.adapter = sliderAdapter

        // to add the bottom indicator dots
        dotsIndicator = findViewById(R.id.dotsIndicator)
        dotsIndicator.setViewPager(slideViewPager)

        // to listen the page change of the onBoard
        slideViewPager.setOnPageChangeListener(object : ViewPager.OnPageChangeListener {
            override fun onPageScrolled(i: Int, v: Float, i2: Int) {
            }
            override fun onPageSelected(i: Int) {
                // here you will get the position of selected page
                if (i == 2) buttonID.visibility = View.VISIBLE
                else buttonID.visibility = View.GONE
            }
            override fun onPageScrollStateChanged(i: Int) {
            }
        })

        buttonID.setOnClickListener {
            startActivity(Intent(this, MainActivity::class.java))
        }
    }
}
```

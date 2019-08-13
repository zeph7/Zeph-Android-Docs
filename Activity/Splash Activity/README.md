# Splash Activity

* ## SplashActivity.kt :

Below defined is kotlin code for splash screen

```kotlin
class SplashActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        // removes the Title Bar and sets the layout parameter to Fullscreen
        window.requestFeature(Window.FEATURE_NO_TITLE)
        window.setFlags(WindowManager.LayoutParams.FLAG_FULLSCREEN,
            WindowManager.LayoutParams.FLAG_FULLSCREEN)

        setContentView(R.layout.activity_splash)

        // postDelayed function delays the task for, developer passed 1000 milliseconds
        Handler().postDelayed({
            startActivity(Intent(this@SplashActivity, MainActivity::class.java))
        }, 1000)
    }
}
```

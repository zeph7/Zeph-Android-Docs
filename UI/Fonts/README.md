# Fonts

## Using Custom Fonts

Here are the steps to do it:

    1. Go to the (project folder)
    2. Then app>src>main
    3. Create folder 'assets>fonts' into the main folder.
    4. Put your .ttf file(ex- oxygen.ttf) into the fonts folder.
    
![](https://i.stack.imgur.com/i6XNU.png)

Then in Kotlin file:

```kotlin
val customFontTypeface = Typeface.createFromAsset(assets, "fonts/oxygen.ttf")
textViewId.setTypeface(customFontTypeface)
```
### or

If you have Fonts in `font` folder under `res` folder

```kotlin
val customFontTypeface = ResourcesCompat.getFont(this, R.font.oxygen)
textViewId.setTypeface(customFontTypeface)
```

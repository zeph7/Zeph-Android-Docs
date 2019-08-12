# Buttons

## Round Edge Buttons :

```xml
<?xml version="1.0" encoding="utf-8"?>
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <item>
        <shape android:shape="rectangle">
            <solid android:color="@color/colorButton"/>
            <!--corners allow us to make the rounded corners button-->
            <corners android:radius="8dp" />
        </shape>
    </item>
</selector>
```
Save the above code as `round_edge_button.xml` in a `Drawable Resource File` format inside `Drawable` folder. 
Use this file as the background of the `Button` widget as :
```xml 
android:background="@drawable/round_edge_button"
```


## Remove shadows around button :

```xml
style="?android:attr/borderlessButtonStyle"
```

## Remove all text capital style :

```xml
android:textAllCaps="false"
```

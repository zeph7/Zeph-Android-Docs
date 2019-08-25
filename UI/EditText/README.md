# [EditText](https://developer.android.com/reference/android/widget/EditText)

## Make the cursor invisible :

```xml
android:cursorVisible="false"
```

## Set max char input limit to 10 :

```xml
android:maxLength="10"
```

## Set the width of editText to 10 char wide :

<b>Note - </b>
Remove `android:ems=10` from editText and set `android:layout_width="wrap_content"`

```xml
android:maxEms="10"
```

## Hide underBar of editText :

```xml
android:background="@null"
```

## EditText TextWatcher :

When an object of this type is attached to an Editable, its methods will be called when the text is changed

```kotlin
editText.addTextChangedListener(object : TextWatcher {
  override fun afterTextChanged(p0: Editable?) {
  }

  override fun beforeTextChanged(p0: CharSequence?, p1: Int, p2: Int, p3: Int) {
  }

  override fun onTextChanged(p0: CharSequence?, p1: Int, p2: Int, p3: Int) {
  }
})
```

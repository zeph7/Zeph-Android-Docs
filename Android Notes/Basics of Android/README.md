# Basics of Android

* **Activity** - An Activity is a `core Android class` which is responsible for drawing an app user interface and receiving input events. 

  Each activity has a associated layout file. `Layout files` are actually `XML files` that express what the app locks like. They do this by 
  defining things (called `Views`) like texts, images and buttons and where these things will appear on screen.

* **Layout Inflation** - Activity and layout are connected by a process known as Layout Inflation. 

  And this process is triggered when the 
  activity starts. The `Views` defined in the XML layout files are turned or `inflated into kotlin view objects` in memory. Once this is done 
  the activity can draw these objects to the screen and also dymnamically modify them.

* `Layout Inflation` process makes a bunch of kotlin view oblects in the memory from the XML description. The inflated view oblects are 
organised into a **View Hierarchy Tree** which is a tree of views that matches the structure in the XML file (Ex - LinearLayout is the root 
of the tree with children as a TextView, a Button or any other view). The Activity gets the reference of the entire View Hierarchy Tree. 
The unique ID assigned to the Views are used to search the View in that Tree. Android Studio will automatically generate an integer constant 
with that ID's name (Ex - id roll_button=0x7f070061). It does this in a generated class called R (R stands for Resource). And 
findViewById(R.id.roll_button) searches the View Hierarchy.


* **Important Optimization Note** - When Android system draws the View Hierarchy, it is traversed, sometimes multiple times to calculate 
where every view needs to go taking into account each view size, location and additional constraints. For some apps this View Hierarchy 
could get pretty complex, the deeper the Hierarchy is, the more work the Android system has to do to calculate layout. Well, the Android 
system optimizes this process having big deep View Hierarchy can eventually effect performance. To help with this Android offers  a layout 
that promotes a `flat View Hierarchy` and is optimized for laying out its views, its `Constraint Layout`.

* **Important Optimization Note** - When we write the declaration of a view inside the Activity class, if we do it as: 

		var xyzImage: ImageView? = null
    
	It will complicate the code because everytime we wanna use this View, we're gonna make null checks, so use `lateinit` keyword. It 
  promises the Kotlin compiler that the variable will be initialized before calling any operation in it.


* **ViewGroup** - View like LinearLayout is a special type of layout called the ViewGroup. ViewGroup are responsible for holding multiple 
views on screen	and helping to specify their position

* **sp** - size measurefor texts is sp, stands for [Scale Independent Pixels]
* **dp** - unit for expressing location and dimensions is dp. stands for [Density Independent Pixels] 

		on 160 dpi screen: 1 dp == 1 pixel
    
		on 480dpi screen: 1dp == 3 pixel

* Kotlin Code is responsible for defining the interactive parts of the app

* **Gradle** - Gradle is a build tool of choice of Android.

	It controls a number of different things:
  
* What devices run your app - which devices your app is made to run on
* Compile to execution - compiling code and resources to executable Code
* Dependency management - declaring and managing dependent code and libraries
* App signing for Google Play - app sigining so that users can download it from Google Play
* Automated tests - running Automated tests

* **Basics of Gradle**

  When you press Run button, a series of Gradle commands compile your source code through dependencies and any associated resources into 
  a Android Application Package (called APK). An APK is a file format used to distribute and install android applications after its build 
  by gradle. Android Studio then transfers the APK to your physical device or emulator, it installs the APK and runs it.

* **Dependencies** (in gradle) - are external code, such as libraries, that a project depends on

* Adding **Vectors** to the drawable folder:

	1. Enable the use of support library for vector drawables in build.gradle file (app level):
			`vectorDrawables.useSupportLibrary = true`
	2. Use app:srcCompat in the image tag in the layout file:
			`app:srcCompat="@drawable/empty_dice"`
	3. You’ll also need to add the namespace to the root of the layout:
			`xmlns:app="http://schemas.android.com/apk/res-auto"`

* **app:srcCompat** - is an attribute used when you want a vector drawable (vector images can be resized without losing image quality where 
  png files lose image quality). 
* **android:src** - would be the attribute for you if you were to go with a png drawable. You can use these attributes on ImageButtons and 
  ImageViews

* **Namespaces** - Namespaces are how you access all the Android attributes and tags that are defined by Google already. 

  When you give `xmlns:android="http://schemas.android.com/apk/res/android”` all the keys i.e attributes and tags that are attached to this 
  namespace will be imported( or at least sort of ). So next time when you give android: the autocomplete list occurs.

  There are many `namespaces` available. The most used are `app`, `tools` .

  Namespaces are almost like `import` statements in Java or Python.

 * **Data Binding** - Connecting views with data

    If we use findViewById to reference to a view, when we search for a view after it has been created or recreated, Android has to traverse the 
    View Hierarchy to find it for us at runtime. For large View Hierarchy, it can slow down the app for the user. 
    To fix this there is a techinque called `Data Binding`, that allow us to connect a layout to an activity or fragment at compile time.
    The compiler generated a helper class called a `binding class` when the activity is created, so is an instance of the binding class and then 
    we can access the views from the binding class without any extra overhead.


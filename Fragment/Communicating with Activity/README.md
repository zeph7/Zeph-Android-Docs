# Fragment communicating with Activity using Interfaces

* ## Firstly create an Interface Communicator.kt :

Create an Interface with functions to send data from fragment to activity or to another fragment

```kotlin
interface Communicator {

    fun sendData(data: String)
}
```

* ## Secondly use the Interface in the fragment FragmentX.kt :

Declare and initialize a Communicator interface reference variable

```kotlin
class FragmentX : Fragment() {

    private lateinit var comm: Communicator   // Communicator interface reference variable
    private var userData: String = ""
    
    override fun onCreateView(inflater: LayoutInflater, container: ViewGroup?,
        savedInstanceState: Bundle?): View? {
        // Inflate the layout for this fragment
        return inflater.inflate(R.layout.fragment_signup_name, container, false)
    }


    override fun onActivityCreated(savedInstanceState: Bundle?) {
        super.onActivityCreated(savedInstanceState)

        // initializing Communicator interface reference variable
        comm = activity as CommunicatorSignupDetails

        val data = edittextX.text.toString
        
        buttonX.setOnClickListener {
            comm.sendData(data)     // this will invoke the method in Interface 
        }
    }

}
```

* ## Thirdly use the Interface in the activity MainActivity.kt :

Implement the Communicator Interface in the MainActivity.kt and overrride its method sendData() and use the data received as per requirement

```kotlin
class MainActivity : AppCompatActivity(), Communicator {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_signup_info)
        
    }

    // function to retrieve data from FragmentX
    override fun sendData(data: String) {
        userData = data
        // Do use this data as per requirement
    }
}
```




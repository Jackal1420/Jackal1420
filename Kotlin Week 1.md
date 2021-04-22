
---------------------------------------------------------------------------------------
Kotlin Basics
---------------------------------------------------------------------------------------


⌨️ (0:06:33​) Working With Variables

⌨️ (0:11:04​) Type System

⌨️ (0:15:00​) Basic Control Flow
  - Scope ( Top-Level vs local within <Class, Function, etc>)
  - Val and Var
  - Nullability (?)
  - Conditionals and Control Flow (If/else, When)
  - Using conditionals to assign value
 
⌨️ (0:21:31​) Basic Kotlin Functions

⌨️ (0:27:12​) Function Parameters
  - Function format: 
    ```
    fun functionName( <param>:<paramType>, <param2>:<paramType2> ): ReturnValue{
      // Do Stuff //
      return value;
    }
    ```
  - A "Unit" type in kotlin is "the absence of any useful type," same as leaving return type out.
  - How would you get a function to return null? 
    ```
    fun functionName(): ReturnValue?{
      return null;
    }
    ```
  - How would you get a function to return a type by compiler inference?
    ```
    fun functionName( name: String ) = println("Hello $name")
    ```    


---------------------------------------------------------------------------------------
DATA TYPES, Iteration
---------------------------------------------------------------------------------------

⌨️ (0:32:52​) Arrays

⌨️ (0:35:28​) Iterating with forEach

  ```
  val myArray = arrayOf("Bob", "Tom") // arrayOf is called a convenience function. Performs type inference and builds your list.
  myArray.size
  myArray[ <element index> ]
  myArray.get( <element index> )

  for (myItem in myArray){
      println(myItem)
  }

  // OR Invoke a foreach lambda function //

  myArray.forEach { item ->
      println(item)
  }

  // Using an index with a lambda function //

  myArray.forEachIndexed { index, item ->
      println("myArray[$index] = $item")
  }

  ```

⌨️ (0:41:17​) Lists

  - "`Array<T>` is mutable (it can be changed through any reference to it), but `List<T>` doesn't have modifying methods (it is either read-only view of `MutableList<T>` or an immutable list implementation)."

⌨️ (0:42:47​) Maps

  - Associated key/value pairs for quick lookups

⌨️ (0:45:05​) Mutable vs Immutable Collections

  ```
  val map = mapOf(1 to "A", 2 to "B", 3 to "C") // access by map[1], map[2]

  map.forEach { key, value -> println("$key -> $value") }
  ```

⌨️ (0:49:24​) Vararg Parameters

⌨️ (0:54:21​) Named Arguments

⌨️ (0:56:26​) Default Parameter Values

---------------------------------------------------------------------------------------
Classes
---------------------------------------------------------------------------------------

⌨️ (1:00:27​) Create A Simple Class

⌨️ (1:03:35​) Adding Class Properties

⌨️ (1:05:15​) Class Init Block
  - Called FIRST
  - Called in order of how they appear in the file

⌨️ (1:06:40​) Accessing Class Properties

⌨️ (1:07:32​) Primary Constructor Properties

⌨️ (1:08:17​) Secondary Constructors

⌨️ (1:09:50​) Working With Multiple Init Blocks

⌨️ (1:11:30​) Default Property Values

⌨️ (1:11:59​) Properties With Custom Getters/Setters

⌨️ (1:16:52​) Class Methods

  - https://kotlinlang.org/docs/classes.html

⌨️ (1:20:12​) Visibility Modifiers - Public/Private/Protected
  - Public = Everyone
  - Private = Only Class or File
  - Protected = Only Class or File and Inheritor 
  - Internal = Within the module 


---------------------------------------------------------------------------------------
Other Class Things
---------------------------------------------------------------------------------------

⌨️ (1:22:30​) Interfaces

⌨️ (1:26:13​) Implementing An Interface

⌨️ (1:26:35​) Overriding Methods

⌨️ (1:29:30​) Interface Properties

⌨️ (1:31:40​) Implementing Multiple Interfaces

⌨️ (1:28:30​) Default Interface Methods
  - Interfaces are used to standardize and communicate behavior
  - https://kotlinlang.org/docs/interfaces.html
  
⌨️ (1:24:21​) Abstract Classes
  - Abstract classes let you define some behaviors; they force your subclasses to provide others
  - https://kotlinlang.org/docs/classes.html#abstract-classes
  
⌨️ (1:32:57​) Type Checking And Smart Casts
  - `is` and `as`
  ```
  fun checkTypes(infoProvider: PersonInfoProvider){
    if (infoProvider is SessionInfoProvider){
        println("Is a session info provider: id = ${(infoProvider as SessionInfoProvider).getSessionId()}")
    } else {
        println("Is not a session info provider")
    }
  }
  ```

⌨️ (1:36:18​) Inheritance
  - Adopting behavior from a class and making your own more specialized 
  - https://kotlinlang.org/docs/inheritance.html

---------------------------------------------------------------------------------------
Data Objects, Less common classes
---------------------------------------------------------------------------------------

⌨️ (1:43:07​) Object Expressions
  - limited scope special override of a class
  ```
  val provider = object : PersonInfoProvider {
    override val provdierInfo: String
      get() = "override string"
  }
  ```

⌨️ (1:45:06​) Companion Objects
  - Useful for storing state and methods common to all instances of a class
  ```
  class Entity private constructor (val id: String) { 
    companion object Factory {
      fun create() = Entity (id: "id")
    }
  }
  Entity.Factory.create()
  ```

⌨️ (1:49:51​) Object Declarations
  - Easy way to create thread safe singletons in kotlin
    - Thread safe = resources can't be accessed by two separate threads at the same time
    - Singleton = One instance per the entire module
  ```
  object EntityFactory{
    fun create() = Entity(id: "id", name: "name")
  }
  class Entity(val id: String, val name: String){
    override fun toString(): String{
      return "id:$id name:$name"
    }
  }
  ```

⌨️ (1:52:41​) Enum Classes
  - Differentiating between different types of entities 

⌨️ (1:58:16​) Sealed Classes
⌨️ (2:00:07​) Data Classes
  - Sealed classes define a set number of classes extending a base type 
  - Only those classes can extend the base type 
  ```
  seald class Entity(){
    object Help{
      val name = "Help"
    }
    data class Easy (val id: String, val name: String): Entity()
    data class Medium (val id: String, val name: String): Entity()
    data class Hard (val id: String, val name: String, val multiplier: Float): Entity()
  }
  ```
---------------------------------------------------------------------------------------
Advanced Topics
---------------------------------------------------------------------------------------

⌨️ (2:12:25​) Extension Functions/Properties
  - Modify the way in which classes are used outside of the class 
  ```
  fun Class.NewMethod() {
    println("Class ${property.value}")
  }
  ```

⌨️ (2:16:40​) Higher-Order Functions
  - Return another function or take functions as parameter values 
  - Useful when our class needs to know how to process data etc... 
  - e.g. `myClass.Process( data, function that performs specialized operation on data )`
  - Lambdas are functions passed as arguments, directly constructed in argument call  
  
⌨️ (2:29:07​) Using The Kotlin Standard Library
  - https://kotlinlang.org/docs/collections-overview.html

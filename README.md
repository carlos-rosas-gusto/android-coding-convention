# Android Coding Convention with ![](./gusto_logo.png)


This document contains a series of recomendations and guidelines that must be take in consideration when writting code or implementing an amazing new feature for the Gusto Android app.

This is a living document and can be updated and/corrected in any time with suggestions, don't hesitate in get in touch if you think something could be improved. Most of the conventions here are taken directly form the official [Kotlin lang](https://kotlinlang.org/docs/reference/coding-conventions.html) webpage.


## Source code file naming

The name of the source files must be camel case with uppercase first letter with the `kt` extension. 

```Kotlin
Vehicle.kt
```

```Kotlin
package com.gusto.android

interface Vehicle {
	fun accelerate(): Unit
}

class Car : Vehicle() {
	override fun accelerate() { /** Do some magic **/ }
}

class Bicycle : Vehicle() {
	override fun accelerate() { /** Do other magic **/ }
}
```

If the file has more than one class, the file must be called like the most significant class in the file.

In the case the file isn't a class, but a collection of extensions, the file must be have a meaningful name related to the context of the extensions following the convetion of the Classes naming with the postfix `Ext`.

```Kotlin
GustoViewsExt.kt
```

When it comes to name a package, remember the package name must be in lower case.

## Resource files naming

When creating a new resource file within the project, you also need to be sure to follow the naming convention, the following is a table describing the names for resource files.

| Component  | Prefix | Class Name | Layout Name |
|------------|--------|------------|-------------|
| Activity | activity_ | `HomeActivity` | `activity_home.xml` |
| Fragment | fragment_ | `SavingsDetailFragment` | `fragment_savings_detail.xml` |
| Dialog | dialog_ | `ConfirmExitDialog` | `dialog_confirm_exit.xml` |
| AdapterView item | item_ | `AccountItem` | `item_account.xml` |
| Partial Layout | content_ | --- | `content_user_contact_info.xml` |

## Class layout

The code inside the Kotlin files must folllow the layout following layout :

  - Companion object
  - Enumeration classes
  - Private properties
  - Public Properties
  - Constructors
  - Initializer block
  - Private methods
  - Public methods

Remember that properties and methods names must start with a lower case letter and use camel case and no underscores.

```Kotlin
package com.gusto.android

class Account {
	
	companion object {
	  const val TYPE_EMPLOYER = 0 // Account type for the Employer
		const val TYPE_EMPLOYEE = 1 // Account type for the Employee
	}
	
	private id: String
	public Type: Int
	
	constructor(id: String, type: Int) { /** Do stuff */ }
	constructor(id: String, isEmployee: Boolean = false) { /** More stuff */ }
	
	init { /** Remember init is being called by all the constructors */ }
	
	private fun setId() { /* Do magic with the Id */ }

	public fun printAccount() { /** Format the Account info */ }	
}
```

## Methods, properties and constants naming rules

Names of methods and properties must start with a lower case letter and use the camel case and no underscores.

```Kotlin
val requestResult: Result? // Good
val _res: Result? = null // Bad

fun onRequestResultCallback(result: Result) {} // Bad
fun resultreceived(res: Result) {} // Bad
```

Never use magic numbers or values, if you need to specify a constant within the code, you must create a constant property in the companion object of the class or the class, the constant property must be all uppercase with words separated by underscores. If needed, you can document this constants with a single line comment.

```Kotlin
package com.gusto.android

const val ASYNC_OPERATION_TIME_OUT_ = 10000 // Time out value when requesting an Async operation, in millis

/** Custom Button with fancy Gusto style */
class GustoClickableButton : Button {
	
	companion object {
		const val RECT_BUTTON = 0 // Rectangular button
		const val ROUND_BUTTON = 1 // Round button
	}
	
	private const val MIN_WITDH = 120 // Minimun size for the button
}
```

## Documenting your code

Documenting your code is highly encouraged, though you don't have to document every property and method, you must document the class and the most relevant or ambiguous properties and methods. 

This will help anybody else to understand the way in which the code was created, it's more likely to be reused and will ensure you or any other developer won't take as much time to understand it.

```Kotlin
package com.gusto.android

/** Interface used to represent Mathematical operations */
interface MathOperation<T> {
  
  /** Abstract method in charge of perform the Matemathical operation */
	fun performOperation(args: List<T>): T throws Exception
}

/** Class for the Mutiplication matemathical operation */
class Multiplication : MathOperation<Double>() {

/**
 * Returns the multiplication all elements in the list.
 * @param args List containing the [Double] values to be multiplied.
 */
	override fun performOperation(args: List<Double>): Double {
    if (!isListValid(args)) { throws IllegalArgumentException("Argument list is invalid or contains INFINITY.")}
    return 0.toDouble().apply { args.forEach { this * it }}
  } 
	
	/** 
	 * Returns the multiplication all elements in the list. Notice this 
	 * method might return a [NumberFormatException] if a non-numeric value 
	 * is found.
	 * @param args List containing the values to be multiplied
	*/
	fun performOperation(args: List<String>) = this.performOperation(args.map { it.toDouble() })
	
	private fun isListValid(args: List<Double>) = 
  	if (args.isEmpty()) { false }
  	else {
      args.none { 
        it == Double.NEGATIVE_INFINITY || it == Double.POSITIVE_INFINITY 
      }
		}
}
```

To be continued ...

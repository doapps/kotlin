# DOAPPS Kotlin Style Guide

# Table of Contents

- [Nomenclature](#nomenclature)
  + [Packages](#packages)
  + [Classes & Interfaces](#classes--interfaces)
  + [Methods](#methods)
  + [Fields](#fields)
  + [Variables & Parameters](#variables--parameters)
  + [Misc](#misc)
- [Declarations](#declarations)
  + [Visibility Modifiers](#visibility-modifiers)
  + [Fields & Variables](#fields--variables)
  + [Classes](#classes)
  + [Data Type Objects](#data-type-objects)
  + [Enum Classes](#enum-classes)
  + [LiveData](#LiveData)
- [Spacing](#spacing)
  + [Indentation](#indentation)
  + [Line Length](#line-length)
  + [Vertical Spacing](#vertical-spacing)
- [Semicolons](#semicolons)
- [Getters & Setters](#getters--setters)
- [Brace Style](#brace-style)
- [When Statements](#when-statements)
- [Types](#types)
  + [Type Inference](#type-inference)
  + [Constants vs. Variables](#constants-vs-variables)
  + [Companion Objects](#companion-objects)
  + [Optionals](#optionals)
- [Language](#language)

## Nomenclature

On the whole, naming should follow Java standards, as Kotlin is a JVM-compatible language.

### Packages

Package names are similar to Java: all __lower-case__, multiple words concatenated together, without hypens or underscores:

__BAD__:

```kotlin
com.RayWenderlich.funky_widget
```

__GOOD__:

```kotlin
com.raywenderlich.funkywidget
```

### Classes & Interfaces

Written in __UpperCamelCase__. For example `RadialSlider`. 

### Methods

Written in __lowerCamelCase__. For example `setValue`.

### Fields

Generally, written in __lowerCamelCase__. Fields should **not** be named with Hungarian notation, as Hungarian notation is [erroneously thought](http://jakewharton.com/just-say-no-to-hungarian-notation/) to be recommended by Google.

Example field names:

```kotlin
class MyClass {
  var publicField: Int = 0
  val person = Person()
  private var privateField: Int?
}
```

Constant values in the companion object should be written in __uppercase__, with an underscore separating words:

```kotlin
companion object {
  const val THE_ANSWER = 42
}
```

### Variables & Parameters

Written in __lowerCamelCase__.

Single character values must be avoided, except for temporary looping variables.

### Misc

In code, acronyms should be treated as words. For example:

__BAD:__

```kotlin
XMLHTTPRequest
URL: String? 
findPostByID
```
__GOOD:__

```kotlin
XmlHttpRequest
url: String
findPostById
```

## Declarations

### Visibility Modifiers

Only include visibility modifiers if you need something other than the default of public.

**BAD:**

```kotlin
public val wideOpenProperty = 1
private val myOwnPrivateProperty = "private"
```

**GOOD:**

```kotlin
val wideOpenProperty = 1
private val myOwnPrivateProperty = "private"
```

### Access Level Modifiers

Access level modifiers should be explicitly defined for classes, methods and member variables.

### Fields & Variables

Prefer single declaration per line.

__GOOD:__

```kotlin
username: String
twitterHandle: String
```

### Classes

Exactly one class per source file, although inner classes are encouraged where scoping appropriate.

If we want to use the arguments passed through the constructor, we can do it by defining the properties, these properties can be mutable or immutable and they help us to define in a simple way the famous Java getters and setters fields, but with a big difference, the simplicity.

* Properties without modifying its get and set method

__BAD:__

```kt
class Person(name: String, age: Int) {
    val name: String
    val age: Int

    init {
        this.name = name
        this.age = age
    }
}
```
__BAD:__

```kt
class Person(name: String, age: Int) {
    val name: String = name
    val age: Int = age
}
```

__GOOD:__

```kt
class Person(val name: String, val age: Int)

```

* Properties modifying its get and set method.

You don't need to move all the arguments to the body of the class, only the one that will be modified.

__BAD:__

```kt
class Person(name: String, age: Int) {
    val age = age
    var name = name
        get() = "Su nombre es: $field"
        set(value) { field = "Nuevo $value" }
}
```

__GOOD:__
```kt
class Person(name: String, val age: Int) {
    var name = name
        get() = "Su nombre es: $field"
        set(value) { field = "Nuevo $value" }
}

```

### Data Type Objects

Prefer data classes for simple data holding objects.

__BAD:__

```kotlin
class Person(val name: String) {
  override fun toString() : String {
    return "Person(name=$name)"
  }
}
```

__GOOD:__

```kotlin
data class Person(val name: String)
```

### Enum Classes

Enum classes without methods may be formatted without line-breaks, as follows:

```kotlin
private enum class CompassDirection { EAST, NORTH, WEST, SOUTH }
```

### LiveData

Declare a LiveData as public and associate it with a private MutableLiveData, it is true that you can work it defining and observing only a MutableLiveData, but this is not a good practice, since the logic and values ​​that are bound to that MutableLiveData could be modified by other classes from outside. Remember that LiveData are read only and are perfect to be observed by other classes.

__BAD:__

```kotlin
val progressVisible: MutableLiveData<Boolean> by lazy {
    MutableLiveData<Boolean>()
}
```

__GOOD:__

```kotlin
private val _progressVisible = MutableLiveData<Boolean>()
val progressVisible: LiveData<Boolean> get() = _progressVisible
```

## Spacing

Spacing is especially important in raywenderlich.com code, as code needs to be easily readable as part of the tutorial. 

### Indentation

Indentation is using spaces - never tabs.

#### Blocks

Indentation for blocks uses 2 spaces (not the default 4):

__BAD:__

```kotlin
for (i in 0..9) {
    Log.i(TAG, "index=" + i)
}
```

__GOOD:__

```kotlin
for (i in 0..9) {
  Log.i(TAG, "index=" + i)
}
```

#### Line Wraps

Indentation for line wraps should use 4 spaces (not the default 8):

__BAD:__

```kotlin
val widget: CoolUiWidget =
        someIncrediblyLongExpression(that, reallyWouldNotFit, on, aSingle, line)
```

__GOOD:__

```kotlin
val widget: CoolUiWidget =
    someIncrediblyLongExpression(that, reallyWouldNotFit, on, aSingle, line)
```

### Line Length

Lines should be no longer than 100 characters long.


### Vertical Spacing

There should be exactly one blank line between methods to aid in visual clarity and organization. Whitespace within methods should separate functionality, but having too many sections in a method often means you should refactor into several methods.

## Comments

When they are needed, use comments to explain **why** a particular piece of code does something. Comments must be kept up-to-date or deleted.

Avoid block comments inline with code, as the code should be as self-documenting as possible. *Exception: This does not apply to those comments used to generate documentation.*


## Semicolons

Semicolons ~~are dead to us~~ should be avoided wherever possible in Kotlin. 

__BAD__:

```kotlin
val horseGiftedByTrojans = true;
if (horseGiftedByTrojans) {
  bringHorseIntoWalledCity();
}
```

__GOOD__:

```kotlin
val horseGiftedByTrojans = true
if (horseGiftedByTrojans) {
  bringHorseIntoWalledCity()
}
```

## Getters & Setters

Unlike Java, direct access to fields in Kotlin is preferred. 

If custom getters and setters are required, they should be declared [following Kotlin conventions](https://kotlinlang.org/docs/reference/properties.html) rather than as separate methods.

## Brace Style

Only trailing closing-braces are awarded their own line. All others appear the same line as preceding code:

__BAD:__

```kotlin
class MyClass
{
  fun doSomething()
  {
    if (someTest)
    {
      // ...
    }
    else
    {
      // ...
    }
  }
}
```

__GOOD:__

```kotlin
class MyClass {
  fun doSomething() {
    if (someTest) {
      // ...
    } else {
      // ...
    }
  }
}
```

Conditional statements are always required to be enclosed with braces, irrespective of the number of lines required.

__BAD:__

```kotlin
if (someTest)
  doSomething()
if (someTest) doSomethingElse()
```

__GOOD:__

```kotlin
if (someTest) {
  doSomething()
}
if (someTest) { doSomethingElse() }
```

## When Statements

Unlike `switch` statements in Java, `when` statements do not fall through. Separate cases using commas if they should be handled the same way. Always include the else case.

__BAD:__

```kotlin
when (anInput) {
  1 -> doSomethingForCaseOneOrTwo()
  2 -> doSomethingForCaseOneOrTwo()
  3 -> doSomethingForCaseThree()
}
```

__GOOD:__

```kotlin
when (anInput) {
  1, 2 -> doSomethingForCaseOneOrTwo()
  3 -> doSomethingForCaseThree()
  else -> println("No case satisfied")
}
```


## Types 

Always use Kotlin's native types when available. Kotlin is JVM-compatible so **[TODO: more info]**

### Type Inference

Type inference should be preferred where possible to explicitly declared types. 

__BAD:__

```kotlin
val something: MyType = MyType()
val meaningOfLife: Int = 42
```

__GOOD:__

```kotlin
val something = MyType()
val meaningOfLife = 42
```

### Constants vs. Variables 

Constants are defined using the `val` keyword, and variables with the `var` keyword. Always use `val` instead of `var` if the value of the variable will not change.

*Tip*: A good technique is to define everything using `val` and only change it to `var` if the compiler complains!

### Companion Objects

** TODO: A bunch of stuff about companion objects **

### Nullable Types

Declare variables and function return types as nullable with `?` where a `null` value is acceptable.

Use implicitly unwrapped types declared with `!!` only for instance variables that you know will be initialized before use, such as subviews that will be set up in `onCreate` for an Activity or `onCreateView` for a Fragment.

When naming nullable variables and parameters, avoid naming them like `nullableString` or `maybeView` since their nullability is already in the type declaration.

When accessing a nullable value, use the safe call operator if the value is only accessed once or if there are many nullables in the chain:

```kotlin
editText?.setText("foo")
```


## Language

Use `en-US` English spelling. 🇺🇸

__BAD:__

```kotlin
val colourName = "red"
```

__GOOD:__

```kotlin
val colorName = "red"
```

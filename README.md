# Code Style

A guide to my Java/PHP/Obj-C style and conventions.

This is an attempt to encourage patterns that accomplish the following goals (in
rough priority order):

 1. Increased rigor, and decreased likelihood of programmer error
 2. Increased readability
 3. Increased clarity of intent
 4. Reduced verbosity

----

#### Indent style

 * Use IDE default configuration, instead of your preferences, to be able to setup the source code in any other environment.
 * If there are multiple IDEs (developing for PHP, using Eclipse, Netbeans, PHPStorm...), use tabs, not spaces. Configure tab size as you wish, so other developers could choose their own tab size without modifying source code.

#### Whitespace

 * End files with a newline.
 * Make liberal use of vertical whitespace to divide code into logical chunks.
 * Don’t leave trailing whitespace.

#### Variable names

 * Choose a good name, one that accurately describes the use of the variable.
 * The bigger the variable scope is, the larger the name should be.
 * Use language conventions. If not, choose camelCase naming convention.

#### Constants

 * Use language conventions: Upper case in Java, k prefix in Obj-C...
 * (Java, PHP...) Underscore naming convention.
 * Name should be composed by every context it belongs to, from bigger to smaller. Ex:
```java
public static final PREFERENCES_USER_NAME = "PREFERENCES_USER_NAME";
```

#### Methods

 * Choose where do you like to put open bracket (same line method definition or next line). Use the same standart to every method!
 * If you like open bracket same line, keep a white space between parameters and bracket.

#### Spaces

 * Use spaces like natural writing: respect spaces between words and operators. Ex:
```php
// Use this
$oneAwesomeArray = array('foo' => 'bar');
$var = $arg1 . 'static string' . $arg2;
// Instead of this
$oneAwesomeArray=array('foo'=>'bar');
$var=$arg1.'static string'.$arg2;
```
 * Use them also between method parameters. Ex:
```php
// Use this
public function analyzeAnArray($theArray, $someFlag, $anotherFlag = true) {
    // The code
}
// Instead of this
public function analyzeAnArray($theArray,$someFlag,$anotherFlag=true){
    // The code
}
```

#### Comments

 * Use first capital letter when starting a comment.
 * Keep one whitespace between line comment syntax and the first word. Ex:
```java
// The explanation
```
 * Use them to describe the reason why you write the code, not what you are doing (any programmer could understand what are you doing but not why you did or choose that solution).
 * Write comments over the block of code you want to explain, not in the same line.
For example, use this:
```java
// If user is allowed to edit resources and the resource is not blocked
if (user.couldEditResources() && !resource.isBlocked()) {
    // The code
}
```
Instead of this.
```java
if (user.couldEditResources() && !resource.isBlocked()) { // If user is allowed to edit resources and the resource is not blocked
    // The code
}
```
 * Remember adding javadoc for complex or critical methods. I recommend writing final dots as natural language. Keep one line separation between method explanation and parameter descriptions. Use html format to highlight important quotes. Add website and local links if needed. Ex:
```java
/**
 * The method explanation. <strong>Important note</strong>. Referenced here:
 * http://www.alink.com
 *
 * @param int param1 The param1 description.
 * @param int param2 The param2 description.
 * @return int The result description.
 */
public int myCriticalMethod(int param1, int param2) {
    return param1 + param2;
}
```

### Return and break early

When you have to meet certain criteria to continue execution, try to exit early. So, instead of this:

```java
if (!myArray.isEmpty()) {
    // Code
} else {
    return
}
```

use this:
```java
if (myArray.isEmpty()) {
    return
}
// Code
```

It is very important when writing a method with several validation block of codes. Real code execution and result should be at the end of the method. Ex:

```java
public int calculateAValue(Integer arg1, Integer arg2) {
    // First validation
    if (arg1 == null || arg2 == null) {
        // Stop execution here
        throw new Exception("The error message");
    }
    
    // Continue next validation
    if (arg1 < 1) {
        // Stop execution here
        throw new Exception("The error message");
    }
    
    // Real code
    return arg1 + arg2;
}
```

Use only one return inside a method, even using switchs and ifs. Ex:

```java
public int calculateSomething(int arg1, int arg2) {
    // Initialize return variable with default value
    int result = 0;
    // Perform operations
    switch (arg1) {
        case ARGS_KEY1:
            // Calculate the value, but don't return the value
            result = arg2 * ARGS_VALUE1;
        break;
        case ARGS_KEY2:
            // Calculate the value, but don't return the value
            result = arg2 - ARGS_VALUE2;
        break;
    }
    // Only one return, at the final of the method
    return result;
}
```

#### Class variables and method order

 1. Public constants should be at the beginning of the class
 2. Protected constants
 3. Private constants
 4. Protected attributes
 5. Public attributes
 6. Private attributes
 7. Static instance constructors
 8. Constructors
 9. Overriden methods
 10. Public methods
 11. Protected methods
 12. Private methods


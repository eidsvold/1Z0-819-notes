# Java SE 11 Developer 1Z0-819

- [Java SE 11 Programmer I 1Z0-815](#Java-SE-11-Programmer-I-1Z0-815)
- [Java SE 11 Programmer II 1Z0-816](#Java-SE-11-Programmer-II-1Z0-816)

## Java SE 11 Programmer I 1Z0-815

[_Tim Buchalka's video course at Udemy_](https://www.udemy.com/course/java-se-11-developer-1z0-819-ocp-course-part-1/ "Java SE 11 Developer 1Z0-819 OCP Course - Part 1 at Udemy")

1. [Creating a Simple Java Program](#1-Creating-a-Simple-Java-Program)
2. [Understanding Java Technology and Environment](#2-Understanding-Java-Technology-and-Environment)
3. [Working With Primitive Data Types and String APIs](#3-Working-With-Primitive-Data-Types-and-String-APIs)
4. [Using Operators and Decision Constructs](#4-Using-Operators-and-Decision-Constructs)
5. [Working with Java Arrays](#5-Working-with-Java-Arrays)
6. [Describing and Using Objects and Classes](#6-Describing-and-Using-Objects-and-Classes)
7. [Creating and Using Methods](#7-Creating-and-Using-Methods)
8. [Applying Encapsulation](#8-Applying-Encapsulation)
9. [Reusing Implementations Through Inheritance](#9-Reusing-Implementations-Through-Inheritance)
10. [Programming Abstractly Through Interfaces](#10-Programming-Abstractly-Through-Interfaces)
11. [Handling Exceptions](#11-Handling-Exceptions)
12. [Understanding Modules](#12-Understanding-Modules)

### 1. Creating a Simple Java Program

* If existent, the _package_ import MUST be the **first** statement in a source file, before any other statement.
* The _-d_ option of the _javac_ command sets the destination directory for class files. If a class is part of a package, then _javac_ puts the class file in a subdirectory that reflects the package name and creates directories as needed.
* When launching a program with the java command, the _classpath_ option ```-classpath``` indicates a semicolon ```;``` separated list of directories, JAR archives, and ZIP archives to search for class files. E.g. executing a program with class files stored in two directories: ```java -classpath dir1;dir2 MainClass```.
* The **classpath** option has three forms: ```-cp```, ```-classpath``` (!! only one dash) and ```--class-path```.
* The _java.lang_ package is imported into all types by default, hence importing this package is redundant and can be removed without affecting the program.
* Types are only loaded when they are **first referenced** in the code. This means an _import_ statement with the asterisk ```*``` character doesn't load all types in a package.
* To use a static member of a type directly in another type, we must use a **static import statement**. We can either import that particular static member: ```import static foo.MyFoo.myField``` or import all static members of the enclosing type: ```import static foo.MyFoo.*```.
* The entry method of a program **must be** a _public static_ method. Its name **must be** _main_, the parameter type **must be** _String[]_ or _String..._, and the return type **must be** _void_. **!!**: The parameter name as well as the order of the modifiers **are not** important.

### 2. Understanding Java Technology and Environment
* The Java Development Kit (JDK) is the only software required to set up a development environment.
* The Java Runtime Environment (JRE) is used to run a compiled program instead of working with source files.
* Integrated Development Environment (IDE) and Version Control System (VCS) are very important to developing applications, but they **are not** included in the JDK.
* A **type** defined with no package declaration is part of an unnamed package. Such a type can be referenced from other types in the unnamed package, but is invisible to types in named packages.

### 3. Working With Primitive Data Types and String APIs

* A _String_ object is immutable - in cannot be changed after being created. The _concat_ method appends the string argument to the end of the current string and returns the concatenation - hence the varible must be reassigned or assigned to another variable.
* The _StringBuilder_ method _delete_ removes characters from **index inclusive to index exclusive**, e.g. ```StringBuilder builder = new StringBuilder("ABCDE").delete(1, 2);``` removes only the ```"B"``` from the builder object.
* Remember when dividing with integers, the decimal point is always removed (number is floored). E.g. if you divide ```-2 by 4``` on a calculator, you get ```-0.5```. When working with integers in Java, this results in ```0```.
* The _String_ _lastIndexOf_ method searches backwards for the substring provided, returning the index of the first character in the substring. When providing a second argument, the search will start, backwards, at the index provided.
* The _String_ _split_ method splits a string around matches of a given regular expression. The limit argument (a second argument) controls the number of times the pattern is applied and therefore affects the length of the resulting array. If the _limit_ is positive then the pattern will be applied at most _limit_ - 1 times, the array's length will be no greater than _limit_, and the array's last entry will contain all input beyond the last matched delimeter.
* A local variable is different to a class-level field in that it's **not** automatically set to the default value of its type. Checking a local variable that hasn't been set results in a compile-time error.
* The _String_ passed to the _LocalDateTime_ _parse_ method must represent a valid date-time and is parsed using a _DateTimeFormatter_ type. If the formatter type includes time, a time component must be present. Also, with all ISO formatters, the number representing the month of the year or date of month always has two digits. A malformed string leads to a _DateTimeParseException_ at runtime.
* _var_ can **not** be used for fields, constructors and method parameters, as well as method return types.
* A local variable is visible only within the method or block where it's declared.
* When the _intern_ method is invoked, if the pool already contains a string equal to this _String_ object as determined by the _equals(Object)_ method, then the string from the pool is returned. Otherwise, this _String_ object is added to the pool and a reference to this _String_ object is returned.
* The _replace_ method with 2 _char_ parameters simply returns the same _String_ object it's called on, if those two parameters are the same. The _replace_ method with two _CharSequence_ parameters and the _replaceAll_ method always return a new object.
* We can use the underscore character to separate groups of digits in numeric literals, which can improve the readability of the code. However, such a character cannot be used at:
  * The beginning or end of a number
  * Adjacent to a decimal point in a floating-point literal
  * Prior to a suffix
* The _String substring_ method with 1 integer parameter returns a new string which begins with the character at the specified index and extends to the end of the string.
* The _isEmpty_ method returns _true_ if and **only if** its length is 0.
* The _isBlank_ method returns true if the string is empty or contains only white space codepoints, otherwise _false_.
* The _trim_ and _strip_ methods in the _String_ class both remove leading and trailing spaces, but they use different definitions of white spaces;
  * **trim**: all characters whose codepoint is less than or equal to 'U+0020'
  * **strip**: all characters whose codepoint returns true when passed to the _Character isWhitespace_ method. We can say _strip_ is "Unicode-aware" evolution of _trim_. The **strip** method was recently added to the API, starting with Java 11.
* Classes ub the _java.time_ package, including _LocalTime_, are immutable. Any changes made to an instance will create a new object instead of modifying the existing one.
* _**var**_ can only be used if the type of the declared varibale can be inferred from its initial value. _**var**_ cheat sheet:
  * compound declaration is not allowed
  * _var_ must go with a variable initializer
  * cannot be initialized to null
* Object member access has the highest precedence in Java. This operation is performed before casting. _CharSequence_ does not have a method called _toUpperCase_, meaning you cannot convert to uppercase as you are casting from _CharSequence_ to _String_ like this: ```String string = String) charSequence.toUpperCase();```.

### 4. Using Operators and Decision Constructs

* A _**switch** statement_ can only work with the following primitive data types: _byte_, _short_, _char_, and _int_. It also works with _enumerated types_, the _String_ class, and a few special classes that wrap certain primitive types: _Character_, _Byte_, _Short_ and _Integer_.
* A mismatch between switch expression and the label expressions makes the code unable to compile.
* The _default_ label in a **switch** statement only matches an argument if all the other labels don't, **regardless of its position**. If a case block is returning a value, the switch statement exits when a case matches the argument.
* The _break_ statement in a loop exits the construct right away, and the _continue_ statement skips to the next iteration of the construct.
* A _do_ _statement_ can complete normally **if and only if at least one** of the following is true:
  * The contained statement can complete normally and the condition expression **is not a constant** expression with value true.
  * The _do_ statement contains a reachable continue statement with no label, and the _do_ statement is the innermost _while_, _do_, or _for_ statement that contains that continue statement, and the continue statement continues that _do_ statement, and the condition expression **is not a constant** expression with value true.
  * The _do_ statement contains a reachable continue statement with a label _L_, and the _do_ statement has label _L_, and the continue statement continues that _do_ statement, and the condition expression **is not a constant** expression with value true.
  * There is a reachable break statement that exits the _do_ statement.

```Java
// Given:
List list = List.of("a", "b");
for (String element : list) {
    switch(element) {
        case "b":
        default:
            continue;
    }
    System.out.println(element);
}
```
The _continue_ statement is **not applicable** in a _switch construct_. In the given code snippet, the _continue_ statement doesn't skip a switch label, but rather the current iteration of the _foreach_ loop. Each time a switch label is matched, the _continue_ statement gets executed, skipping the rest of the foreach construct. This makes the ```System.out.println(element);``` statement unreachable, thereby causing a compile-time error.
* Any code after a return statement in the same scope is unreachable and will lead to a compile-time error.
* Unlike all other operators in Java, assignment operators are evaluated **from right to left**.
* A _for_ loop with all expressions empty (initialization; termination; increment) ```for( ; ; )``` may look weird, but is entirely valid. Instead of relying on such expressions, we must control the _for_ loop using statements in its body.
* A basic _for_ loop can complete normally if and **only** if at least one of the following is true:
  * The _for_ statement is reachable, there is a condition expression, and the condition expression is not a constant expression with value true.
  * There is a reachable break statement that exits the for statement
  The contained statement is reachable if and only if the for statement is reachable and the condition expression is not a constant expression whose value is false.
*

### 5. Working with Java Arrays

* The _Arrays.compare_ method returns the value ```0``` if the first and second array are equal and contain the same elements in the same order; a value **less than** ```0``` if the first array is _lexicographically_ less than the second array; and a value **greater than** ```0``` if the first array is _lexicographically_ greater than the second array. The method compares two and two elements at an index within the respective arrays.
Given:
```Java
int[] array1 = {1, 2, 3};
int[] array2 = {1, 3};

int result = Arrays.compare(array1, array2); // result = -1
```
The method returns ```-1``` because while the first element of the two is equal, the second element of array1 is **less than** the second element of array2. Therefore, the comparison stops and result in a negative number.
If all elements in a shorter array are equal to the other array, but the other array is longer with more elements, the result is the **difference in length** (positive or negative, depending on which array passed as first argument).
* The _Arrays_ _fill_ method assigns the specified Object reference to each element of the specified array of Objects.
* The _Arrays mismatch_ method finds and returns the index of the first mismatch between the two array arguments, otherwise return ```-1``` if no mistmatch is found.
* The _Arrays asList_ method returns a fixed-size list backed by the specified array. **Changes to the returned list "write through" to the array.** This method acts as a bridge between array-based and collection-based APIs. Changes made to the specified array affects the returned list, and changes made to the returned list affects the specified list.

### 6. Describing and Using Objects and Classes
* The compiler only adds the default constructor if a class isn't defined with an explicit one.
* Both _String_ and _StringBuilder_ classes implement the _CharSequence_ interface, thus we can pass objects of these classes to methods requiring a _CharSequence_ object.
* Objects passed in as a method parameter is not eligble for garbage collection even after the method returns.

### 7. Creating and Using Methods

```Java
public class Test {
    static String text1 = printAndEcho("a");

    static {
        printAndEcho("b");
    }

    static String text2 = printAndEcho("c");

    static String printAndEcho(String text) {
        System.out.println(text);
        return text;
    }

    public static void main(String[] args) { }
}
```
* _What is the output of the code above?_ All members of the given class are static, hence they are initialized and executed when the class is loaded. The emptiness of the _main_ method doesn't affect that process. The expressions initializing the two static fields as well as the static initialization block are executed in the order they are defined. As a result, the string **_abc_** is printed when the _Test_ class is loaded.
* A call to **_this()__** or **_super()_** inside a constructor, if any, **must** be the **first** statement. Of course _this()_ and _super()_ cannot be the first statement at the same time, meaning that we cannot call more than one constructor inside the body of another constructor.
* Passing a _String_ parameter to a method and modifying the parameter won't change the original object as _String_ is immutable.
* Unlike an object reference parameter that keeps the address of the passed-in argument, a primitive parameter stores a copy of the argument itself. Any changes made to this parameter only impact the copy, not the original value.
* When a static field is declared as _final_, it must be set when the class is loaded. This can be dine by initializing the fielld at the declaration point or using a static initialization block.
* When calling overloaded methods with a given argument, the compiler determines the applicable method by **following these three phases**:
  * The **first phase** performs overload resolution without permitting boxing or unboxing conversion, or the use of variable arity method invocation. If no applicable method is found during first phase, then processing continues to the second phase.
  * The **second phase** performs overload resolution while allowing boxing and unboxing, but still precludes the use of variable arity method invocation. If no applicable method is found during the second phase, then processing continues to the thirs phase.
  * The **third phase** allows overloading to be combined with variable arity methods, boxing, and unboxing.
* When classes are loaded, all static fields are initialized, and static methods/initialization blocks are executed.
* A method that looks like a constructor, but has a return type, is in fact not a constructor, just a regular method. Nothing wrong with that.

### 8. Applying Encapsulation
* Classes declared with no access modifier are package-private, meaning they are invisible outside of the containing package, and so are its members as well.

### 9. Reusing Implementations Through Inheritance

* Unlike methods, fields are never overridden. A field of an object is always associated with the reference type of the varaible referring to the object.
* _Polymorphism_: Subclasses can define their own unique behaviors and yet share some of the same functionality of the parent class.
* If a superclass have at least one constructor declared, the compiler will back off and not automatically generate a no-argument constructor. If a constructor is declared in the superclass, and there is no no-arguments constructor declared, any subclass that inherits the superclass **must** make an explicit call to its superclass' constructor.
* An _abstract_ method can **only** be defined in an _abstract_ class or an interface.
* An _abstract_ method is **always** NON-static.
* Static methods are not overridden, but hidden. The @Override annotation doesn't apply to method hiding.
* A _non-static_ method **cannot** override a static method. It will cause a compile-time error.
* A static method **cannot** hide or override a _non-static_ method. It will cause a compile-time error.
* When method overriding occurs, the overriding method cannot specify a checked exception that isn't specified by the overridden one. Specifying unchecked exceptions are valid, and so are subtypes of the overridden one. Cannot specify an exception class a class which isn't a subtype the overridden method specified exception.
* In Java, **fields** and **static methods** are **NOT** polymorphic, meaning they can be hidden, and not overridden. Therefor, override rules does not apply to fields and static methods. Field hiding occurs even if the fields in the subclass and superclass have different types.
* Static fields can be accessed via both class references and instance references. A class which is a subtype of the class containing a static field, inherits that field.
* To be able to override a method in a subclass, the method must have a return type that is a subtype of the method it overrides.

### 10. Programming Abstractly Through Interfaces

* When a field is declared in an interface, it's by default _public_, _static_ and _final_. Not initializing a declared field in an interface will lead to a **compile-time error**.
* Not all classes that implement an interface must override its methods: classes marked as _abstract_ does **not** need to override for the code to compile.
* An implementation class can define a field with the same name as a field in the interface it's implementing: doing so just **hides** the field in the interface.
* Overloading methods doesn't need to have a less restrictive access modifier; overriding methods does.
* An interface field is a constant, meaning it cannot be changed in an implementation class (ref. _final_ by default).
* A method in an interface is abstract by default, hence we don't need to add the _abstract_ keyword. However, it's still valid if we do.
* A field defined within a subtype can hide fields of the same name in supertypes, but a field defined in a supertype cannot hide other fields in other supertypes.
* The _List_ _remove_ method removes the **first occurrence** of the specified element.
  * The _remove_ method with an _int_ parameter removes the element at the specified position and returns the element itself.
  * The _remove_ method with an _Object_ parameter removes the first occurence of the specified element and returns _true_ if the list contains such an element, otherwise _false_.
* The _List add_ method with two parameters inserts the specified element, denoted by the second parameter, at the specified location, denoted by the first parameter.
* The _List_ _addAll_ method appends all of the elements in the specified colllection to the end of the list, in the order they are returned by the specified collection's iterator. If the method takes a first argument integer, all elements are inserted into the list at the specified position.
* The _List_ _subList_ method returns a view of the portion of the original list, starting at the index specified by the first parameter (inclusive) and ending at the index specified by the second parameter (exclusive). The method does **not modify** the original list.
* The _List_ _copyOf_ method returns an modifiable list containing elements of the original one. Calling any mutator method on the _List_ will **always** cause **_UnsupportedOperationException_** to be thrown.
* A static method with a body belongs to the interface its declared in, and subtypes of this interface don't even inherit that static method. Meaning they can define a method with the  exact same signature.
* When a class declares an extended class and implemented interfaces, the class name must go first, then interface names which are separated by commas. I.e. an extended class must first EXTEND one and only one class, then IMPLEMENT one or multiple interfaces, separated by commas, not the otherway around.
* The _List of_ method provides an unmodifiable list. Calling any mutator method on the _List_ will **ALWAYS** cause _UnsupportedOperationException_ to be thrown.

### 11. Handling Exceptions

* When a method throws a **checked** exception, it must be either caught or specified in method delcaration.
* Including throws clause for **unchecked** exceptions on a method declaration is redundant, however it doesn't harm if we still indicate such an exception on the method's declaration.
* Unchecked exceptions do not need an exception handling mechanism for the code to compile.
* When the exception type specified in the _catch_ block is a checked exception, it must match the type of exception objects that can be thrown in the _try_ block. If no such checked exception is thrown in the _try_ block, a compile-time error occurs where such an exception is caught.
* A _finally_ block, if existent, **must** be the last block in an exception handling handler, or else it is a compile-time error.
* The compiler doesn't evaluate any expression at compile time: thus, it must prepare for all possible workflows.
* When an exception is thrown from within a _try_ block, the first exception handler whose exception type matches the exception object takes action. When we specify multiple _catch_ blocks with exception types in the same inheritance hierarchy, the bllock with the most specific type must go first, and the one with the most general type is the last.
* An exception handler may contain only a _try_ block and a _finally_ block, i.e. a _try_ block must not always be followed by a _catch_ block.
* A _finally_ block may not always execute in special cases where the JVM exits, or the blocks previous is interrupted or killed etc.
* A _finally_ block can also throw exceptions.
* There cannot be more than one finally block in an exception handler.
* No code can be inserted between to adjacent blocks in an exception handler.
* 

### 12. Understanding Modules

* In addition to explicit dependencies, all modules depend on the base module (java.base). If one or more modules doesn't depend on the base module in a module graph, the option is WRONG. Every module must point to the java.base module.
* The _exports_ directive specify packages - it has **nothing** to do with the module graph.
* A module must explicitly require a depending module. Exporting a package in one module to another specific module does not exempt the target module from explicitly requiring the dependency module.
* You use the ```jdeps``` command to launch the Java class dependency analyzer.
* You can produce a dependency summary by using the _jdeps_ command with the _-s_ or _-summary_ option. E.g. ```jdeps --module-path . -s foo```.
* The _jdeps_ command shows the package-level or class-level dependencies of Java class files. The input class can be a path to a _.class_ file, a directory, a JAR file, or it can be a fully qualified class name (FQCN) to analyze all class files. The options determine the output. By default, the _jdeps_ command writes the dependencies to the system output. The command can generate the dependencies in DOT language (stored in _.dot_ files).
* Here's a description of the ```--print-module-deps``` option of the _jdeps_ command:
  * Same as ```--list-reduced-deps``` with printing a comma-separated list of module dependencies. The output can be used by ```jlink --add-modules``` to create a custom image that contains those modules and their transitive dependencies.
  * ```jdeps --module-path . --print-module-deps foo``` prints _bar,java.base_.
* With the modular JDK, we can create custom runtimes consisting of only modules needed for our apps or the devices we're targeting. This means the runtime's size can be much smaller than it was.
* With the modular JDK, internal APIs used by the platform itself are encapsulated and hidden from applications.
* When an application fires up, the JVM walks through the module graph. If any module is missing, the JVM produces an error and shuts down. This helps avoid catastrophic consequences if sucj an issue were only found at runtime.
* The ```-p``` and ```--module-path``` options specify where to find application modules, when compiling source files with the ```javac``` command.
* Executing a modular program:
  * The main module and all the dependency modules must be added to the module path. This module path is indicated by the _-m_ or _-module-path_ option.
  * When adding a module in a JAR file to the module path, we can specify that file or its containing directory.
  * The main class to be run must be specified under the containing module with the _-m_ or _--module_ option.
* Circular dependency is forbidden in Java, leading to a compile-time error. E.g. if module _bar_ requires module _foo_, and module _foo_ requires module _bar_, the dependency is circular.
* Multiple directories can be used to indicate the module path - these directories must be separated by semicolons (;).

## Java SE 11 Programmer II 1Z0-816

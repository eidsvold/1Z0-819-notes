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

* The _-d_ option of the _javac_ command sets the destination directory for class files. If a class is part of a package, then _javac_ puts the class file in a subdirectory that reflects the package name and creates directories as needed.

### 2. Understanding Java Technology and Environment

### 3. Working With Primitive Data Types and String APIs

* A _String_ object is immutable - in cannot be changed after being created. The _concat_ method appends the string argument to the end of the current string and returns the concatenation - hence the varible must be reassigned or assigned to another variable.

### 4. Using Operators and Decision Constructs

* A _**switch** statement_ can only work with the following primitive data types: _byte_, _short_, _char_, and _int_. It also works with _enumerated types_, the _String_ class, and a few special classes that wrap certain primitive types: _Character_, _Byte_, _Short_ and _Integer_.

### 5. Working with Java Arrays

* 

### 6. Describing and Using Objects and Classes

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
* _What is the output of the code above?_ All members of the given class are static, hence they are initialized and executed when the class is laoded. The emptiness of the _main_ method doesn't affect that process. The expressions initializing the two static fields as well as the static initialization block are executed in the order they are defined. As a result, the string **_abc_** is printed when the _Test_ class is loaded.

### 8. Applying Encapsulation

### 9. Reusing Implementations Through Inheritance

* Unlike methods, fields are never overridden. A field of an object is always associated with the reference type of the varaible referring to the object.
* _Polymorphism_: Subclasses can define their own unique behaviors and yet share some of the same functionality of the parent class.
* If a superclass have at least one constructor declared, the compiler will back off and not automatically generate a no-argument constructor. If a constructor is declared in the superclass, and there is no no-arguments constructor declared, any subclass that inherits the superclass **must** make an explicit call to its superclass' constructor.

### 10. Programming Abstractly Through Interfaces

* When a field is declared in an interface, it's by default _public_, _static_ and _final_. Not initializing a declared field in an interface will lead to a **compile-time error**.
* Not all classes that implement an interface must override its methods: classes marked as _abstract_ does **not** need to override for the code to compile.
* An implementation class can define a field with the same name as a field in the interface it's implementing: doing so just **hides** the field in the interface.
* Overloading methods doesn't need to have a less restrictive access modifier; overriding methods does.
* An interface field is a constant, meaning it cannot be changed in an implementation class (ref. _final_ by default).

### 11. Handling Exceptions

* Including throws clause for unchecked exceptions on a method declaration is redundant, however it doesn't harm if we still indicate such an exception on the method's declaration.
* Unchecked exceptions do not need an exception handling mechanism for the code to compile.
* When the exception type specified in the _catch_ block is a checked exception, it must match the type of exception objects that can be thrown in the _try_ block. If no such checked exception is thrown in the _try_ block, a compile-time error occurs where such an exception is caught.
* A _finally_ block, if existent, **must** be the last block in an exception handling handler, or else it is a compile-time error.

### 12. Understanding Modules

* In addition to explicit dependencies, all modules depend on the base module (java.base).
* The _exports_ directive specify packages - it has **nothing** to do with the module graph.

## Java SE 11 Programmer II 1Z0-816

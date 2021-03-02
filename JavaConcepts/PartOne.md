# JVM ,JRE and JDK

This is how the magic happens, you write your logic aka code in a java file, its converted into class file so that the machine can read your logic  and run it.



![image-20200913105154181](C:\Users\gmalarski\AppData\Roaming\Typora\typora-user-images\image-20200913105154181.png)



- JVM is the java virtual machine that runs the java byte code.
- JVM can be loaded on various hardware platforms, byte codes are the machine language of JVM. So Java is a better portable language. JVM is the  entity that makes Java portable; there are different implementations of  JVM for different OS (mac, windows, linux) etc.
- JRE is java runtime environment that is sufficient to run the program.
- JRE = JVM + library files/java package classes (Util, Lang, Math etc).
- JDK is java development kit, required to write, compile and run a program.
- JDK = JRE + Tools needed to develop java program.

# Memory Allocation

So in the backgroud how the memory allcation works from your code. Brief pointers:

- Each time object is created in Java it is stored in heap memory.
- Primitive variables and local are stored in stack, member variables in heap.
- In multithreading each thread will have its own stack but will share same heap. We will discuss multithreading later in part 2.
- Methods and variables are pushed to the stack when a method is invoked and stack pointer is decremented when call is completed.
- 32 bit OS can’t use more than 4GB RAM for java application. 64 bit use more memory for same object, almost twice.
- Primitive int uses 4 times less memory than Integer.

![Image for post](https://miro.medium.com/max/600/0*YnLwmAEJscRkHwx_.)

The below table gives an idea of various datatypes and range of values it can hold.

![Image for post](https://miro.medium.com/max/974/1*uOebRGa_vJm6x5xhtPF88w.png)

# OOPS — Encapsulation, Inheritance, Polymorphism, and Abstraction

Object Oriented Programming(OOP) is a programming concept that works on the 4 principles.

## **1. Encapsulation**

Encapsulation is wrapping data(variables) and functionality(methods) together as a  single unit. Functionalities mean “methods” and data means “variables”.  Its all wrapped in is “class.” It is a blueprint or a set of  instruction.

**Class**: A class is a blueprint or prototype that defines the variables and the methods. For example:

> Class: Car
> Data members or objects: color, type, model, etc.
> Methods: stop, accelerate, cruise.

**Object**: Now, an object is a specimen of a class. Like in the above example my car is an object of the class Car.

**Variable**: can be local, instance and static. Local variables are declared inside  the body of a method. Instance variables are declared outside method.  They are object specific. Static variables are initialized only once and at the start of program execution. Static variables are initialized  first, we will discuss static in detail later.

**Method**: methods are various functionalities, its nothing but set of code which  is referred to by name and can be called (invoked) at any point in a  program. You can pass multiple values to a method and it returns  value(s).

**Package**: A Package is a collection of related classes. It helps organize classes into a folder structure and make it easy to locate and reuse them.

```java
package com.example;

class Car {
    String color = "black"; //instance variable  
    void accelerate() { 
        int speed = 90; //local variable
    }
}
```

## 2. Abstraction

Abstraction is selecting data from a larger pool to show only the relevant details  to the object. Here is a chart showing different access modifiers and  how it restricts the data from a class.

![Image for post](https://miro.medium.com/max/773/1*F9fPgoOxgzEGDrd2bJpfkQ.png)

## 3. Inheritance

Inheritance is a mechanism in which one class acquires the property of another  class. For example, a child inherits the traits of his/her parents.

```java
class Developer{
  public void writeCode(){
  // writeCode method
  
}
class BackendDeveloper extends Developer{
  public void writeCode(){
  // writeCode method
  }
}
Class run{
  public static void main (String args[]){
    Developer developerObject = new Developer()
	// writeCode method in class Developer will be executed
    developerObject.writeCode();
   
    BackendDeveloper backendDeveloperObj = new BackendDeveloper();
    // writeCodemethod in class BackendDeveloper will be executed
    backendDeveloperObj.writeCode();
  }
}
```

## 4. Polymorphism

Polymorphism is a OOPs concept where one name can have many forms also knows as  overloading. Dynamic Polymorphism is the mechanism by which multiple  methods can be defined with same name and signature in the superclass  and subclass also known as overriding.

- Overloading is multiple methods in the same class with same name but different method signature.
- Overriding deals with two methods, one in parent class and one in child class and both have same name and signature.
- Subclass method overrides the method from super class.
- In overriding sub classes access modifier must be greater than parent class E.g if we use *public abc()* in parent class and *private abc()* in sub class that will throw exception.

# Static Class Loading and Dynamic Class Loading

- Loading the class to JVM to run is called class loading.
- Classes are statically loaded using new operator.
- Very first class is loaded using static main() method and then subsequent class are loaded.
- Server based projects do not have main() at all, server provides  infrastructure. Class to be loaded first is mentioned in config file. So the framework implements main() method and provides API in many cases.  E.g: Container invokes init() method in servelets.
- Main is required when Java program is run on JVM from command prompt.
- NoClassDefinationFoundException is thrown if class reference is not found during static class loading.
- Dynamic class loading is programmatically invoking class at run time. E.g: Class.forName(String ClassName);
- ClassNotFoundException is thrown for dynamic class loading.

# Abstract Class and Interface

- Interface has no implementation code and all methods are abstract i.e. all methods are only declared and none are defined.
- Abstract class has executable methods and abstract methods.
- A class can implement any number of interfaces but can extend only one abstract class.
- In abstract class methods can be abstract and may not be.
- An abstract class cannot be instantiated in can only be subclassed.
- All abstract methods must be defined in subclass else the subclass should be abstract.
- Interface cannot be instantiated it can only be implemented by other classes or extended by other interfaces.
- Interface variables are final and static; interface methods are public and abstract by default.
- Interface cannot contain implementation and cannot be subclassed, so variables have to be constant.

# Java Packages

Here are some libraries available in java package to help code better. We will discuss them all eventually.

![Image for post](https://miro.medium.com/max/889/1*9-kl0KixCNNWIxo_6NmndA.png)
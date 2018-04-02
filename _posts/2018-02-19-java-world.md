---
title: Java World
description: We all love Java!
categories:
- Java
tags:
- Java
---


![Java Learning Path](/assets/images/post/java-world/java.png)
## 1. Basics

### Data Type
#### Primitive Data Types

byte, short, int, long, char, float, double, boolean

#### Object Data Types

class, interface, array

![Data Types](http://i1.wp.com/javafrombasics.com/wp-content/uploads/2016/06/data-types.gif?zoom=2&fit=720%2C540)

### Access Modifier
> Access level modifiers determine whether other classes can use a particular field or invoke a particular method. There are two levels of access control:
> - At the top level—public, or package-private (no explicit modifier).
> - At the member level—public, private, protected, or package-private (no explicit modifier).

![Access Modifier](https://qph.fs.quoracdn.net/main-qimg-07b6e84dcef8589f6fd02323f103a4cf.webp)

### Abstract Class & Interface
#### Abstract Class
An abstract class can have abstract and non-abstract methods.
#### Interface
Methods in an interface are by default public and abstract; variables in an interface are by default public, static and final. An interface can only have abstract methods.
#### Example
```java
// Creating interface that has 4 methods
interface A {
    void a();//bydefault, public and abstract
    void b();
    void c();
    void d();
}

// Creating abstract class that provides the
// implementation of one method of A interface
abstract class B implements A {
    public void c() {
        System.out.println("I am C");
    }
}

// Creating subclass of abstract class,
// now we need to provide the implementation of rest of the methods
class M extends B {
    public void a() {
        System.out.println("I am a");
    }
    public void b() {
        System.out.println("I am b");
    }
    public void d() {
        System.out.println("I am d");
    }
}

// Creating a test class that calls the methods of A interface
class Test {
    public static void main(String args[]) {
        A a = new M();
        a.a();
        a.b();
        a.c();
       a.d();
    }
}
```

## 2. Object Oriented Programming
### Abstraction

### Encapsulation
Encapsulation in Java is a mechanism of wrapping the data (variables) and code acting on the data (methods) together as a single unit. In encapsulation, the variables of a class will be hidden from other classes, and can be accessed only through the methods of their current class. Therefore, it is also known as data hiding.

To achieve encapsulation in Java:
+ Declare the variables of a class as private.
+ Provide public setter and getter methods to modify and view the variables values.

### Inheritance
### Polymorphism
#### Overloading

static / compile time polymorphism

#### Overriding

dynamic / run time polymorphism

![Overloading and Overriding](https://www.programcreek.com/wp-content/uploads/2009/02/overloading-vs-overriding.png)

### Design Pattern
#### Singleton Pattern
Intent:
+ Ensure that only one instance of a class is created.
+ Provide a global point of access to the object.

```java
public class Singleton {
    private static Singleton instance;
    private Singleton() {
        ...
    }
    public static synchronized Singleton getInstance() {
        if (instance == null) instance = new Singleton();
        return instance;
    }
    ...
    public void doSomething() {
        ...
    }
}
```
#### Factory Pattern
Intent:
+ The client needs a product, but instead of creating it directly using the new operator, it asks the factory object for a new product, providing the information about the type of object it needs.
+ The factory instantiates a new concrete product and then returns to the client the newly created product(casted to abstract product class).
+ The client uses the products as abstract products without being aware about their concrete implementation.

```java
public class ProductFactory {
    public Product createProduct(String ProductID) {
        if (id == ID1) return new OneProduct();
        if (id == ID2) return new AnotherProduct();
        ... // so on for the other Ids
        return null; // if the id doesn't have any of the expected values
    }
    ...
}
```

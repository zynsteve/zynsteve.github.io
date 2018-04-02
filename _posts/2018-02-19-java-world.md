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

### Encapsulation

### Inheritance

### Polymorphism
#### Overloading

static / compile time polymorphism

#### Overriding

dynamic / run time polymorphism

![Overloading and Overriding](https://www.programcreek.com/wp-content/uploads/2009/02/overloading-vs-overriding.png)

### Design Pattern
#### Singleton Pattern
#### Factory Pattern


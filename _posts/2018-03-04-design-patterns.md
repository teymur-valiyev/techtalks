---
author: teymur
comments: true
date: 2018-03-04 22:16:08+00:00
layout: post
slug: design-pattern
title: Design Patterns
categories: Tutorial
tags:
- design patterns
- oop
---

# Design patterns


#### Design Principle
> Identify the aspects of your application that vary and separate them from what stays the same.

> take the parts that vary and encapsulate them, so that later you can alter or extend the parts that vary without affecting those that don’t.

Separating what changes from what stays the same
if things vary i can make them standalone class 

> Program to an interface, not an implementation.

Programming to an implementation would be:
```
Dog d = new Dog();
d.bark();
```
Programming to an interface/supertype would be:
```
Animal animal = new Dog(); // we can now a Dog, but use the animal
animal.makeSound();
```

> Favor composition over inheritance.

> Strive for loosely coupled designs between objects that interact.

> Classes should be open for extension, but closed for modification.

> Depend upon abstractions. Do not depend upon concrete classes.

> Principle of Least Knowledge -talk only to your immediate friends.

> The Hollywood Principle Don’t call us, we’ll call you.


#### The Open-Closed Principle
##### The Dependency Inversion Principle

--------------------------------------------------------------------

### The Strategy Pattern

The Strategy Pattern defines a family of algorithms, encapsulates each one, and makes them interchangeable.
Strategy lets the algorithm vary independently from clients that use it.

#### Observer Pattern

Publishers + Subscribers = Observer Pattern

The Observer Pattern defines a one-to-many dependency between objects so that when one object changes state, all of its dependents are notified and updated automatically.

#### Loose Coupling.
When two objects are loosely coupled, they can interact, but have very little knowledge of each other.
The Observer Pattern provides an object design where subjects and observers are loosely coupled.
Loosely coupled designs allow us to build flexible OO systems that can handle change because they minimize
the interdependency between objects.


programming idiom.





#### The Adapter Pattern

The Adapter Pattern converts the interface of a class
into another interface the clients expect. Adapter lets
classes work together that couldn’t otherwise because of
incompatible interfaces.

object adapters and class adapters


So what’s a class adapter and why haven’t we told you about it? Because you need
multiple inheritance to implement it, which isn’t possible in Java



Decorator 	Doesn’t alter the interface, but adds responsibility
Adapter 	Converts one interface to another
Facade 		Makes an interface simpler


The difference between the two is not in
terms of how many classes they “wrap,” it
is in their intent. The intent of the Adapter
Pattern is to alter an interface so that it
matches one a client is expecting. The
intent of the Facade Pattern is to provide a
simplified interface to a subsystem.





#### Bridge Pattern

Abstraction -  Car interface
Implementation -  Ferrari 



---------------------------------------------------------------------------

## Creational design patterns

These design patterns are all about class instantiation. This pattern can be further divided into class-creation patterns and object-creational patterns. While class-creation patterns use inheritance effectively in the instantiation process, object-creation patterns use delegation effectively to get the job done.

### Abstract Factory
Creates an instance of several families of classes

```
abstract class CPU {}

class EmberCPU extends CPU {}

class EnginolaCPU extends CPU {}

abstract class MMU {}

class EmberMMU extends MMU {}

class EnginolaMMU extends MMU {}

class EmberToolkit extends AbstractFactory {
    @Override
    public CPU createCPU() {
        return new EmberCPU();
    }

    @Override
    public MMU createMMU() {
        return new EmberMMU();
    }
}

class EnginolaToolkit extends AbstractFactory {
    @Override
    public CPU createCPU() {
        return new EnginolaCPU();
    }

    @Override
    public MMU createMMU() {
        return new EnginolaMMU();
    }
}

enum Architecture {
    ENGINOLA, EMBER
}

abstract class AbstractFactory {
    private static final EmberToolkit EMBER_TOOLKIT = new EmberToolkit();
    private static final EnginolaToolkit ENGINOLA_TOOLKIT = new EnginolaToolkit();

    static AbstractFactory getFactory(Architecture architecture) {
        AbstractFactory factory = null;
        switch (architecture) {
            case ENGINOLA:
                factory = ENGINOLA_TOOLKIT;
                break;
            case EMBER:
                factory = EMBER_TOOLKIT;
                break;
        }
        return factory;
    }

    public abstract CPU createCPU();

    public abstract MMU createMMU();
}

public class Client {
    public static void main(String[] args) {
        AbstractFactory factory = AbstractFactory.getFactory(Architecture.EMBER);
        CPU cpu = factory.createCPU();
    }
}

```


### Factory Method

The Factory Method Pattern defines an interface for creating an object, but lets subclasses decide which
class to instantiate. Factory Method lets a class defer instantiation to subclasses.

```
interface ImageReader {
    DecodedImage getDecodeImage();
}

class DecodedImage {
    private String image;

    public DecodedImage(String image) {
        this.image = image;
    }

    @Override
    public String toString() {
        return image + ": is decoded";
    }
}

class GifReader implements ImageReader {
    private DecodedImage decodedImage;

    public GifReader(String image) {
        this.decodedImage = new DecodedImage(image);
    }

    @Override
    public DecodedImage getDecodeImage() {
        return decodedImage;
    }
}

class JpegReader implements ImageReader {
    private DecodedImage decodedImage;

    public JpegReader(String image) {
        decodedImage = new DecodedImage(image);
    }

    @Override
    public DecodedImage getDecodeImage() {
        return decodedImage;
    }
}

public class FactoryMethodDemo {
    public static void main(String[] args) {
        DecodedImage decodedImage;
        ImageReader reader = null;
        String image = args[0];
        String format = image.substring(image.indexOf('.') + 1, (image.length()));
        if (format.equals("gif")) {
            reader = new GifReader(image);
        }
        if (format.equals("jpeg")) {
            reader = new JpegReader(image);
        }
        assert reader != null;
        decodedImage = reader.getDecodeImage();
        System.out.println(decodedImage);
    }
}

```


##### Factory Method and Abstract Factory

 Example
```
class A {
    public void doSomething() {
        Foo f = makeFoo();
        f.whatever();   
    }

    protected Foo makeFoo() {
        return new RegularFoo();
    }
}

class B extends A {
    protected Foo makeFoo() {
        //subclass is overriding the factory method 
        //to return something different
        return new SpecialFoo();
    }
}
```
And here is an abstract factory in use:
```
class A {
    private Factory factory;

    public A(Factory factory) {
        this.factory = factory;
    }

    public void doSomething() {
        Foo f = factory.makeFoo();
        f.whatever();
    }
}

interface Factory {
    Foo makeFoo();
    Bar makeBar();
}
```

	Factory pattern creates single object 
	Absract Factory Patterns constructs  multiple objects

### Builder

Builder pattern builds a complex object using simple objects and using a step by step approach. 

 Example 
```
public class BankAccount {
    public static class Builder {
        private long accountNumber; 
        private String owner;
        private String branch;
        private double balance;
        private double interestRate;

        public Builder(long accountNumber) {
            this.accountNumber = accountNumber;
        }
        public Builder withOwner(String owner){
            this.owner = owner;
            return this; 
        }
        public Builder atBranch(String branch){
            this.branch = branch;
            return this;
        }
        public Builder openingBalance(double balance){
            this.balance = balance;
            return this;
        }
        public Builder atRate(double interestRate){
            this.interestRate = interestRate;
            return this;
        }
        public BankAccount build(){
            BankAccount account = new BankAccount(); 
            account.accountNumber = this.accountNumber;
            account.owner = this.owner;
            account.branch = this.branch;
            account.balance = this.balance;
            account.interestRate = this.interestRate;
            return account;
        }
    }

    private BankAccount() {
        //Constructor is now private.
    }
}
```

```
BankAccount account = new BankAccount.Builder(1234L)
            .withOwner("Marge")
            .atBranch("Springfield")
            .openingBalance(100)
            .atRate(2.5)
            .build();

```
https://dzone.com/articles/design-patterns-the-builder-pattern

 Example 2 	

```
class Pizza {
    private String dough = "";
    private String sauce = "";
    private String topping = "";

    public void setDough(String dough) {
        this.dough = dough;
    }

    public void setSauce(String sauce) {
        this.sauce = sauce;
    }

    public void setTopping(String topping) {
        this.topping = topping;
    }
}
```

```
abstract class PizzaBuilder {
    protected Pizza pizza;

    public Pizza getPizza() {
        return pizza;
    }

    public void createNewPizzaProduct() {
        pizza = new Pizza();
    }

    public abstract void buildDough();
    public abstract void buildSauce();
    public abstract void buildTopping();
}
```

```
class HawaiianPizzaBuilder extends PizzaBuilder {
    public void buildDough() {
        pizza.setDough("cross");
    }

    public void buildSauce() {
        pizza.setSauce("mild");
    }

    public void buildTopping() {
        pizza.setTopping("ham+pineapple");
    }
}
```

```
class SpicyPizzaBuilder extends PizzaBuilder {
    public void buildDough() {
        pizza.setDough("pan baked");
    }

    public void buildSauce() {
        pizza.setSauce("hot");
    }

    public void buildTopping() {
        pizza.setTopping("pepperoni+salami");
    }
}
```

```
class Waiter {
    private PizzaBuilder pizzaBuilder;

    public void setPizzaBuilder(PizzaBuilder pb) {
        pizzaBuilder = pb;
    }

    public Pizza getPizza() {
        return pizzaBuilder.getPizza();
    }

    public void constructPizza() {
        pizzaBuilder.createNewPizzaProduct();
        pizzaBuilder.buildDough();
        pizzaBuilder.buildSauce();
        pizzaBuilder.buildTopping();
    }
}
```

```
public class PizzaBuilderDemo {
    public static void main(String[] args) {
        Waiter waiter = new Waiter();
        PizzaBuilder hawaiianPizzabuilder=new HawaiianPizzaBuilder();
        PizzaBuilder spicyPizzaBuilder = new SpicyPizzaBuilder();

        waiter.setPizzaBuilder( hawaiianPizzabuilder );
        waiter.constructPizza();

        Pizza pizza = waiter.getPizza();
    }
}
```

### Object Pool
Avoid expensive acquisition and release of resources by recycling objects that are no longer in use

### Prototype
A fully initialized instance to be copied or cloned

### Singleton
A class of which only a single instance can exist

```
public class SingleObject {

   private static SingleObject instance = new SingleObject();

   private SingleObject(){}

   public static SingleObject getInstance(){
      return instance;
   }

   public void showMessage(){
      System.out.println("Hello World!");
   }
}
```

```
public class SingletonPatternDemo {
   public static void main(String[] args) {

      SingleObject object = SingleObject.getInstance();
      object.showMessage();
   }
}
```















## Structural design patterns
These design patterns are all about Class and Object composition. Structural class-creation patterns use inheritance to compose interfaces. Structural object-patterns define ways to compose objects to obtain new functionality.

### Adapter
Match interfaces of different classes

### Bridge
Separates an object’s interface from its implementation


### Composite

The Composite Pattern allows you to compose objects into tree structures to represent part-whole hierarchies. Composite lets clients treat individual objects and compositions of objects uniformly.

compenent 
composite 
leaf

learn Tree


### Decorator

The Decorator Pattern attaches additional responsibilities to an object dynamically.
Decorators provide a flexible alternative to subclassing for extending functionality.

With composition, we can mix and match decorators any way we like... at runtime.
Java I/O Decorator

### Facade 

The Facade Pattern provides a unified interface to a set of interfaces in a subsytem. Facade defines a higher-level interface that makes the subsystem easier to use.



### Flyweight
A fine-grained instance used for efficient sharing

### Private Class Data
Restricts accessor/mutator access

### Proxy
An object representing another object


## Behavioral design patterns

These design patterns are all about Class's objects communication. Behavioral patterns are those patterns that are most specifically concerned with communication between objects.


### Chain of responsibility
A way of passing a request between a chain of objects

### Command

The Command Pattern encapsulates a request as an
object, thereby letting you parameterize other objects
with different requests, queue or log requests, and support
undoable operations.

### Iterator
Sequentially access the elements of a collection

### Mediator
Defines simplified communication between classes

### Memento
Capture and restore an object's internal state

### Null Object
Designed to act as a default value of an object

### Observer
A way of notifying change to a number of classes

### State
Alter an object's behavior when its state changes



### Strategy
Encapsulates an algorithm inside a class

### Template method

The Template Method defines the steps of an algorithm and allows
subclasses to provide the implementation for one or more steps.

The Template Method Pattern defines the skeleton
of an algorithm in a method, deferring some steps to
subclasses. Template Method lets subclasses redefine
certain steps of an algorithm without changing the
algorithm’s structure.

beforeSave() magento 2 is hook of template pattern


### Visitor
Defines a new operation to a class without change
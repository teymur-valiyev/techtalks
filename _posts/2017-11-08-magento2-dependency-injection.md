---
author: teymur
comments: false
date: 2005-05-13 22:16:08+00:00
layout: post
slug: magento2-dependency-injection
title: Magento 2 Dependency Injection
categories: Personal
tags:
- php
- magento2
- oop
---


In Java, all classes inherit from Object, but there is no such generic super-class in PHP.

Major 3 things I always remember for OO PHP does not have:

1. PHP has no main function for classes.
2. Like C++ you have declare a constructor and destructor i.e. __construct()
3. You cannot declare final (constant) to your variables, but to methods and classes so that they cannot be overrided and inherited repsectivley.


> The include (or require) statement takes all the text/code/markup that exists in the specified file and copies it into the file that uses the include statement.

    The include and require statements are identical, except upon failure:
        require will produce a fatal error (E_COMPILE_ERROR) and stop the script
        include will only produce a warning (E_WARNING) and the script will continue![alt text]( "Logo Title Text 1")

```
include('pageBanner.php');
or
require('pageBanner.php');
```

Assume we have a standard footer file called "footer.php", that looks like this:
```
// footer.php
<?php
echo "<p>Copyright &copy; 1999-" . date("Y") . " W3Schools.com</p>";
?>
```
```
<!-- index.html -->
<html>
    <body>
        <h1>Welcome to my home page!</h1>
        <p>Some text.</p>
        <?php include 'footer.php';?>
    </body>
</html>
``` 

## Autoloading

PHP doesn't have packages, but it does have namespaces.

```
namespace B
{ 
  class A
  {
    public static function say()
    {
      echo 'Я пространство имен B';
    }
  }
}

namespace A;
  class A
  {
    public static function say()
    {
      echo 'Я пространство имен А';
    }
  }

require_once 'A.php';
require_once 'B.php';

use A\A;
use B\A

A\A::say();
B\A::say();
```

> Autoloading allows us to use PHP classes without the need to require() or include() 

    __autoload — Attempt to load undefined class

```
<?php 
use App\Controller\MyClass as MC;

$obj = new MC();
echo $obj->WhoAmI();

function __autoload($class) {
	$class = 'classes\' . str_replace('\\', '/', $class) . '.php';
	require_once($class);
}
```

> spl_autoload_register — Register given function as __autoload() implementation

```
<?php
class Autoloader {
    static public function loader($className) {
        $filename = "Classes/" . str_replace("\\", '/', $className) . ".php";
        if (file_exists($filename)) {
            include($filename);
            if (class_exists($className)) {
                return TRUE;
            }
        }
        return FALSE;
    }
}
spl_autoload_register('Autoloader::loader');
```

--------------------------

## Composer 
### Dependency Manager for PHP


Composer solves the following problems:

* dependency resolution for PHP packages
* autoloading solution for PHP packages
* keeping all packages updated


Create and empy file in the myproject folder, called composer.json:

>/var/www/myproject/composer.json

>Kint - debugging helper for PHP developers
```
{
    "require": {
        "raveren/kint": "0.9"
    }
}
```

> composer install

Composer has created a folder named vendor in your project

```
//index.php
<?php
require 'vendor/autoload.php';
```

This loads the Composer autoloader. So this line includes everything that Composer has downloaded into the project.


```
// create demo data
$variable = [1, 17, "hello", null, [1, 2, 3]];

// use KINT directly (which has been loaded automatically via Composer)
d($variable);
```
```
{
    "require": {
        "raveren/kint": "0.9",
        "phpmailer/phpmailer": "5.2.*"
    }
}
```

##Magento
>Magento is the World’s #1 Commerce Platform
Magento is the leading platform for open commerce innovation. Every year, Magento handles over $100 billion in gross merchandise volume


>Magento is the leading eCommerce platform used for online stores. It is a high-performant, scalable solution with powerful out of the box functionality and a large community built around it that continues to add new features.

CE AND EE
* MAGENTO - (2008)
* MAGENTO 2 - (2015)


---------------------------------------



__wakeup(), __sleep()



The __get() method is called whenever you attempt to read a non-existing or private property of an object.
The __set() method is called whenever you attempt to write to a non-existing or private property of an object.

```
<?php
 
class Person{
	private $firstName;
 
	public function __get($propertyName){
		echo "attempted to read non-existing property: $propertyName";
	}	
	public function __set($propertyNane, $propertyValue){
		echo "attempted to write to non-existing property: $propertyNane";
	} 
}
 
$p = new Person();

$p->firstName = 'Doe';
echo $p->firstName;
 
$p->lastName = 'John';
echo $p->lastName;
```


    First, we attempted to write and read a private property: $firstName.  The method __get() and __set() methods are called automatically.
    Second, we attempted to write and read a non-existing property: $lastName. The method __get() and __set() methods are also called automatically.



Similar to the __get() and __set() methods, the __call() magic method is called automatically when a nonexistent method of the class is called. 

https://code.tutsplus.com/tutorials/deciphering-magic-methods-in-php--net-13085

----------------------------------------------

## Dependency Injection
More specifically, dependency injection is effective in these situations:

	You need to inject configuration data into one or more components.
	You need to inject the same dependency into multiple components.
	You need to inject different implementations of the same dependency.
	You need to inject the same implementation in different configurations.
	You need some of the services provided by the container.


### Dependency injection is not effective if:

	You will never need a different implementation.
	You will never need a different configuration.
	
#### Advantages of DI

    Reduces class coupling
    Increases code reusability
    Improves code maintainability
    Improves application testing
    Centralized configuration

#### Drawback

    The main drawback of dependency injection is that using many instances together can become a very difficult if there are too many instances and many dependencies that need to be resolved.	
	

There are at least three ways an object can receive a reference to an external module
        
1. constructor injection: the dependencies are provided through a class constructor.
2. setter injection: the client exposes a setter method that the injector uses to inject the dependency.
3. interface injection: the dependency provides an injector method that will inject the dependency into any client passed to it. Clients must implement an interface that exposes a setter method that accepts the dependency.

#### Constructor injection
This method requires the client to provide a parameter in a constructor for the dependency.
``` 
// Constructor
Client(Service service) {
    // Save the reference to the passed-in service inside this client
    this.service = service;
}
```

#### Setter injection
This method requires the client to provide a setter method for the dependency.
```
// Setter method
public void setService(Service service) {
    // Save the reference to the passed-in service inside this client
    this.service = service;
}
```
#### Interface injection
This is simply the client publishing a role interface to the setter methods of the client's dependencies. It can be used to establish how the injector should talk to the client when injecting dependencies.
```
// Service setter interface.
public interface ServiceSetter {
    public void setService(Service service);
}

public class Client implements ServiceSetter {
    // Internal reference to the service used by this client.
    private Service service;

    // Set the service that this client is to use.
    @Override
    public void setService(Service service) {
        this.service = service;
    }
}
```

## Magento2 Object Manager

> Magento uses constructor injection to provide dependencies through an object’s class constructor.
#### Overview

Large applications, such as the Magento application, use an object manager to avoid boilerplate code when composing objects during instantiation.

#### Responsibilities

The object manager has the following responsibilities:

	Object creation in factories and proxies.
	Implementing the singleton pattern by returning the same shared instance of a class when requested.
	Dependency management by instantiating the preferred class when a constructor requests its interface.
	Automatically instantiating parameters in class constructors.

#### Configuration

	The di.xml file configures the object manager and tells it how to handle dependency injection.

	This file specifies the preferred implementation class the object manager generates for the interface declared in a 

	class constructor.


#### Injection types used in Magento

This section explains the two dependency injection types used in Magento using the following example:

``` 
namespace Magento\Backend\Model\Menu;
class Builder
{
    /**
     * @param \Magento\Backend\Model\Menu\Item\Factory $menuItemFactory
     * @param \Magento\Backend\Model\Menu $menu
     */
    public function __construct(
        Magento\Backend\Model\Menu\Item\Factory $menuItemFactory,  // Service dependency
        Magento\Backend\Model\Menu $menu  // Service dependency
    ) {
        $this->_itemFactory = $menuItemFactory;
        $this->_menu = $menu;
    }

    public function processCommand(\Magento\Backend\Model\Menu\Builder\CommandAbstract $command) // API param
    {
        // processCommand Code
    }
}
```

Let’s examine how this works on a simple example:
``` 
class A
{
  public function __construct(B $b)
  {
    $this->_b = $b;
  }
}
```
When creating object from class A, the following would happen:

* ObjectManager->create(‘A’) is called
* Constructor of A is examined
* Class B is being created, and used for creating A


Magento 2, they are separated into two groups: injectable, and non-injectable.

> Injectable: Service objects that are singletons obtained through dependency injection. The object manager uses the configuration in the di.xml file to create these objects and inject them into constructors.

> Newable/non-injectable: Objects obtained by creating a new class instance every time. Transient objects, such as those that require external input from the user or database, fall into this category. Attempts to inject these objects produce either an error that the object could not be created or an incorrect object that is incomplete.

---------------------------------------
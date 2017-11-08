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



<?php 
	include('pageBanner.php');
	require('pageBanner.php');
 ?>

 require is identical to include except upon failure it will also produce a fatal E_COMPILE_ERROR level error. 

Autoloading allows us to use PHP classes without the need to require() or include() 

PHP doesn't have packages, but it does have namespaces.

In Java, all classes inherit from Object, but there is no such generic super-class in PHP.

Major 3 things I always remember for OO PHP does not have:

1-PHP has no main function for classes.

2-Like C++ you have declare a constructor and destructor i.e. __construct()

3-You cannot declare final (constant) to your variables, but to methods and classes so that they cannot be overrided and inherited repsectivley.

```
use App\Controller\MyClass as MC;

$obj = new MC();
echo $obj->WhoAmI();

function __autoload($class) {
	$class = 'classes\' . str_replace('\\', '/', $class) . '.php';
	require_once($class);

}
```

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

```
require_once 'A.php';
require_once 'B.php';

use A\A;
use B\A

A\A::say();
B\A::say();

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

Dependency Manager for PHP


Composer solves the following problems:

* dependency resolution for PHP packages
* autoloading solution for PHP packages
* keeping all packages updated


/var/www/myproject/

Create and empy file in the myproject folder, called composer.json:

/var/www/myproject/composer.json

Kint - debugging helper for PHP developers

{
    "require": {
        "raveren/kint": "0.9"
    }
}


composer install

Composer has created a folder named vendor in your project

index.php
<?php
require 'vendor/autoload.php';

This loads the Composer autoloader. So this line includes everything that Composer has downloaded into the project.

index.php
<?php
// load Composer
require 'vendor/autoload.php';

// create demo data
$variable = array(1, 17, "hello", null, array(1, 2, 3));

// use KINT directly (which has been loaded automatically via Composer)
d($variable);


{
    "require": {
        "raveren/kint": "0.9",
        "phpmailer/phpmailer": "5.2.*"
    }
}




Magento is the World’s #1 Commerce Platform
Magento is the leading platform for open commerce innovation. Every year, Magento handles over $100 billion in gross merchandise volume


Magento is the leading eCommerce platform used for online stores. It is a high-performant, scalable solution with powerful out of the box functionality and a large community built around it that continues to add new features.

MAGENTO -- 2008
MAGENTO 2 -- 2015

Community
Enterprice

CE AND EE


---------------------------------------



__wakeup(), __sleep()



The __get() method is called whenever you attempt to read a non-existing or private property of an object.
The __set() method is called whenever you attempt to write to a non-existing or private property of an object.

```
<?php
 
class Person{
	private $firstName;
 
	public function __get($propertyName){
		echo "attempted to read non-existing property: $propertyName 
";
	}	
	public function __set($propertyNane, $propertyValue){
		echo "attempted to write to non-existing property: $propertyNane 
";
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

```
<?php
 
class Person{
	private $properties;
 
	public function __get($propertyName){
		if(array_key_exists($propertyName, $properties)){
			return $this->properties[$propertyName];
		}
 
	}	
	public function __set($propertyNane, $propertyValue){
		$this->properties[$propertyNane] = $propertyValue;
	} 
 
}
 
$p = new Person();
$p->lastName = 'John';
$p->firstName = 'Doe';
 
var_dump($p);
```


PHP __call() method

Similar to the __get() and __set() methods, the __call() magic method is called automatically when a nonexistent method of the class is called. 

https://code.tutsplus.com/tutorials/deciphering-magic-methods-in-php--net-13085

----------------------------------------------

ObjectManager

Overview

Large applications, such as the Magento application, use an object manager to avoid boilerplate code when composing objects during instantiation.


Responsibilities

The object manager has the following responsibilities:

	Object creation in factories and proxies.
	Implementing the singleton pattern by returning the same shared instance of a class when requested.
	Dependency management by instantiating the preferred class when a constructor requests its interface.
	Automatically instantiating parameters in class constructors.


Configuration

	The di.xml file configures the object manager and tells it how to handle dependency injection.

	This file specifies the preferred implementation class the object manager generates for the interface declared in a 

	class constructor.

---------------------------------------
---
author: teymur
comments: false
date: 2017-11-11 22:16:08+00:00
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

--------------------------------------

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

## Magento
>Magento is the World’s #1 Commerce Platform
Magento is the leading platform for open commerce innovation. Every year, Magento handles over $100 billion in gross merchandise volume


>Magento is the leading eCommerce platform used for online stores. It is a high-performant, scalable solution with powerful out of the box functionality and a large community built around it that continues to add new features.

CE AND EE
* MAGENTO - (2008)
* MAGENTO 2 - (2015)


---------------------------------------

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



### The di.xml file

#### Overview

The di.xml file configures which dependencies to inject by the object manager.

#### Areas and application entry points

Each module can have a global and area-specific di.xml file. Magento reads all the di.xml configuration files declared in the system and merges them all together by appending all nodes.

As a general rule, the area specific di.xml files should configure dependencies for the presentation layer, and your module’s global di.xml file should configure the remaining dependencies.

Magento loads The configuration in the following stages:

* Initial (app/etc/di.xml)
* Global (<moduleDir>/etc/di.xml)
* Area-specific (<moduleDir>/etc/<area>/di.xml)

#### Examples:

* In index.php, the \Magento\Framework\App\Http class loads the area based on the front-name provided in url.
* In static.php, the \Magento\Framework\App\StaticResource class also loads the area based on the url in the request.
* In cron.php, the \Magento\Framework\App\Cron class always loads the ‘crontab’ area.

### Type configuration

You can configure the type in your di.xml configuration node in the following ways:
``` 
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
    <virtualType name="moduleConfig" type="Magento\Core\Model\Config">
        <arguments>
            <argument name="type" xsi:type="string">system</argument>
        </arguments>
    </virtualType>
    <type name="Magento\Core\Model\App">
        <arguments>
            <argument name="config" xsi:type="object">moduleConfig</argument>
        </arguments>
    </type>
</config>
```
The preceding example declares the following types:

* moduleConfig: A virtual type that extends the type Magento\Core\Model\Config.
* Magento\Core\Model\App: All instances of this type receive an instance of moduleConfig as a dependency.

### Virtual types

A virtual type allows you to change the arguments of a specific injectable dependency and change the behavior of a particular class. This allows you to use a customized class without affecting other classes that have a dependency on the original.

The example creates a virtual type for Magento\Core\Model\Config and specifies system as the constructor argument for type.

### Constructor arguments

You can configure the class constructor arguments in your di.xml in the argument node. The object manager injects these arguments into the class during creation. The name of the argument configured in the XML file must correspond to the name of the parameter in the constructor in the configured class.

The following example creates instances of Magento\Core\Model\Session with the class constructor argument $sessionName set to a value of adminhtml:
``` 
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
    <type name="Magento\Core\Model\Session">
        <arguments>
            <argument name="sessionName" xsi:type="string">adminhtml</argument>
        </arguments>
    </type>
</config>
```

### Abstraction-implementation mappings

The object managers uses the abstraction-implementation mappings when the constructor signature of a class requests an object by its interface. The object manager uses these mappings to determine what the default implementation is for that class for a particular scope.

The preference node specifies the default implementation:
``` 
<!--  File: app/etc/di.xml -->
<config>
    <preference for="Magento\Core\Model\UrlInterface" type="Magento\Core\Model\Url" />
</config>
This mapping is in app/etc/di.xml, so the object manager injects the Magento\Core\Model\Url implementation class wherever there is a request for the Magento\Core\Model\UrlInterface in the global scope.

<!-- File: app/code/core/Magento/Backend/etc/adminhtml/di.xml -->
<config>
    <preference for="Magento\Core\Model\UrlInterface" type="Magento\Backend\Model\Url" />
</config>
```
This mapping is in app/code/core/Magento/Backend/etc/adminhtml/di.xml, so the object manager injects the Magento\Backend\Model\Url implementation class wherever there is a request for the Magento\Core\Model\UrlInterface in the admin area.


### Parameter configuration inheritance
    
Parameters configured for a class type pass on its configuration to its descendant classes. Any descendant can override the parameters configured for its supertype; that is, the parent class or interface:
``` 
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
    <type name="Magento\Framework\View\Element\Context">
        <arguments>
            <argument name="urlBuilder" xsi:type="object">Magento\Core\Model\Url</argument>
        </arguments>
    </type>
    <type name="Magento\Backend\Block\Context">
        <arguments>
            <argument name="urlBuilder" xsi:type="object">Magento\Backend\Model\Url</argument>
        </arguments>
    </type>
</config>
```
``` 
<config xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:ObjectManager/etc/config.xsd">
    <type name="Magento\Filesystem" shared="false">
        <arguments>
            <argument name="adapter" xsi:type="object" shared="false">Magento\Filesystem\Adapter\Local</argument>
        </arguments>
    </type>
</config>
```
-------------------------------------
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


### Factories

Factories are service classes that instantiate non-injectable classes, that is, models that represent a database entity

The following example illustrates the relationship between a simple factory and the ObjectManager:
```
namespace Magento\Framework\App\Config;

class BaseFactory
{
  /**
   * @var \Magento\Framework\ObjectManagerInterface
   */
  private $_objectManager;

  /**
   * @param \Magento\Framework\ObjectManagerInterface $objectManager
   */
  public function __construct(\Magento\Framework\ObjectManagerInterface $objectManager)
  {
    $this->_objectManager = $objectManager;
  }
  /**
   * Create config model
   * @param string|\Magento\Framework\Simplexml\Element $sourceData
   * @return \Magento\Framework\App\Config\Base
   */
  public function create($sourceData = null)
  {
    return $this->_objectManager->create(\Magento\Framework\App\Config\Base::class, ['sourceData' => $sourceData]);
  }
}
```


### Using factories

You can get the singleton instance of a factory for a specific model using dependency injection.

The following example shows a class getting the BlockFactory instance through the constructor:
```

function __construct ( \Magento\Cms\Model\BlockFactory $blockFactory) {
    $this->blockFactory = $blockFactory;
}
```
Calling the create() method on a factory gives you an instance of its specific class:
``` 
$block = $this->blockFactory->create();

// or 

$resultItem = $this->itemFactory->create([
  'title' => $item->getQueryText(),
  'num_results' => $item->getNumResults(),
]);
```
  
### Proxies
  
Magento’s constructor injection pattern enables you to flexibly manage your class dependencies. 
  
If a class’s constructor is particularly resource-intensive, this can lead to unnecessary performance impact when another class depends on it
  
As an example, consider the following two classes:
  ``` 
  class SlowLoading
  {
      public function __construct()
      {
          // ... Do something resource intensive
      }
  
      public function getValue()
      {
          return 'SlowLoading value';
      }
  }
  
  class FastLoading
  {
      protected $slowLoading;
  
      public function __construct(
          SlowLoading $slowLoading
      ){
          $this->slowLoading = slowLoading;
      }
  
      public function getFastValue()
      {
          return 'FastLoading value';
      }
  
      public function getSlowValue()
      {
          return $this->slowLoading->getValue();
      }
  }
  ```
  
  Proxies are generated code
  
  Magento has a solution for this situation: proxies. Proxies extend other classes to become lazy-loaded versions of them. That is, a real instance of the class a proxy extends created only after one of the class’s methods is actually called.
  
  Using the preceding example, a proxy can be passed into the constructor arguments instead of the original class, using DI configuration as follows:
  ``` 
  <type name="FastLoading">
      <arguments>
          <argument name="slowLoading" xsi:type="object">SlowLoading\Proxy</argument>
      </arguments>
  </type>
  ```
  
  With the proxy used in place of SlowLoading, the SlowLoading class will not be instantiated—and therefore, the resource intensive constructor operations not performed—until the SlowLoading object is used (that is, if the getSlowValue method is called).
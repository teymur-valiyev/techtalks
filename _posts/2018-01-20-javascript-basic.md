#JavaScript 

> JavaScript is easy to learn. :))

## JavaScript Data Types

Primitive Data and Complex Data types 

• null
• undefined
• boolean
• number
• string
• object

JavaScript Types are Dynamic.

```
var x;               // Now x is undefined
var x = 5;           // Now x is a Number
var x = "John";      // Now x is a String
```


### Typeof

You can use the JavaScript typeof operator to find the type of a JavaScript variable.

```
typeof {name:'John', age:34} // Returns "object"
typeof [1,2,3,4]             // Returns "object" (not "array", see note below)
typeof null                  // Returns "object"
typeof function myFunc(){}   // Returns "function"

typeof null === "object"; // true
typeof [1,2,3] === "object"; // true
```

Difference Between Undefined and Null
Undefined and null are equal in value but different in type:

```
typeof undefined           // undefined
typeof null                // object

null === undefined         // false
null == undefined          // true
```


### Function are objects
```
typeof function a(){ /* .. */ } === "function"; // true


function a(b,c) {
/* .. */
}

a.length; // 2
```



### undefined Versus “undeclared”

> Many developers will assume “undefined” and “undeclared” are
roughly the same thing, but in JavaScript, they’re quite different.
undefined is a value that a declared variable can hold. “Undeclared”
means a variable has never been declared.

```
var a;
a; // undefined
b; // ReferenceError: b is not defined

if (typeof DEBUG !== "undefined") {
console.log( "Debugging is starting" );
}
```

• null is an empty value.
• undefined is a missing value.
Or:
• undefined hasn’t had a value yet.
• null had a value and doesn’t anymore.

### Array

```
var a = [ 1, "2", [3] ];
a.length; // 3
a[0] === 1; // true
a[2][0] === 3;// true

a[19] = 19;
console.log(a);

```
> Using delete on an array value will remove
that slot from the array , but even if you remove
the final element, it does not update the length
property,

```
var a = [ ];
a["13"] = 42;
a.length; // 14

a["test"] = "test";
a.test
```

```
var a = "foo"

var c = Array.prototype.join.call(a, "-")

Array.prototype.reverse.call(c) // error

c.split("-").reverse().join("-") // split converts string to array
```

### Arithmetic 
```
0.1 + 0.2 === 0.3; // false
0.3 . It’s really close, 0.30000000000000004
```

> “integer” is just a value that has no fractional decimal
value. That is, 42.0 is as much an “integer” as 42 .


### NaN 

NaN literally stands for “not a number,” though this label/description
is very poor and misleading, as we’ll see shortly. It would be much
more accurate to think of NaN as being an “invalid number,” “failed number,” or even “bad number,” than to think of it as “not a num‐
ber.”

For example:
``` 
var a = 2 / "foo"; // NaN
typeof a === "number"; // true
```


------------------------------------------------

In JavaScript, there are no pointers, and references work a bit differ‐
ently. You cannot have a reference from one JS variable to another
variable

```
var a;
var b;
b++;
a = 2; //
b = a; // `b` is always a copy of the value in `a`

var c = [1,2,3];
var d = c; // `d` is a reference to the shared `[1,2,3]` value
d.push( 4 );
c; // [1,2,3,4]
d; // [1,2,3,4]
```

> Simple values (aka scalar primitives) are always assigned/passed by
value-copy: null , undefined , string , number , boolean , and ES6’s
symbol .


> Compound values objects and functions always create a copy of
the reference on assignment or passing.

```
var a = [1,2,3];
var b = a;
a; // [1,2,3]
b; // [1,2,3]
// later
b = [4,5,6];
a; // [1,2,3]
b; // [4,5,6]
```

```
function foo(x) {
	x.push( 4 );
	x; // [1,2,3,4]
	// later
	x.length = 0; // empty existing array in-place
	x.push( 4, 5, 6, 7 );
	x; // [4,5,6,7]
}
var a = [1,2,3];
foo( a );
a; // [4,5,6,7] not [1,2,3,4]
```

```
function foo(x) {
 x = x + 1; // 3
}
var a = 2;
var b = new Number( a ); // or equivalently `Object(a)`
foo( b );
console.log( b ); // 2, not 3
```

> The problem is that the underlying scalar primitive value is not
mutable (same goes for String and Boolean). If a Number object
holds the scalar primitive value 2, that exact Number object can never
be changed to hold another value; you can only create a whole new
Number object with a different value.


### String 
```
var a = new String( "abc" );
typeof a; // "object" ... not "String"
a instanceof String; 
``` 

Internal [[Class]]

```
Object.prototype.toString.call( [1,2,3] );
// "[object Array]"
Object.prototype.toString.call( /regex-literal/i );
// "[object RegExp]"
So, for the array in this example, the internal [[Class]] value is
"Array", and for the regular expression, it’s "RegExp"
```

### Boxing

```
var a = "abc";
a.length; // 3
a.toUpperCase(); // "ABC"

var a = new String( "abc" );
var b = new Number( 42 );
var c = new Boolean( true );
a.valueOf(); // "abc"
b.valueOf(); // 42
c.valueOf(); // true

```


```
var a = new Boolean( false );
if (!a) {
 console.log( "Oops" ); // never runs
}
```


### Natives as Constructors

```
var a = new Array( 1, 2, 3 );
a; // [1, 2, 3]
var b = [1, 2, 3];
b; // [1, 2, 3]
```
> The Array(..) constructor does not require the
new keyword in front of it.

```
var a = new Array( 3 );
var b = [ undefined, undefined, undefined ];
var c = [];
c.length = 3;

var c = [4,5,6,8];
c.length = 2;

c // [4,5]
```

```
var c = new Object();
c.foo = "bar";
c; // { foo: "bar" }

var d = { foo: "bar" };
d; // { foo: "bar" }

var e = new Function( "a", "return a * 2;" );
var f = function(a) { return a * 2; }
function g(a) { return a * 2; }
var h = new RegExp( "^a*b+", "g" );
var i = /^a*b+/g;
```


### Scope
{
}

> javascript only function scope

```
var name = "Jhon";

if(name == "Jhon") {
	var surname = "Doe"
}

console.log(name);
console.log(surname);
```


```
var name = "Jhon";

function foo() {
	if(name == "Jhon") {
		var surname = "Doe";
	}
}

foo();

console.log(surname) // error
```

```
var a = 40;

function myFunc() 
    var b = 1;
    console.log(b);
	c = 50;
    console.log(c);
}

myFunc();
console.log(c);
```


## Object 

```
var user = {
    name: "Jhon",
    say: function (name) { console.log(name); }
};
```


```
var Person = function (name) {
    this.name = name;
};

Person.prototype.say = function (words) {
    alert(this.name + ' says "' + words + '"');
};

var jhon = new Person('Jhon');

console.log(jhon);

jhon.say("Hi");


```

```
function User(name) {
  // this = {};  (implicitly)

  // add properties to this
  this.name = name;
  this.isAdmin = false;

  // return this;  (implicitly)
}

var user  = new User("Jhon");
```

```
let user = {
  name: "John",
  age: 30,
  isAdmin: true
};

for(let key in user) {
  // keys
  alert( key );  // name, age, isAdmin
  // values for the keys
  alert( user[key] ); // John, 30, true
}
```

## Global object
When JavaScript was created, there was an idea of a “global object” that provides all global variables and functions


> https://javascript.info/
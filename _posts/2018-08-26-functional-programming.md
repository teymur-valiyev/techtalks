---
author: teymur
comments: true
date: 2019-04-09 00:00:00+00:00
layout: post
slug: functional-programming
title: Functional Programming
categories: Tutorial
published: false
tags:
- functional-programming
---


## The Lambda Calculus


https://medium.com/@ahlechandre/lambda-calculus-with-javascript-897f7e81f259

An expression may correspond to a variable, an abstraction or a function application

expression = variable || abstraction || application

The expression classes are defined inductively as:

The variable x is an expression by itself.
variable = expression

If x is a variable and E is an expression, then λx.E is an abstraction.
abstraction = λ(variable).(expression)

If E is an expression and A is an expression, then EA is an application.
application = (expression)(expression)


Pure lambda calculus has no built-in functions. Let us evaluate the following expression −
```
(+ (* 5 6) (* 8 3)) 
```
Here, we can’t start with '+' because it only operates on numbers. There are two reducible expressions: (* 5 6) and (* 8 3).

We can reduce either one first. For example −
```
(+ (* 5 6) (* 8 3)) 
(+ 30 (* 8 3)) 
(+ 30 24) 
= 54
```

```
(λx . * 2 x) 4 
(* 2 4) 
= 8
```


```
(λx . (λx . + (− x 1)) x 3) 9 
The inner x belongs to the inner λ and the outer x belongs to the outer one.

(λx . + (− x 1)) 9 3 
+ (− 9 1) 3 
+ 8 3 
= 11
```


```
f(x, y) = x + y
We are accustomed to defining and applying it as follows:

const F = (x, y) => (x + y)
F(5, 10)

```


```
λx (λy.x + y)
const F = x => (y => (x + y))
```


```
const F = x => (y => (x + y))
F(5)(10)
// "x => (y => 5 + y)"
// "x => (y => 5 + 10)"
// 15

```

### Encoding data types

Boolean logic is viewed as an action of choice. Both functions have two parameters and return one; the difference is that True choose the first to return and False choose the second.

```
true = λa. (λb.a)
false = λa. (λb.b)
const True = a => b => a
const False = a => b => b
```

Based on this, the If-then-else structure is represented as:
```
if = λp.(λa. (λb. p a b))
const If = Condition => Then => Else => Condition(Then)(Else)
```

```
const isTrue = () => "it's true!"
const isFalse = () => "it's false!"
Now let’s apply the function If with Booleans:

const First = If(True)(isTrue)(isFalse)
const Second = If(False)(isTrue)(isFalse)
First() // "it's true!"
Second() // "it's false!"
```



Making the reductions is easy to explain the result; note that a in the code is represented by the function Then and b is represented by the function Else:

```
if true = λp.(λa.(λb. p a b)) true = p[p := true] = true a b = λa.(λb.a) a b = a

if false = λp.(λa.(λb. p a b)) false = p[p := false] = false a b = λa.(λb.b) a b = b
```

```
and = λp.(λq. p q p)
or = λp.(λq. p p q)

const And = Exp1 => Exp2 => Exp1(Exp2)(Exp1)
const Or = Exp1 => Exp2 => Exp1(Exp1)(Exp2)

```


Lambda Calculus and functional programming
“Computability via Turing machines gave rise to imperative programming. Computability described via λ-calculus gave rise to functional programming. “- Cooper & Leeuwen (2013)



















-------------------------

```
const I = a => a
```
```
I := λa.a
```


λa.a - lambda abstraction

λ - function sugnifier
a. - parameter variable
a - return expression

### λ  calculus syntax

expression ::= varaible - identifier

expression expression - application
λ variable. expression - abstraction
(expression) -  grouping


#### Variables 
variables cant be changes

#### Application

f a = f(a)

f a b = f(a)(b)

f(a b) = f(a(b))

```
add = a => b => a+b
add(1)(2) // 3
``` 

λa.b  -  a => b
λa.b x - a => b(x)
(λa.b) x - (a=>b)(x)
λa.λb.a -  a => b => a



λx.x

The name after λ is the argument identifier and the expression after point (.) represents the body of the function.
In JavaScript we have:
```
function (x) { 
    return x 
}
x => x

```

λy.y²
```
const Square = y => (y ** 2)
```


EA = E(A)
EA = (λy.y²)(A)
const E = y => (y ** 2)       // Abstraction.
E(A)                          // Application.






λa.λb.λc.b -  a => b => c => b
λabc.b -  a => b => c => b


```
K = a => b => a;

var k7 =K(7);

k7(3); // 7 
```


C :=λfab.fba.
```
C = f => a => b => f(b)(a)
K = a => b => b

C(K)(1)(2) = 2

```




------------------------------------------------------------
http://codekirei.com/posts/currying-with-arrow-functions/

```
const addOneToEach = ar =>
  ar.map(entity => {
    if (typeof entity === 'string') {
      return parseInt(entity) + 1
    }
    return entity + 1
  })

addOneToEach([1, 2, 3])
  // still returns [2, 3, 4]

addOneToEach([1, '2', 3])
  // returns [2, 3, 4] as well, awesome!

```

```
const ensureNum = entity =>
  typeof entity === 'string' ? parseInt(entity) : entity

const addOne = num => num + 1

const addOneToEach = ar =>
  ar.map(ensureNum)
    .map(addOne)
```


#### Curry

```
const sum = function(a, b) {
  return a + b
}

sum(3, 4) // returns 7
```


```
const sum = function(a) {
  return function(b) {
    return a + b
  }
}

sum(3)(4) // returns 7
```

```
// no curry
const sum = (a, b) => a + b

// curry
const sum = a => b => a + b
```


```
const ensureNum = entity =>
  typeof entity === 'string' ? parseInt(entity) : entity

const addNums = (a, b) => a + b

const incrementEach = (ar, by) =>
  ar.map(ensureNum)
    .map(num => addNums(num, by))
```

```
const ensureNum = entity =>
  typeof entity === 'string' ? parseInt(entity) : entity

const addNums = a => b => a + b

const incrementEach = (ar, by) =>
  ar.map(ensureNum)
    .map(addNums(by))
```





### Church arithmetic


One

N1 := λfa.fa - takes function and argument and applies function argument

Two

N1 := λfa.f(fa)

```
twice = f => a => f(f(a))
```
```
jsnum = n => n(x => x+1)(0);
jsnum(once) // 1
```

```
zero = f => a => a
once = f => a => f(a)
twice = f => a => f(f(a))

succ = n => f => a => f(n(f)(a));
```
```
succ(twice)(x => x+1)(1) // 4
```

### Bluebird combinator

> λfga.f(ga) 
B = f => g => a => f(g(a));

```
B(jsnum)(succ)(twice);
```

### Vireo

> λabf.fab

```
V =  a => b => f => f(a)(b)`
``` 

### Loop

> (λx.xx)(λx.xx)
λx - input x calc x with argument x


### Y Combinator 
rec 
> λf.(λx.f(xx))(λx.f(xx))

---
author: teymur
comments: true
date: 2019-04-09 00:00:00+00:00
layout: post
slug: c-cpp
title: C pointer and references
categories: Tutorial
published: false
tags:
- c
- c++
---

### c pointer and references

pointer 
``` 
char c = 'z'

char* p = &c;

p is adress of c 
*p is value of c 
```

reference

char& r = c;

no memeory is used to store r 
r is alias for c 
when we refer r we refer to c
r and c is one
reference must initialize and it cannon re-inintialze 

const char& r = c // const references same as reference but immutable
r = 'y' // error
c = 'y' // okey and same r == 'y' true


In assembly language, variable names represent addresses, not data!

EatMsg: db "Eat at Joe's!"
mov ecx,EatMsg

NASM provides various define directives for reserving storage space for variables. The define assembler directive is used for allocation of storage space. It can be used to reserve as well as initialize one or more bytes.

Directiv | Purpose| Storage Space
--- | --- | --- 
DB | Define Byte | allocates 1 byte
DW | Define Word | allocates 2 bytes
DD | Define Doubleword | allocates 4 bytes
DQ | Define Quadword | allocates 8 bytes
DT | Define Ten Bytes | allocates 10 bytes

choice		DB	'y'

Each byte of character is stored as its ASCII value in hexadecimal.

### c++ pointer and references

Pointer Variables
A computer memory location has an address and holds a content.

The address is a numerical number (often expressed in hexadecimal), which is hard for programmers to use directly. Typically, each address location holds 8-bit (i.e., 1-byte) of data. It is entirely up to the programmer to interpret the meaning of the data, such as integer, real number, characters or strings.



A variable is a named location that can store a value of a particular type. Instead of numerical addresses, names (or identifiers) are attached to certain addresses. Also, types (such as int, double, char) are associated with the contents for ease of interpretation of data.


Each address location typically hold 8-bit (i.e., 1-byte) of data. A 4-byte int value occupies 4 memory locations. A 32-bit system typically uses 32-bit addresses. To store a 32-bit address, 4 memory locations are required.

```
int *p1, *p2, i;    // p1 and p2 are int pointers. i is an int
int* p1, p2, i;     // p1 is a int pointer, p2 and i are int
int * p1, * p2, i;  // p1 and p2 are int pointers, i is an int
```

The address-of operator (&) operates on a variable, and returns the address of the variable. For example, if number is an int variable, &number returns the address of the variable number.


The indirection operator (or dereferencing operator) (*) operates on a pointer

int * iPtr;
*iPtr = 55;
cout << *iPtr << endl;
The pointer iPtr was declared without initialization, i.e., it is pointing to "somewhere" which is of course an invalid memory location. The *iPtr = 55 corrupts the value of "somewhere"! You need to initialize a pointer by assigning it a valid address. Most of the compilers does not signal an error or a warning for uninitialized pointer?!


Reference Variables

C++ added the so-called reference variables (or references in short). A reference is an alias, or an alternate name to an existing variable. For example, suppose you make peter a reference (alias) to paul, you can refer to the person as either peter or paul.

C++ assigns an additional meaning to & in declaration to declare a reference variable.
The meaning of symbol & is different in an expression and in a declaration.


```
type &newName = existingName;
// or
type& newName = existingName;
// or
type & newName = existingName;
```

A reference works as a pointer. A reference is declared as an alias of a variable. It stores the address of the variable, as illustrated:


Reference is closely related to pointer. In many cases, it can be used as an alternative to pointer. A reference allows you to manipulate an object using pointer, but without the pointer syntax of referencing and dereferencing.

```
/* Passing back return value using reference (TestPassByReferenceReturn.cpp) */
#include <iostream>
using namespace std;
 
int & squareRef(int &);
int * squarePtr(int *);
 
int main() {
   int number1 = 8;
   cout <<  "In main() &number1: " << &number1 << endl;  // 0x22ff14
   int & result = squareRef(number1);
   cout <<  "In main() &result: " << &result << endl;  // 0x22ff14
   cout << result << endl;   // 64
   cout << number1 << endl;  // 64
 
   int number2 = 9;
   cout <<  "In main() &number2: " << &number2 << endl;  // 0x22ff10
   int * pResult = squarePtr(&number2);
   cout <<  "In main() pResult: " << pResult << endl;  // 0x22ff10
   cout << *pResult << endl;   // 81
   cout << number2 << endl;    // 81
}
 
int & squareRef(int & rNumber) {
   cout <<  "In squareRef(): " << &rNumber << endl;  // 0x22ff14
   rNumber *= rNumber;
   return rNumber;
}
 
int * squarePtr(int * pNumber) {
   cout <<  "In squarePtr(): " << pNumber << endl;  // 0x22ff10
   *pNumber *= *pNumber;
   return pNumber;
}

```

You should not pass Function's local variable as return value by reference

Dynamic Memory Allocation
allocating dynamicaly at runtime

```
// Static allocation
int number = 88;
int * p1 = &number;  // Assign a "valid" address into pointer
 
// Dynamic Allocation
int * p2;            // Not initialize, points to somewhere which is invalid
cout << p2 << endl; // Print address before allocation
p2 = new int;       // Dynamically allocate an int and assign its address to pointer
                    // The pointer gets a valid address with memory allocated
*p2 = 99;
cout << p2 << endl;  // Print address after allocation
cout << *p2 << endl; // Print value point-to
delete p2;           // Remove the dynamically allocated storage
```


new and delete operators work on pointer.

The main differences between static allocation and dynamic allocations are:

1. In static allocation, the compiler allocates and deallocates the storage automatically, and handle memory management. Whereas in dynamic allocation, you, as the programmer, handle the memory allocation and deallocation yourself (via new and delete operators). You have full control on the pointer addresses and their contents, as well as memory management.

2. Static allocated entities are manipulated through named variables. Dynamic allocated entities are handled through pointers.


Dynamic array is allocated at runtime rather than compile-time, via the new[] operator. 

```

int* arr = new int[5];

for (int i = 0; i< 5; i++) {
	*(arr + i) = i;
}

delete[] arr;
```


Array is Treated as Pointer

In C/C++, an array's name is a pointer, pointing to the first element (index 0) of the array.

```
int nubmers[5] = {11,12,13,14,15};

cout << &numbers[0] << endl; // Print address of first element (0x22fef8)
cout << numbers << endl;     // Same as above (0x22fef8)
cout << *numbers << endl;         // Same as numbers[0] (11)
cout << *(numbers + 1) << endl;   // Same as numbers[1] (22)
cout << *(numbers + 4) << endl;   // Same as numbers[4] (41)

```

Pointer Arithmetic

```
int numbers[] = {11, 22, 33};
int * iPtr = numbers;
cout << iPtr << endl;        // 0x22cd30
cout << iPtr + 1 << endl;    // 0x22cd34 (increase by 4 - sizeof int)
cout << *iPtr << endl;       // 11
cout << *(iPtr + 1) << endl; // 22 
cout << *iPtr + 1 << endl;   // 12
```


The operation sizeof(arrayName) returns the total bytes of the array. You can derive the length (size) of the array by dividing it with the size of an element (e.g. element 0). For example,

int numbers[100];
cout << sizeof(numbers) << endl;     // Size of entire array in bytes (400)
cout << sizeof(numbers[0]) << endl;  // Size of first element of the array in bytes (4)
cout << "Array size is " << sizeof(numbers) / sizeof(numbers[0]) << endl;  // (100)


An array is passed into a function as a pointer to the first element of the array


the following declarations are equivalent:
```
int max(int numbers[], int size);
int max(int *numbers, int size);
int max(int number[50], int size);
```


#### C-String and Pointer


c string is a character array, terminated with a null character '\0'

```
char msg1[] = "Hello";
char *msg2 = "Hello";
  // warning: deprecated conversion from string constant to 'char*'

cout << strlen(msg1) << endl;    // 5
cout << strlen(msg2) << endl;
cout << strlen("Hello") << endl;

int size = sizeof(msg1)/sizeof(char);
cout << size << endl;  // 6 - including the terminating '\0'
for (int i = 0; msg1[i] != '\0'; ++i) {
  cout << msg1[i];
}
cout << endl;

for (char *p = msg1; *p != '\0'; ++p) {
      // *p != '\0' is the same as *p != 0, is the same as *p
  cout << *p;
}
```


#### Function pointer 
In C/C++, functions, like all data items, have an address. The name of a function is the starting address where the function resides in the memory, and therefore, can be treated as a pointer. We can pass a function pointer into function as well.

```
// Function-pointer declaration
return-type (* function-ptr-name) (parameter-list)
 
// Examples
double (*fp)(int, int)  // fp points to a function that takes two ints and returns a double (function-pointer)
double *dp;             // dp points to a double (double-pointer)
double *fun(int, int)   // fun is a function that takes two ints and returns a double-pointer

double f(int, int);      // f is a function that takes two ints and returns a double
fp = f;   
```

```
/* Test Function Pointers (TestFunctionPointer.cpp) */
#include <iostream>
using namespace std;
 
int arithmetic(int, int, int (*)(int, int));
    // Take 3 arguments, 2 int's and a function pointer
    //   int (*)(int, int), which takes two int's and return an int
int add(int, int);
int sub(int, int);
 
int add(int n1, int n2) { return n1 + n2; }
int sub(int n1, int n2) { return n1 - n2; }
 
int arithmetic(int n1, int n2, int (*operation) (int, int)) {
   return (*operation)(n1, n2);
}
 
int main() {
   int number1 = 5, number2 = 6;
 
   // add
   cout << arithmetic(number1, number2, add) << endl;
   // subtract
   cout << arithmetic(number1, number2, sub) << endl;
}
```



https://www.ntu.edu.sg/home/ehchua/programming/cpp/cp4_PointerReference.html


#### Reference counting

Destroy an object when it will no longer be used.


Instead of connecting your program to an external database, it is often
more practical to make your data structures (or framework) persistent and
use them as a fast internal database.


Screenshot from 2018-05-28 15-10-31.png

```
class Faculty {
Collection<Department> depts; // R1
HashTable<Student> students; // R4
};
class Department {
Collection<Lecturer> lecturers; // R2
};
class Lecturer {
Collection<Course> courses; // R3
};
class Course {
Lecturer *taughtBy; // R3
Collection<Attends> atts; // R5
};
class Student {
Collection<Attends> atts; // R5
};
class Attends {
Course *toCourse;
// R5
Student *toStudent; // R5
int mark;
int attendance;
};
int main(int argc,char *v[]){ // call with c to create,with o to open
Faculty *f;
if(argv[1][0]==’c’){
f=new Faculty;
d=new Department;
f->depts.add(d);
.. generate initial data
}
if(argv[1][0]==’o’){
f=utility.open(“facultyFile”);
}
.. add, remove, modify data
utility.save(“facultyFile”,f);
return 0;
}
```
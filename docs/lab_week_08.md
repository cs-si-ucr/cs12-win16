Lab Week 8: Recursion
=====================

Read your book to learn about recursion.


Exercise 1
----------
Write a function to return the nth fibonacci number recursively.

```c++
/// Our fibonacci sequence is zero-indexed
// 0 is first fibonacci number (argument is 0)
// 1 is second fibonacci number (argument is 1)
// 1 is third fibonacci number (argument is 2)
// 2 is fourth fibonacci number (argument is 3)
// 3 is fifth fibonacci number (argument is 4)
// 5 is sixth fibonacci number (argument is 5)
// 8 is seventh fibonacci number (argument is 6)
// and so on...

// returns the nth fibonacci number
int fib(unsigned int);
```


Exercise 2
----------
Write a function to print to collatz conjecture sequence recursively.

Remember that the collatz conjecture is defined in this way:

Take any number.
If it's even, divide it by two.
If it's odd, multiply it by 3, then add 1.
Eventually, you will end up with the value of 1.

There is no known number that will not eventually end up at 1.

```c++
// prints the collatz sequence defined by the argument
void collatz(unsigned int);
```


Exercise 3
----------
Write a multiplication function recursively.

```c++
// returns the product of the two arguments
int mul(int, int);
```


Exercise 4
----------
Write ``pow`` recursively.

``pow`` exponentiates a given value.
Google ``cmath pow`` for more information.

```c++
// returns the exponentiation of the first argument to the second argument
double pow(double base, unsigned int exponent);
```


Exercise 5
----------
Write a function to print a cstring.

```c++
// prints a cstring
void printForward(const char*);
```


Exercise 6
----------
Write a function to print a cstring backwards.

```c++
// prints a cstring backwards
void printBackward(const char*);
```


Exercise 7
----------
Write ``strlen`` recursively.

```c++
// returns the length of the argument
unsigned int myStrlen(const char*);
```

Exercise 8
----------
Write ``strcpy`` recursively.

```c++
// copies the second cstring to the first cstring
void myStrcpy(char*, const char*);
```


Exercise 9
----------
Write ``min`` recursively.

```c++
// returns the index of the smallest element in an array of integers
// first parameter is the array
// second parameter is the size of the array
unsigned int min(int*, unsigned int);
```


Exercise 10
----------
Write ``strcmp`` recursively.

```c++
// compares the first string to the second, lexicographically
// -1: argument1 < argument2
//  0: argument1 = argument2
//  1: argument1 > argument2
int myStrcmp(const char*, const char*);
```




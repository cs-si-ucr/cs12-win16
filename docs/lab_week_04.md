Lab 4: Classes, Syntactical Sugar, Compilation, and Makefiles
================

This
----

```c++
class Foo {
    public:
        Foo() {
            this->a = 0;
            this->b = 0;
        }
        Foo(int a, int b) {
            // now, which "a" does "a" refer to?
            /* this doesn't work for obvious reasons:
            a = a;
            b = b;
            */
            // using "this" helps us clear the confusion up
            this->a = a; // a is the parameter
            this->b = b; // b is the parameter
        }
    private:
        int a, b;
};
```

The keyword ``this`` is used to access the implicit parameter's fields.
To use access fields of the implicit parameter, use the arrow operator (``->``).

Overloading
---------

<a href="https://en.wikipedia.org/wiki/Operators_in_C_and_C%2B%2B" target="_blank">This</a> article contains a list of all C++ operators and whether or not they are able to be overloaded.
Operators can be overloaded as part of a class, or outside of class definitions.
When overloading as part of a class, the object referred to by ``this`` is assumed to be the first parameter of the operator being overloaded.
Also, the overloaded operator can operate on and with private data and private member functions.

Operators overloaded globally must specify all parameters to the operator in question.
Because they are defined outside of the class, they cannot access private data or private member functions unless the operator is made to be a ``friend``.


Classes Within Classes
----------------------
<a href="https://zybooks.zyante.com/#/zybook/UCRCS12Winter2016/chapter/9/section/17" target="_blank">Chapter 9 section 17 in your book</a> talks about using classes within classes.
Nothing special is happening here;
once a class is created, it can be used just about anywhere.

```c++
class A {
    private:
        int x, y;
    public:
        A(int x, int y) : x(x), y(y) {}
        void setX(int x) { this->x = x; }
        void setY(int y) { this->y = y; }
        int  getX()      { return x; }
        int  getY()      { return y; }
};

class B {  // contains instances of A
    private:
        A pv1, pv2;
};
```

Preprocessor Directives
-----------
Preprocessor directives are very powerful tools that a programmer can use to make code more quickly.
All preprocessor directives start with the <a href="http://www.merriam-webster.com/dictionary/octothorpe" target="_blank">octothorpe</a> (``#``).

```c++
#include <filename.h>
#include "filename.h"
```
The ``#include`` directive finds a file specified, and places its contents where the ``#include`` statement was located.
When the filename is surrounded with angle brackets (``<>``), the preprocessor will look in standard library locations for your file.
When the filename is surrounded with quotation marks (``""``), the preprocessor will look for the file in the same directory as the file you're trying to compile.


Separate Files
--------------





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
When programs become very large, it is a good idea to split them up into smaller logical units so they are easier to maintain.
There is a way to do this that also has the added benefit of allowing for separate compilation;
instead of compiling every part of your program every time you want to build an executable, you can instead separate the code in such a way that only parts you change need to be recompiled.

```c++
/* main.cpp */

#include <iostream>

class Foo { // class declaration
    public:
        Foo();        // default constructor
        void hello(); // some function
        // stuff
        // ...
    private:
        // stuff
        // ...
};

// class definition
Foo::Foo() {}

void Foo::hello() {
    std::cout << "hello world" << std::endl;
}

int main() {
    Foo a;
    a.hello();
}
```

Let's say we're working with the single file ``main.cpp`` above.
How would we break it up?
Start by taking out the class and putting it in another file.
We'll call it ``foo.cpp``.

```c++
/* foo.cpp */

#include <iostream>

class Foo { // class declaration
    public:
        Foo();        // default constructor
        void hello(); // some function
        // stuff
        // ...
    private:
        // stuff
        // ...
};

// class definition
Foo::Foo() {}

void Foo::hello() {
    std::cout << "hello world" << std::endl;
}
```

```c++
/* main.cpp */

#include "foo.cpp"

int main() {
    Foo a;
    a.hello();
}
```

Notice that ``main.cpp`` doesn't actually use anything from ``iostream``, so it is not necessary to include it there.
This is a good first step.
We have logically separated all of the parts of our simple program.
Generally, each class will have its own file(s) containing all the code associated with it.

What about the separate compilation I promised?
If you understand preprocessor directives, you can tell that we're basically ending up with our original ``main.cpp``, just using extra steps.
Let's fix that:

```c++
/* foo.h */

#include <iostream>

class Foo { // class declaration
    public:
        Foo();        // default constructor
        void hello(); // some function
        // stuff
        // ...
    private:
        // stuff
        // ...
};
```

```c++
/* foo.cpp */

#include "foo.h"

// class definition
Foo::Foo() {}

void Foo::hello() {
    std::cout << "hello world" << std::endl;
}
```

```c++
/* main.cpp */

#include "foo.h"

int main() {
    Foo a;
    a.hello();
}
```

Wow!
Three files!!
Now, we can perform separate compilation.
Previously, ``g++ main.cpp`` would have done the trick for us.
Now, that won't work.
Instead, we compile like this:

```sh
g++ -c foo.cpp
g++ -c main.cpp
g++ foo.o main.o
```

Alternatively, you could compile like this:

```sh
g++ -c foo.cpp
g++ main.cpp foo.o
```

Remember how we are allowed to use prototypes for compilation, and give actual function definitions at a later point?
This is because there are actually two steps to building an executable.
The first is the compilation step.
All the code you write gets turned into machine language.
Next is the linking step.
All the functions you used get "linked" into your executable.
You don't need to know the details of linking, but basically during compilation, a placeholder is put in for each function call, which is then filled in with an actual, correct value later.

Knowing this, let's explore what's happening in the code above.
When we attempt to compile ``foo.cpp``, ``foo.cpp`` brings in ``foo.h``.
No reason to type anything twice, so we keep the class declaration in one spot, and that's usually the header file (ending in ``.h``).
There's no ``main`` function, but this is okay because we're only compiling for now.
We tell the compiler to only compile by sending the ``-c`` flag.

Next, we attempt to compile ``main.cpp``.
The only thing ``main.cpp`` needs to know to be compiled are the prototypes of ``Foo``, and nothing else!
We're not linking yet, so we don't need the definitions.

Lastly, we link everything together.
When compiling, we get *object code*.
The file generated usually has the same name as the file compiled, but with a ``.o`` exstension instead of the original ``.cpp``.

In the first compilation example, I created two object files, ``main.o`` and ``foo.o``, and linked them together.
In the second compilation example, I created one object file, ``foo.o``, and then compiled and linked ``main.cpp`` in a single step.
Either way works, and is a matter of style.
The former is usually more preferable, because it's easier to remember;
just do the exact same thing for all files, then link everything together!
Both allow for separate compilation.

But what does separate compilation mean, exactly?
If I were to change ``main.cpp`` to the following:

```c++
/* main.cpp */

#include "foo.h"

int main() {
    Foo a, b;
    a.hello();
    b.hello();
}
```

The only thing I would need to do to recompile is the following:

```sh
g++ -c main.cpp
g++ main.o foo.o
```

Notice how I did **not** recompile ``foo.cpp``!
The old *definitions* for ``Foo`` are still in ``foo.o``, so I can still use it (assuming you didn't delete it).
Now imagine if you have many large classes included in your project.
Compiling the entire project every time you wanted to run it could be a time-consuming process.
It may take sever minutes to several hours, for larger projects.
A solution to this problem is separate compilation;
organize your files in such a way that you don't need to compile everything every time.

NOTE: This doesn't mean you don't have to compile anything.
You still need to compile everything you *change*.
If you change how ``Foo`` works, or add a function, you need to recompile and relink everything you change.





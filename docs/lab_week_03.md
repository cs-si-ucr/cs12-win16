Lab 3: Structs and Classes
===================================
Structs
-------

Structs are a way to create new datatypes that are combinations of smaller datatypes.

Here's the syntax for creating a struct:

```c++
struct StructName {
    Type1 field1;
    Type2 field2;
    // ...
};  // <-- Notice this semicolon
```

After this point, there now exists a new type - a struct - called ``StructName``, and it can be used like so:

```c++
StructName myStruct;
myStruct.field1;     // expression of type Type1
myStruct.field2;     // expression of type Type2
```

Structs define different fields.
Each field gets its own type.
When using the struct, each field is available through the dot operator.

Now, you can use your new type like you would any other type.

```c++
/* in containers */
vector<StructName> v(20);        // a vector of StructName with a size of 20

/* functions */
void f1(StructName arg1);        // accepts StructName by value
void f1(StructName& arg1);       // accepts StructName by reference
void f1(const StructName& arg1); // accepts StructName by const reference

StructName f2();                 // returns StructName
```

Classes
-------

Classes are very similar to structs in that they can hold their own data.
Unlike structs however, they can also hold contain their own methods.


```c++
class MyClass {
    public:
        Type1 publicData;
        Type2 f1();
    private:
        Type3 privateData;
        Type4 f2();
};
```

First, you should notice the ``public`` and ``private`` keywords.
This is one of the big differences between structs and classes.
In a struct, all members are public.
This can't be changed.
In a class, the programmer decides whether each element is ``public`` or ``private``.
``private`` members can't be accessed with the dot operator.

```c++
MyClass obj;
obj.publicData;  // this is allowed
obj.privateData; // this isn't allowed
```

Another difference is the concept of member functions.
You've already been using member functions.
Some examples include ``.size()``, ``.at(int)``, and ``.find(...)``.

Now, combine your knowledge of member function usage and ``public`` and ``private`` permissions, and it's easy to see how to use member functions:

```c++
MyClass obj;
obj.f1(); // allowed because it's public
obj.f2(); // not allowed because it's private
```

Notice that the parentheses mean that the member is a function, not just data.

An important thing you will need to learn now is "encapsulation."
Think about cars for a moment.
To drive a car well, you don't need to know how the engine works.
You don't need to keep track of every little piece;
instead you just focus on the steering wheel and pressing the pedals.
Similarly for classes, the users of your class shouldn't have access to the internal details.
They might mess something up!
Instead, you provide a clean interface that abstracts the details away.
Refer to your book on how to do this.


Accessors, Mutators, and Private Helper Functions
-------------------------------------------------
```c++
class MyClass {
    private:
        Type data;
        void helper();

    public:
        void accessor(int x) const; // this function can't change any private data
        void mutator(int x);        // this function can change private data
};
```

Mutators aren't **required** to change data;
they only have the ability to.
Accessors that change private data will cause compiler errors.

Class functions declared ``private`` are known as "helper functions".
This is due to the fact that they can only be called from within the class's own member functions.

```c++
MyClass obj;
obj.helper();  // not allowed
obj.mutator(); // mutator is allowed to call helper
```

NOTE: functions declared as const (accessors) aren't allowed to ever call a non-const function (mutator).

Constructors
------------
```c++
class MyClass {
    public:
        MyClass();      // notice: NO return type
        MyClass(int x); // also, it can be overloaded to accept different parameters
};
```

Constructors exist to allow you to start your class at a known state.
They have **no** return type.
When an object of your class is created, the constructor is called.
If you don't write a constructor for your class, a default constructor will be used.

Bonus
-----
If you want to learn a cool trick that will make coding easier in the future, look up [initialization lists](http://lmgtfy.com/?q=c%2B%2B+initialization+lists)



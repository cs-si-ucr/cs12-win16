Lab 1: Templates
================
You may remember (or should remember) from CS12 a data structure
that is formed by connecting a group of nodes called a "Linked List".

In order to implement a Linked List, you must define the structure
for an individual node. 

For a singly-linked list of integers, it may look something like:
```cpp
struct IntNode{
    int val;
    IntNode * next;
};
```
In order to implement the Linked List, we store the head of the list,
which is a pointer to a `IntNode`. We also implement methods that
insert/remove elements from the list
e.g.
```cpp
class IntLinkedList {
    public:
        void push_front(int val);
        // ...
    private:
        IntNode * head;
};
```

That's all fine and dandy, but if instead want a `DoubleList` or a
`StringList`, then we are in trouble. 

A common first instinct is to copy-and-paste code manually 
and change the types where needed. But even expert programmers 
start to [make mistakes](http://www.viva64.com/en/b/0260/print/)
copy and pasting.

Introducing templates!
---------------------
The solution for this problem is function-templates and class-templates which in a way generate this "copy-and-paste" code for you.

In fact, you've already been using templates all-along. The standard
library container, vector, which makes dynamic arrays easy to use is
also one of these template classes.

To create an instance of a template class is simple, just provide the
desired type in the "angle-brackets".

```cpp
vector<int> numbers; // creates a vector of integers
vector<string> words; // creates a vector of strings
```

To create a new class template, before our class declaration we use the keyword `template` followed by a type parameter inside "angle-brackets"
e.g. `template<typename T>`. The keyword `typename` tells the compiler
that `T` is a placeholder for an actual type. 

*Note: `T` is a common name for a placeholder type, this name like parameter names should be a tell for how the class is used - e.g. a common typename for classes that take in any container such as Vectors or Lists is `Container`*

Let's say, we want to create a templated version of our Node and List.

`IntNode` becomes:
```cpp
template<typename T>
struct Node {
   T val;
   Node<T> * next;
};
```

and `IntLinkedList` becomes:
```cpp
template<typename T>
class LinkedList {
    public:
        void push_front(T val);
        // ...
    private:
        Node<T> * head;
};
```
To create a `LinkedList` of doubles, we declare the list as so:

```cpp
LinkedList<double> list;
```

In order to template functions and method, we do something similar.

For example, if we want to define the templated LinkedList's
`push_front` method:

```cpp
template<typename T>
LinkedList<T>::push_front(T val) {
    Node * new_node = new Node<T>();
    new_node -> val = val;

    Node * old_head = this -> head;
    new_node -> next = old_head;
    this -> head = new_node;
}
```

For more info on templates check out [this FAQ](https://isocpp.org/wiki/faq/templates#overview-templates)!

Exercises
---------
Implement a vector class template. You should have an implementation of IntVector from CS12 that makes this much easier! 

**Pro-Tip: before implementing the class as a class template, `typedef` the type `T` as an integer and replace type with `T` as needed.**
e.g.
```cpp
typedef int T; // give the int an alias which is T
T my_int = 42;
```

**This give you much nicer error messages and makes it easier to debug.**

Example Usage, should implement at least the following methods:
```cpp
MyVector<string> vec;
vec.push_back("CS14");
vec.push_back("World");
vec.insert("Hello", 0); 
cout << vec.front() << endl; // "Hello"
cout << vec.back() << endl; // "World"
vec.pop_back();
cout << vec.back() << endl; // "CS14"
vec.pop_back();
cout << vec.back() << endl; // "Hello"

MyVector<int> another_vec;
another_vec.push_back(42);
```
Stretch-goal exercise:
---------------------
Rewrite your IntList as a class template!


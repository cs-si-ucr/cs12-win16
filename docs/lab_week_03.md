Lab 3: Stacks and Queues
===================================
Stacks
------

Stacks are LIFO (last in, first out) data structures.
You've already encountered stacks before.
Recursion takes advantage of the function call stack.

Here's a small demo of how stacks work:
```cpp
#include <iostream>
#include <stack>

using namespace std;

int main() {
  stack<int> s;
  for(unsigned i = 0; i < 6; ++i) {
    cout << "Pushing i (" << i << ")" << endl;
    s.push(i);
  }

  while (!s.empty()) {
    cout << "Popping (" << s.top() << ")" << endl;
    s.pop();
  }
  
  if (s.empty()) cout << "stack is empty" << endl;

  return 0;
}
```

Try running that and see what is output.
Go ahead. I'll wait.

Were you surprised by the output?

Queues
------

Queues are FIFO (first in, first out) data structures.
They're structured similarly to checkout lines at the grocery store;
Whoever gets in line first gets serviced first.

Here's a small demo of how queues work:

```cpp
#include <iostream>
#include <queue>

using namespace std;

int main() {
  queue<int> q;
  for(unsigned i = 0; i < 6; ++i) {
    cout << "Pushing i (" << i << ")" << endl;
    q.push(i);
  }

  while (!q.empty()) {
    cout << "Popping (" << q.front() << ")" << endl;
    q.pop();
  }
  
  if (q.empty()) cout << "queue is empty" << endl;

  return 0;
}
```

Run it!!

Exercise 1
----------
Implement your own ``stack`` and ``queue``!

The ``stack`` should have the following public members:
```cpp
template <typename T>
class myStack {
  public:
    void push(T);       // adds an element to the top of the stack
    T top() const;      // gets the element at the top of the stack
    bool pop();         // returns false if failed
    bool empty() const; // returned true if empty
};
```

The ``queue`` should have the following public members:
```cpp
template <typename T>
class myQueue {
  public:
    void push(T);       // adds an element to the back of the queue
    T front() const;    // gets the element at the front of the queue
    bool pop();         // returns false if failed
    bool empty() const; // returned true if empty
};
```

**Important**: Use a ``deque``, ``list``, or ``vector`` to do all of the heavy lifting for you.
In other words, if you're using arrays and nodes to solve this, you're doing too much work.

Exercise 2
----------
You're all probably able to recite the recursive factorial function in your sleep:
```cpp
unsigned long fact(unsigned long n) {
  if (n < 2) return 1;
  return n * fact(n - 1);
}
```
Write a non-recursive factorial function that takes advantage of ``stack`` similarly to how recursion works.

Stretch-goal Exercise 1
-----------------------
Make a ``queue`` using two stacks!

Stretch-goal Exercise 2
-----------------------
Make a new class ``minStack`` that has the same efficiency as a ``stack`` for ``push`` and ``pop``, as well as constant lookup for the minimum element in the stack.

In other words, I should be able to do this all in constant time:

```cpp
int main() {
  minStack<int> ms;
  ms.push(3);
  cout << "min: " << ms.min() << "(pushed " << ms.top() << ")" << endl;
  ms.push(1);
  cout << "min: " << ms.min() << "(pushed " << ms.top() << ")" << endl;
  ms.push(4);
  cout << "min: " << ms.min() << "(pushed " << ms.top() << ")" << endl;
  ms.push(1);
  cout << "min: " << ms.min() << "(pushed " << ms.top() << ")" << endl;
  ms.push(5);
  cout << "min: " << ms.min() << "(pushed " << ms.top() << ")" << endl;
  ms.push(9);
  cout << "min: " << ms.min() << "(pushed " << ms.top() << ")" << endl;
  ms.push(2);
  cout << "min: " << ms.min() << "(pushed " << ms.top() << ")" << endl;
  ms.push(6);
  cout << "min: " << ms.min() << "(pushed " << ms.top() << ")" << endl;

  while (!ms.empty()) {
    int temp = ms.top();
    ms.pop();
    cout << "min: " << ms.min() << "(popped " << temp << ")" << endl;
  }

  return 0;
}
```

Prototype:
```cpp
template <typename T>
class minStack() {
  public:
    void push(T);       // adds an element to the top of the stack
    T top() const;      // gets the element at the top of the stack
    T min() const;      // gets minimum element
    bool pop();         // returns false if failed
    bool empty() const; // returned true if empty
}
```
(Hint: you can use whatever internal data type you'd like)

(**Hint:** use two stacks)



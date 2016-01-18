Lab 4: Binary Search Trees (BST)
================

What's a tree?
--------------
Trees are often easier to deal with recursively (or if you're a mathematician, 'inductively').
Thus, to define a tree recursively, we can say that:

1. A Tree is a system of nodes
	* A node consists of a value and pointers to its children
2. Every node has a unique parent
	* No node has more than one parent
3. The **Root** of a tree has no parent
4. A Node can have any number of children (including 0)

When we put all of these things together, we end up with something looking like:

<img src="http://upload.wikimedia.org/wikipedia/commons/thumb/f/f7/Binary_tree.svg/220px-Binary_tree.svg.png" alt="It's a Tree!" style="width: 250px;"/>

Where the numbers in the nodes represent the value at that node, and the arrows represent pointers to children nodes.

What's a BST?
-------------
A Binary Search Tree is exactly like any other tree, except every node has **exactly** two children (if there is no child, the node will be a null pointer).
Furtermore (and more importantly), every child to the left of a node will be less than the node, while every child to the right will be greater.

You'll notice that the picture above is **NOT** a BST. Even though each node has two children (we can pretend that there are invisible null children), if we go to the left child of our root, we find a value that is *greater*, breaking our definition.

**This** would be a valid Binary Search Tree:

<img src="http://upload.wikimedia.org/wikipedia/commons/thumb/d/da/Binary_search_tree.svg/2000px-Binary_search_tree.svg.png" alt="It's a BST!" style="width: 250px;"/>

Notice how **every** number to the left of any node (take 8 for example), is less than the node itself (1, 3, 4, 5, 7). Since this is the case, where will the smallest node be? What about the largest?

Put it into practice!
---------------------
We have created a [simple implementation of a BST](https://gist.github.com/scohe001/65ae445a6577cb85b22c) for you to use. The class comes with the member functions `void push(T val)` to add values to the tree, and `void print()` to print a rough representation of the tree.


######NOTE:
*It is often almost always easier to write Tree functions recursively (as you'll see the push function has been written). However, it **is** possible to do all of the following exercises without recursion--you'll just need to be iterating over a stack you're constantly pushing and popping to (as you'll see the print function is doing).*

Exercise 1
----------
Add `min` and `max` funcitons to the `Tree` class to return the minimum and maxiumum values stored.

*(If there are no values in the tree, return the class default, `T()`)*

Exercise 2
----------
Add a `find` function to the `Tree` class that will find a value in the tree and return a Node pointer. If the value is not found, return the null pointer.

Exercise 3
----------
Add a `total` function to the `Tree` class that will return the total of all of the items in the tree (`x1 + x2 + ... + xn`).

Exercise 4
----------
Add `print_ascending` and `print_descending` functions to the `Tree` class that will print all of the values in the tree in ascending and descending order on one line seperated by spaces.

*(Notice how it didn't matter what order you 'visited' the nodes to find the total. Make sure you have your order correct here!)*

Exercise 5
----------
You may notice that 3 very important functions are still missing from our tree. Can you guess what they are? (**hint:** *what is the rule of 3?*)

Since we are using heap memory like a linked list, we need a **Copy Constructor**, **Overloaded Assignment Operator** and **Destructor**!

Your stretch goal will be to make the Copy-ctor and Assignment-op, but for Exercise 5, implement a Destructor for the Tree class.

*(What order will you visit the nodes to delete them?)*
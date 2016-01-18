Lab Week 7: Binary Heaps
=========================

Binary Heaps are binary trees similar to BSTs, but have different properties.
The two types of Binary Heaps you need to know about are MinHeaps and MaxHeaps.
In a MinHeap, the only rule (besides adhering to tree rules) is that children have a larger value than their parent.
Similarly, MaxHeaps maintain that all children are less than their parent.

When inserting nodes into a Binary Heap, start by filling in values at the bottom of the tree from left to right.
For each insertion, heapify up to verify that the rules of the tree have not been broken.
Heapify up is a simple procedure; for a MinHeap, check if the parent is larger than the current value.
If it is, swap them and repeat for the parent until there is no parent or the parent is less than or equal to it's child's value.
This occurs in logarithmic time.

To find the minimum value in a MinHeap, it takes constant time.
Where do you think the minimum value is located?

To remove the minimum, swap the root with the most recently inserted value at the bottom of the tree.
Then, remove the swapped minimum value from the tree.
Next, find the smallest of the root's two children.
If the smallest of those is smaller than the new root, swap with the root.
Repeat this process on the swapped branch through to the bottom of the tree.
This takes logarithmic time.

Use <u><a href="https://www.cs.usfca.edu/~galles/visualization/Heap.html" target="_blank">this visualization</a></u> of a MinHeap to help you with the exercise below.

**Note**: use the following class prototype:

```c++
#include <vector>
#include <algorithm>
#include <functional>

template<typename T, typename Less=std::less<T>>
class MinHeap {
    public:
        const T & top();
        void push(const T & elem);
        void pop();
        bool empty();
        void heapify(const std::vector<T> & vec);
    private:
        std::vector<T> _heap;
        Less _less;
};
```

<!--
```c++
        void _sift_up(int idx);
        void _sift_down(int idx);
        int _sift_up_once(int idx);
        int _sift_down_once(int idx);
        int _get_left_child(int idx);
        int _get_right_child(int idx);
        int _get_parent(int child_idx);
```
-->

Exercise 1
----------
``empty`` returns ``true`` or ``false`` depending on whether or not there are items in the ``heap``

Implement ``empty``.
Comment out the other unimplemented functions to make sure you copied everything over correctly.
Run a simple test to make sure it works.


Exercise 2
----------
``push`` adds elements to the ``heap``.
``top`` gets the top element of the ``heap``.
``heapify`` takes a vector of elements and adds them to the heap.

Implement ``push``, ``top``, and ``heapify``.
See <u><a href="https://gist.github.com/CrazyWearsPJs/4c7ad50a5cd973e2e9c2" target="_blank">this gist</a></u> for some test test harnesses.
Feel free to write your own as well.
Comment out the tests that use ``pop``.

Exercise 3
----------
``pop`` removes the top element of the ``heap``.

Implement ``pop`` and run all the tests on your code.



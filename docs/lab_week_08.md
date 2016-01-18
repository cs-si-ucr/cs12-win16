Lab Week 8: QuickSort
=========================

Today you will be implementing Quicksort.
For a mediocre visualization on how Quicksort works, go <u><a href="http://algoviz.org/OpenDSA/AV/Sorting/quicksortAV.html" target="_blank">here</a></u>.

The general algorithm for quicksort:
```python
def Quicksort(L):
    # lists of size 1 or less
    # are sorted by definition
    if (len(L) <= 1):
        return

    # select pivot index using
    # the list of elements
    pivot = selectPivot(L)

    # partition into two halves
    # using the pivot value
    partIdx = partition(L, pivot)

    # recursively sort the left
    # and right sublists
    Quicksort(L[:partIdx])
    Quicksort(L[partIdx:])
```

Declarations for lab today:


```c++
#include <utility>
#include <algorithm>
#include <vector>
#include <functional>
#include <iostream>
#include <iterator>

/*
 * takes three values and uses comp to put them in sorted order.
 * the median ends up at b.
 */
template<typename T, typename Compare = std::less<T>>
void median_of_three(T & a, T & b, T & c, Compare comp = Compare());

/*
 * partitions v from first to last using mid as the pivot
 */
template<typename T, typename Compare = std::less<T>>
int partition(std::vector<T> & v, int first, int mid, int last, Compare comp = Compare());

/*
 * same as other partition;
 * creates two vectors for the left and right, then puts all the elements (except for mid)
 * in the two. Then, they are put back in v so that v is partitioned, and returns the
 * index of the pivot value.
 */
template<typename T, typename Compare = std::less<T>>
int naive_partition(std::vector<T> & v, int first, int mid, int last, Compare comp = Compare());

/*
 * uses the median of three pivot selection method, and the naive partition method
 * to implement quicksort
 *
 * has a base case of a list of size 1 or fewer
 */
template<typename T, typename Compare = std::less<T>>
void naive_quicksort(std::vector<T> & v, int first, int last, Compare comp = Compare());

/*
 * overload
 */
template<typename T>
void naive_quicksort(std::vector<T> & v) {
    naive_quicksort(v, 0, v.size());
}

/*
 * uses the median of three pivot selection method, and the faster partition method
 *
 * has a base case of a list of size 1 or fewer
 */
template<typename T, typename Compare = std::less<T>>
void quicksort(std::vector<T> & v, int first, int last, Compare comp = Compare());

/*
 * overload
 */
template<typename T>
void quicksort(std::vector<T> & v) {
    quicksort(v, 0, v.size());
}

/*
 * InsertionSort
 */
template<typename T, typename Compare = std::less<T>>
void insertionsort(std::vector<T> & v, int first, int last, Compare comp = Compare()) {
    for(int sorted = first + 1; sorted < last; ++sorted) {
        for(int i = sorted; i > first && comp(v.at(i), v.at(i-1)); --i) {
            std::swap(v.at(i), v.at(i-1));
        }
    }
}

/*
 * overload
 */
template<typename T>
void insertionsort(std::vector<T> & v) {
    insertionsort(v, 0, v.size());
}

/*
 * uses the median of three pivot selection method and the faster partition method
 *
 * insertion sort is called for reasonably small lists
 */
template<typename T, typename Compare = std::less<T>>
void faster_quicksort(std::vector<T> & v, int first, int last, Compare comp = Compare());

/*
 * overload
 */
template<typename T>
void faster_quicksort(std::vector<T> & v) {
    faster_quicksort(v, 0, v.size());
}

```

<u><a href="https://gist.github.com/CrazyWearsPJs/3138795e59a3189df5e7" target="_blank">An example test harness.</a></u>

Exercise 1
----------
Create the median_of_three function for selecting the pivot value.
Discuss with the people around you which three values you should pass into this function to find the best pivot value.

Don't forget to test it!

Exercise 2
----------
Create the naive_partition method.
Test it.

Exercise 3
----------
Create naive_quicksort

Test it!

Exercise 4
----------
Create partition

Test it!1!!

Exercise 5
----------
Create quicksort

Test it!

Exercise 6
----------
Create faster_quicksort

You are now able to run the example test harness. Do it. It is amazing.

Stretch Exercise 1
------------------
tba

Stretch Exercise 2
------------------
tba

Stretch Exercise 3
------------------
tba




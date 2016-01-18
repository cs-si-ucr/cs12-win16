Lab Week 6: Hash Tables
=========================


Exercise 1
----------
(Kinda) heap sort! Use `std::priority_queue` to
sort a vector in ascending order. `std::greater`
may prove useful. 

Hint2: Check out the Example at [cppreference Queue] - the top, pop and push operations can make this possible!(http://en.cppreference.com/w/cpp/container/priority_queue)

```cpp
void pq_sort(std::vector<int> & v)
```

Exercise 2
----------

Write a class called `UnorderedSet` with the following
public methods:

Note: first we will test with `std::string` instead
of `T`. So in your code we should we should 
declare the following typedef: `typedef std::string T`.

```cpp
int count(const T & elem)
void remove(const T & elem) 
void insert(const T & elem)
```

Your implementation of UnorderedSet uses a 
hash table with 6159 buckets ([somewhat 
arbitrary prime](http://www.orcca.on.ca/~yxie/courses/cs2210b-2011/htmls/extra/PlanetMath_%20goodhashtable.pdf)). For this exercise you will handle collisions 
using the seperate chaining method, where each
the hash function mod the table size gives you a bucket
and each bucket is a `std::list` of keys.

For testing purposes, we will use the following
naive hash function:

```cpp
unsigned int str_hash(std::string s){
    /*
     * This hash simply adds up
     * the ascii values of each character in
     * the string.
    */
    unsigned int hash_val = 0;
    unsigned int ascii_val = 0;
    for (char c : s) {
        ascii_val = static_cast<unsigned int>(c);
        hash_val += ascii_val;
    }
    return hash_val;
}
```

Use the following print method to test your class! (assumes `_buckets` is the
name of the array of buckets)
```cpp
void print() {
   unsigned int used_buckets = 0;
   unsigned int num_elems = 0;
   for(unsigned int i = 0; i < NUM_BUCKETS; ++i) {
        const auto & bucket = _buckets[i];
        if(!bucket.empty()) {
            ++used_buckets;
            std::cout << "bucket #" <<  i << ':';
            for(const auto & elem: bucket) {
                std::cout << elem << ',';
                ++num_elems;
            }
            std::cout << std::endl << std::endl;
        }
   }
   std::cout << "Number of buckets used: " << used_buckets
       << '/'  << NUM_BUCKETS  << std::endl;
   std::cout << "Number of total elements: " << num_elems << std::endl;
}


```

Stretch-Goal Exercise 
----------
Extend your `UnorderedSet` class to a `UnorderedMap` class! Use the same collision resolution method.

Implement the following class methods:
```cpp
int count (const Key & k)
Value & operator[](const Key * k) 
void remove(const Key & k)
```

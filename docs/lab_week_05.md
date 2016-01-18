Lab Week 5: Sets and Maps
=========================

Exercise 1
----------

Write a function called `freq_map` which takes in a vector
of strings and returns a stringfrequency map, a map which
maps strings to the number of times it appears in the
vector.

Use the following function prototype:
```cpp
std::map<std::string, unsigned int> freq_map(std::vector<std::string> words) 
```
Use the following text file to test your function, read the words
from the file and put them into a super big vector!
[http://termbin.com/1x6w](http://termbin.com/1x6w)


Exercise 2
----------
Write a function that returns a vector of the top `n` most frequent strings in the frequency map.

Use the following header!

```cpp
std::vector<std::string> 
top_n(std::map<std::string, unsigned int> freq_map, unsigned int n = 5)
```

Stretch-Goal Exercise 1
-----------------------
Write a class called `AnagramChecker` which 
keeps track of strings and is able to tell
if any other string is an anagram in in its
data structure.

Usage example:
```cpp
#include "anagramchecker.h"
#include <iostream>
#include <string>
using namespace std;

void printIfAnagram(const AnagramChecker & a, string s) {
    if(a.check(s)) {
        cout << s << " is an anagram of one of the words in the checker" << endl;
    } else {
        cout << s << " is not an anagram of one of the words in the checker" << endl;
    }
}

int main() {
    AnagramChecker a;
    a.add("hello");
    a.add("bye");

    printIfAnagram(a, "apple");
    printIfAnagram(a, "olleh");
}
```

The above program should print out 
```text
apple is not an anagram of one of the words in the checker
olleh is an anagram of one of the words in the checker

```
Requirements, the data structure must meet the following
space and time complexity requirements:

Where `n` is the number of strings stored by the data structure.
```text
Data Structure: O(n) space

Operations:
    add(string)
        Time: O(log n)
    
    check(string)
        Time: O(log n)
```

Extra Bits: Stretch-Goal Exercise 1
-----------------------------------
Improve SG Exercise 1 so that the data structure guarantees
the following time complexities: 

```text
Data Structure: O(n) space

Operations:
    add(string)
        Time: O(1) amortized
    
    check(string)
        Time: O(1) amortized
```



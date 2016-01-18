Asomptic notations

Order:
1. O(1)
2. O(log(log(n)))
3. O(log(n))
4. O(n)
5. O(n^2)
6. O(2^n)
7. O(n!)

1 + 2 + ... + n = n * (n+1)/2 = n^2/2 + n/2 <= n^2/2 + n^2/2 = n^2

Doubling each iteration from i=0 to i=n-1:

1 + 2 + 4 + 8 + ... + 2^n-1 = 2^n - 1 which is around 2^n


Doubling each iteration from i=0 to i=log_2(n)

1 + 2 + 4 + 8 + ... + log_2(n) = 2^(log_2(n)) -1 which is around 2^(log_2(n)) which reduces to n

Amertized overhead - overtime, it approaches some
runtime

Operations for sequential Linked Allocation:
--------------------------------------------
|Operation       |            Time Complexity|
|---------------|:-------------------------:|
|erasure/insertion at ends|   O(1)|
|"               " interior|  O(1)|
|accessing ends            |  O(1)|
|accessing interior        |  O(n)|


Operations for sequential Array Allocation:
--------------------------------------------
|Operation       |            Time Complexity|
|---------------|:-------------------------:|
|erasure/insertion at ends|   O(1) for backend, O(n) for front|
|"               " interior|  O(n)|
|accessing ends            |  O(1)|
|accessing interior        |  O(1)|


Dynamic Arrays

Deque allocated, when you get into the end, you 
wrap around, reallocate when back meets front

Ring buffer: same as Array allocation, except 
for erasure/insertion on front and end is O(1).

If the size of the buffer is cap, if all of the
operations are mod cap, then it has the same 
mathematical properties the integers have - if
the capacity is a prime number, every index 
can be assigned a unique multiplicative inverse.




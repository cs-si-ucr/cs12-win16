Lab 3: Structs and Classes
===================================
Structs
-------

Structs are a way to create new datatypes that are combinations of smaller datatypes.

Here's how you would use them:

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



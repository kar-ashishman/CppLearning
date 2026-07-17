### Date: 25th May 2026
### Source: [Learn C++ Initializers](https://www.learncpp.com/cpp-tutorial/variable-assignment-and-initialization/)
---
# Variable assignment and initialization
## List initialization is the most preferred initialization in C++ as it doesn't allow value narrowing.

There are 5 common forms of initialization in C++

```Cpp
int a;         // default-initialization (no initializer)

// Traditional initialization forms:
int b = 5;     // copy-initialization (initial value after equals sign)
int c ( 6 );   // direct-initialization (initial value in parenthesis)

// Modern initialization forms (preferred):
int d { 7 };   // direct-list-initialization (initial value in braces)
int e {};      // value-initialization (empty braces)
int h = { 6 }; // copy-list-initialization of initial value 6 into variable height (rarely used)
```
---
## 1. List-initialization disallows narrowing conversions
To list-initialize a variable using a value that the variable can not safely hold, the compiler is required to produce a diagnostic (compilation error or warning) to notify.

```cpp
int main()
{
    // An integer can only hold non-fractional values.
    // Initializing an int with fractional value 4.5 requires the compiler to convert 4.5 to a value an int can hold.
    // Such a conversion is a narrowing conversion, since the fractional part of the value will be lost.

    int w1 { 4.5 }; // compile error: list-init does not allow narrowing conversion

    int w2 = 4.5;   // compiles: w2 copy-initialized to value 4
    int w3 (4.5);   // compiles: w3 direct-initialized to value 4

    return 0;
}
```
Narrowing conversion is only disallowed during initialization. Later in code narrowing conversion is allowed.

```
int main()
{
    int w1 { 4 };
    w1 = 4.5;   // Allowed, w1 has a value of 4
```
---
## 2. Initializing multiple variables

```Cpp
int a = 5, b = 6;          // copy-initialization
int c ( 7 ), d ( 8 );      // direct-initialization
int e { 9 }, f { 10 };     // direct-list-initialization
int i {}, j {};            // value-initialization
```
---
## 3. Unused initialized variables warnings
To stop unused warning use `[[maybe_unused]]`
```Cpp
#include <iostream>

int main()
{
    [[maybe_unused]] double pi { 3.14159 };  // Don't complain if pi is unused
    [[maybe_unused]] double gravity { 9.8 }; // Don't complain if gravity is unused
    [[maybe_unused]] double phi { 1.61803 }; // Don't complain if phi is unused

    std::cout << pi << '\n';
    std::cout << phi << '\n';

    // The compiler will no longer warn about gravity not being used

    return 0;
}
```

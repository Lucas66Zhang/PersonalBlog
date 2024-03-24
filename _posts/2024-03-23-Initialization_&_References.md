---
title: "CPP Course 2: Initialization & References"
date: 2024-03-23
categories: CPP
Lesson: 2
---

## 1. Initialization

**Definition:** Provides initial values at the time of construction.

But How?

1. Direct initialization
2. Uniform initialization
3. Structured Binding

### 1.1 Direct initialization

```cpp
#include <iostream>

int main() {
    int numOne = 12.0;
    int numTwo(12.5);
    std::cout << "numOne is " << numOne << std::endl;
    std::cout << "numTwo is " << numTwo << std::endl;
    
    return 0;
}

// numOne is 12
// numTwo is 12
```

In direct initialization, `C++` does not care the type of initial value. Therefore, sometime there will be unusual thing happened like `numTwo` in the above example (**narrowing conversion**).

### 1.2 Uniform initialization

Initialization variables with **curly braces**.

```cpp
#include <iostream>

int main() {
    int numOne{12};
    // int numTwo{12.5}; will cause error
    std::cout << "numOne is " << numOne << std::endl;
    
    return 0;
}

// numOne is 12
```

**In uniform initialization, data type matters.** Uniform initialization is awesome because:

1. It is **safe**! (Constrains on data types)
2. It is **ubiquitous**. It works for all typpes like `vector`, `map`, and custom classes, among other things.

Uniform initialization for `vector`:

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> numbers{1, 2, 3, 4, 5}; // uniform initialization of a vector
    
    for (int num : numbers) {
        std::cout << num << " ";
    }
    std::cout << std::endl;
    
    return 0;
}

// 1 2 3 4 5 
```

Uniform initialization can provide convenience when initializing structs (recall the example in the last lesson).

```cpp 
Student s; 
s.name = "Haven";  
s.state = "AR"; 
s.age = 22;  

//is the same as ... 
Student s = {"Haven", "AR", 22};
```

### 1.3 Structured Binding (C++ 17)

- A useful way to initialize some variables from data structures with fixed sizes at compile time 
- Ability to access multiple values returned by a function

```cpp
// auto [var1, var2, ..., varN] = expression;

#include <tuple>
#include <iostream>

int main() {
    std::tuple<int, double, std::string> myTuple = {1, 2.3, "hello"};

    auto [x, y, z] = myTuple;

    std::cout << x << ", " << y << ", " << z << std::endl;
    // 1, 2.3, hello
    return 0;
}
```

## 2. References

**Definition:** Declares a named variable as a reference, that is, an alias to an already-existing object or function.

We use reference by `&`. Here is a simple example.

```cpp
int num = 5;
int& ref = num;
ref = 10; // assigning a new value through the reference
std::cout<<num<<std::endl; // output: 10
```

In the above example:

- `num` is a variable of type `int`, that is assigned to have the value 5.
- `ref` is a variable of type `int&`, that is an **alias** to num.
- So when we change `ref`, we therefore also change `num` since it is a reference.

**Pass by reference:** Let’s look at the following example

```cpp
#include <iostream>
#include <math.h>

// note the ampersand!
void squareN(int& N) {
    n = std::pow(n, 2);
}

int main() {
    int num = 2;
    squareN(num);
    std::cout << num << std::endl;
    return 0;
}

// Output: 4
```

- n is being passed into `squaredN` by reference.
- Thus, n is actually going to be modified inside of `squareN`

**Passing by reference:** Take the actual piece of memory, do not make a copy.

**Passing by value:** Make a copy, do not take in the actual variable.

> Just like shallow copy v.s. deep copy in `python`

The example of passing by value:

```cpp
#include <iostream>
#include <math.h>

// note the ampersand!
void squareN(int n) {
    n = std::pow(n, 2);
} // n goes out of the scope

int main() {
    int num = 2;
    squareN(num);
    std::cout << num << std::endl;
    return 0;
}

// Output: 2 (unchanged)
```

To deepen our understanding, let’s look at a classic reference-copy bug.

```cpp
#include <vector>

void shift(std::vector<std::pair<int, int>> &nums) {
    for (auto [num1, num2] : nums) {
        num1++;
        num2++;
    }
}
```

- nums are passed in by reference
- we are not modifying nums in this function
- thus, nums will not be modified

Correct code should be:

```cpp
#include <vector>

void shift(std::vector<std::pair<int, int>>& nums) {
    for (auto& [num1, num2] : nums) {
        num1++;
        num2++;
    }
}
```

## 3. L-values v.s. R-values

- L-value can be to the left **or** the right of an equal sign
- R-value can be **only** to the right f an equal sign

```cpp
#include <stdio.h>
#include <cmath>
#include <iostream>

int squareN(int& num) {
    return std::pow(num, 2);
}

int main() {
    int lValue = 2;
    auto four = squareN(lValue);
    auto fourAgain = squareN(2);
    std::cout << four << std::endl;
    return 0;
}
```

This will cause an error:

![error caused by passing in r-vlaue by reference](https://github.com/Lucas66Zhang/PersonalBlog/blob/main/assets/images/cpp/rvalue.png?raw=true)

- r-values are temporary, so we can not pass in an r-vlaue by reference.

## 4. Const

**Definition:** A qualifier for objects that declares they cannot be modified. 

**How?** Just add a `const` before initialization.

```cpp
const int numOne = 1;
```

> We can not declare a non-const reference to a const variable.

```cpp
const std::vector<int> const_vec{1, 2, 3};
const std::vector<int>& const_ref_vec{const_vec};
```


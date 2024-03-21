---
title: "CPP Course 1: Types & Structs"
date: 2024-03-21
---

## 1. C++ Basic

### 1.1 Basic Syntax

Here is a simple `cpp` code:

```c++
#include <iostream>

int main() {
    std::cout << "Hello world!" << std::endl;
    return 0;
}
```

From the above example, we can obtain some basic rules of `cpp`:

1. To import additional functionality, we use `#include`.
2. All lines / statements end in a semicolon.
3. Function declarations need the type of the return, the name of the function, and any parameters (inside the parentheses).
4. The code of a function lives inside a block marked by curly brackets `{}`.

### 1.2 The STL

 The properties of STL:

- Tons of general functionality
- Built in classes like maps, sets, vectors
- Accessed through the namespace `std::`
- Extremely powerful and well-maintained

## 2. Types

### 2.1 Fundamental Types in `cpp`:

```c++
#include <string> 
int val = 5; //32 bits (usually) 
char ch = 'F'; //8 bits (usually) 
float decimalVal1 = 5.0;  //32 bits (usually) 
double decimalVal2 = 5.0;  //64 bits (usually) 
bool bVal = true;  //1 bit 
std::string str = "Haven";
```

> `cpp` does not support `string` primitively but `std` provides a feasible implementation.

### 2.2 `cpp` is statically typed language

- **Statically typed**: everything with a name (variables, functions, etc) is given a type before runtime.
- **Dynamically typed**: everything with a name is given a type at runtime based on the thing’s current value, like `Python`.

The spot difference is when the source code translated (converting source code into something a computer can understand, such as machine code).

Here are a few examples to show the difference between statically typing and dynamically typing:

![difference between statically typing and dynamically typing 1](/docs/assets/images/image1.png)

![difference between statically typing and dynamically typing 2](/docs/assets/images/image2.png)

![difference between statically typing and dynamically typing 3](/docs/assets/images/image1.png)

### 2.3 Function overloading

We cannot define multiple identical functions in `cpp`, but we can **overload** a function to have multiple versions.

To overload a function, we need to declare multiple functions with the sample name but **different typed** parameters or a **different number** of parameters. Here is an example:

```c++
int half (int x) {
    std::cout << "int version" << std::endl;
    return x / 2;
}

double half(double x) {
    std::cout << "double version" << std::endl;
    return x / 2;
}

half(3); // int version, return 1
half(3.0); // double version, return 1.5
```

## 3. Structs

### 3.1 The problems with types so far

Strong and statically typed languages are great, but there are a few downsides:

- it can be a pain to know what the type of a variable is
- any given function can only have exactly one return type
- `cpp` primitives (and even the types in the STL) can be limited

As for the first problem, we can introduce `auto` keyword. It tells the complier to deduce the type of variables.

- This is **NOT** the same as not having a type
- The complier is able to determine the type itself without being explicitly told.

Here are a few examples:

```c++
// What types are these? 
auto a = 3; // int 
auto b = 4.3; // double 
auto c = ‘X’; // char 
auto d = “Hello”; // char* (a C string)
```

As for the remaining two problems, we need to introduce `struct` to address them.

### 3.2 What is `struct`

A `struct` is a a group of **named variables**, each with their own type, that allows programmers to **bundle different types together**. (Sounds like a `class` with multiple features 🤔)

Here is an example:

```c++
struct Student { 
    string name; // these are called fields 
    string state; // separate these by semicolons 
    int age; }; 

Student s; 
s.name = "Haven"; 
s.state = "AR"; 
s.age = 22; // use . to access fields
```

`struct`s can pass around or return grouped information.

```c++ 
Student randomStudentFrom(std::string state) { 
    Student s; 
    s.name = "Haven";//random = always Haven 
    s.state = state; 
    s.age = std::randint(0, 100); 
    return s; 
} 

Student foundStudent = randomStudentFrom("AR"); 
cout << foundStudent.name << endl; // Haven
```

The above syntax is little clunky to initialize. Let’s abbreviate.

```cpp
 Student s; 
s.name = "Haven";  
s.state = "AR"; 
s.age = 22;  

//is the same as ... 
Student s = {"Haven", "AR", 22};
```

### 3.3 The STL has its own `struct`

`std::pair`: An STL built-in struct with **two fields** of **any type**.

- `std::pair` is a template: You specify the types of the fields inside <> for each pair object you make 
- The fields in `std::pair` are name `first` and `second`

Just like:

```cpp
struct Pair { 
    fill_in_type first; 
    fill_in_type second; 
};
```

## 4. Recap

- Everything with a name in your program has a **type**
- **Static type system** prevent errors before your code runs!
- **Structs** are a way to bundle a bunch of variables of many types
- `std::pair` is a type of struct that had been defined for you and is in the STL
- So you access it through the **std:: namespace** (std::pair)
- `auto` is a keyword that tells the compiler to deduce the type of a variable, it should be used when the type is obvious or very cumbersome to write out

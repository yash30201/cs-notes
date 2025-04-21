# Language Knowledge

* Difference between const, constexpr, and consteval.
* Explain RAII (Resource Acquisition Is Initialization) principle with examples (smart pointers).
* Explain move semantics (std::move, rvalue references) and perfect forwarding.
* What is pointer aliasing? How can restrict keyword (or compiler specifics) help?
* Memory layout of structs/classes (padding, alignment).
* Template specialization and SFINAE (Substitution Failure Is Not An Error).
* Static vs Dynamic linking.

I want to learn about c++. Try to explain the answer to the following question in a paragraph and give code examples if you feel soo. After that, also give some edge case tricky questions and their answers if applicable for that topic.

What are the differences between const, constexpr, and consteval?


## Virtual Functions

- Virtual functions are a fundamental mechanism in C++ used to achieve runtime polymorphism (aka late binding or dynamic dispatch)
- When we declare a method virtual, it signals that the method is intended to by overridden by derived classes using the override keyword.
- This functionality of virtual function is achieved through vTables which contains key value mappings for definitions and is used in runtime to find the appropriate implementation of a method.

<details>
<summary>Code Example</summary>

```cpp
#include <iostream>
#include <string>

// Base class
class Animal {
public:
    // Declare a virtual function
    virtual void speak() const {
        std::cout << "Some generic animal sound" << std::endl;
    }

    // Virtual destructor (important!)
    virtual ~Animal() {
        std::cout << "Animal destructor called." << std::endl;
    }
};

// Derived class 1
class Dog : public Animal {
public:
    // Override the virtual function
    void speak() const override { // 'override' keyword is optional but good practice
        std::cout << "Woof!" << std::endl;
    }

     ~Dog() override {
        std::cout << "Dog destructor called." << std::endl;
    }
};

// Derived class 2
class Cat : public Animal {
public:
    // Override the virtual function
    void speak() const override {
        std::cout << "Meow!" << std::endl;
    }

     ~Cat() override {
        std::cout << "Cat destructor called." << std::endl;
    }
};

// Function that uses a base class pointer
void makeAnimalSpeak(const Animal* pAnimal) {
    pAnimal->speak(); // Calls the correct derived class function at runtime
}

int main() {
    Animal* ptrAnimal1 = new Dog();
    Animal* ptrAnimal2 = new Cat();
    Animal* ptrAnimal3 = new Animal();

    std::cout << "Calling speak via base pointers:" << std::endl;
    makeAnimalSpeak(ptrAnimal1); // Outputs: Woof!
    makeAnimalSpeak(ptrAnimal2); // Outputs: Meow!
    makeAnimalSpeak(ptrAnimal3); // Outputs: Some generic animal sound

    std::cout << "\nDeleting objects via base pointers:" << std::endl;
    delete ptrAnimal1; // Correctly calls ~Dog() then ~Animal()
    delete ptrAnimal2; // Correctly calls ~Cat() then ~Animal()
    delete ptrAnimal3; // Correctly calls ~Animal()

    return 0;
}
```
</details>


### Questions

- What happends if we delete a derived class object through a base class pointer where the base class destructor is not trivial?
  - This behaviour is undefined! The derived class destructor won't be called and it may lead to resource leaks.
- Can a method be static and virtual both?
  - No. Static methods belong to the class itself, not to any instance.
- What is a pure virtual function?
  - Its a virtual function declared in base class that has no implementation in the base class. It's declared as `virtual T methodName(args..) = 0`.
  - A class containing one or more virtual methods becomes an abstract class (whose instance cannot be created directly)
  - For a derived class to be concrete (means if you want to create objects of derived class), then you need to make sure
    all the virtual methods are overridded.
- What happens if you call a virtual function from within a constructor or destructor?
  - When a virtual function is called from within a constructor or destructor, the virtual function mechanism is
    effectively disabled for the object being constructed or destructed.

## How VTable and VPtr work together to achive late binding?

- When a class is defined or inherited, compiler creates a static array called VTable which function pointers mapping
  to actual implementation fo that virtual function for that specific class.
- If a derived class inherits overrides a base class virtual method, then it's VTable contains the entry to overridden
  implementation, otherwise to the base class version.
- Apart from this, each class object creates a hidden VPtr variable pointing to the VTable of the object's actual class.
- When a virtual method is invoked throught a base class pointer or reference, then the program follows the object's VPtr
  to find the relevant VTable.

### Questions

- Does adding the first virtual function to a class affect the size of its objects? What about adding subsequent virtual functions?
  - Yes, when first virtual function is added, each of the object would now take memory for an extra vptr pointer. But
    for each subsequent virtual function addition, no extra memory is needed as the entries are updated in VTable which
    is shared by all objects (as it's static)

## Explain RAII principle with examples (smart pointers).

RAII = Resource Acquisition is Initialization

It comprised of steps:

- Acquisition via constructor (usually, apart from this, there may be framwork in place using SetUp and TearDown
  constructs).
- Release via destructor

Weak Pointer => Like shared pointer but doesn't guarantees that resource will be there. Though it allows to check
if resource is still there.

## Explain move semantics (std::move, rvalue references) and perfect forwarding.

Move semantics allows users to transfer the ownership of a resource from one identifier to another without performing
deep copy.

RValue references are references which can only bind with rvalues. We need rvalue references to distinguish between
lvalue reference and an rvalue reference. `T &&ref = some new object or std::move(x);

`std::move` converts a lvalue to an rvalue reference.

Perfect forwarding is achieved using `std::forward` which forwards lvalue and rvalue references as they are received,
allowing perfect coupling between interfaces while retaining lvalue / rvalue properties.

## What is pointer aliasing? How can restrict keyword (or compiler specifics) help?

Pointer aliasing refers to the situation where two pointers (or references) point to the same memory location.

This is a huge challenge for compiler optimizers because it can never assume that any two pointers are unrelated, it
always has to assume that the pointers could point to same memory location and hence it has to be very conservative.

```cpp
void update(int* p, int* q, int n) {
    for (int i = 0; i < n; ++i) {
        *p = *p + 1;
        *q = *q + 1;
    }
}
```

In ther above example, compiler cannot vectorize the operations (parallelize) because p and q point to same memory location.

Hence C++23 introduced `restrict` keyword, using which you are telling the compiler that for the lifetime of this
pointer, this pointer is the only way to access the memory region it points to, especially for modifications.

Hence in the below example

```cpp
void update_restricted(int* restrict p, int* restrict q, int n) {
    for (int i = 0; i < n; ++i) {
        *p = *p + 1; // Compiler knows this write doesn't affect memory read/written by *q
        *q = *q + 1; // Compiler knows this write doesn't affect memory read/written by *p
    }
}
```

Compiler can perform optimizations.

## Memory layout of structs/classes (padding, alignment).

Padding is done so that all the size of class / structs are aligned to cpu's read chunk size

## Drawback of aggresive inlining

- Increased code size.
- Potential increase in cache misses.

## asdf

## asdf


# Extra Questions

## How a program runs in c++?

### Step 1: Pre processing

- Process #include directives
- Process #define macros
- Process #ifdef, #ifndef and #endif directives for conditional compitation
- Output is a text `.i` file which we usually don't see.

### Step 2: Compilation

- Takes the `.i` file
- Checks for semantic and syntax errors as per c++ language standards
- Compiles it into assembly language specific to your computers architecture
- Output's an assembly file: `.s` file

### Step 3: Assembly

- Takes the `.s` assembly code
- Converts it into machine code files (`.o` or `.obj` files)
- These are still not ready to run as the references are not resolved yet.

### Step 4: Linker

- Linked resolves all external symbols and refences to create a executable `.exe` in windows and extensionless
  executable files in macos / linux.

### Step 5: Loading

- Executable is loaded from filesystem by operating system's loader
- Loader allocates memory for programs' code, data, stack and help
- Loader loads the machine code and data into allocated memory
- Linked any dynamic libraries if program uses any


### Step 6: Execution

- OS sets up necessary registers, program counters, stack pointers, etc.
- Transfers control to program's entry point which is some runtime startup code provided by the linker / compiler
- This runtime startup code initialized c++ runtime environment (static objects, io stream synchronization, etc)
- Main function starts
- On returning or `exit()`, c++ runtime performs cleanup and then control is transfered back to OS.

## How does a compiler works?

### Step 1: Lexical Analysis (Scanning)

Scan to pre processed code to find out tokens and hence convert it into a stream of tokens

### Step 2: Syntactic Analysis

See if syntax is correct or not.

### Step 3: Semantic Analysis

See if tokens make sense, operators are operating in correct types, identifiers are present in correct scope, scopes
are resolved appropriately incase of collision.

### Step 4: Intermediate Code Representation (IR)

Closer to machine code but still machine independent

### Step 5: Optimizations

- Dead code removal
- Loop Optimizations
- Constant folding
- Function inlining
- Register Allocation

### Step 6: Code Generation

Convert into machine dependent assembly

## Storage specifiers

- auto
- static
- register (just a hint for the compiler that this is frequently accessed memory)
- extern, same as static, just says that it may be defined and used across different files
- thread_local



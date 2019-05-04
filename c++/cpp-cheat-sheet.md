# C++ Cheat SHeet
Ingo Andelhofs   
1ste bachelor informatica


## C++ Basics
A simple hello world example.
```cpp
#include <iostream>

int main() {
    std::cout << "Hello World" << std::endl;
}
```

## Templates, auto, ...
```cpp
// Templates
Template <T> ...

// Auto
auto num{7};
```

## C++ Standard Template Library (STL)
### std::string
...

### std::vector
...

### std::map
...

### std::tuple
...


## Classes
```cpp
#include <string>

class MyClass {
    public:
        // Constructors & destructor
        MyClass();
        ~MyClass();

        // Getters
        int getValue() const;
        std::string getString() const; 

        // Setters
        void setValue(int value);
        void setString(std::string str);

        // Utils
        void doSomething();

    private:
        int m_value;
        std::string m_string;
};
```

## Inheritance

## Polymorpism

## Operator overloading

## ...
## Constructors

### Default constructor

A constructor that can be called with no arguments.

#### 1. Implicitly-Declared (Compiler-Generated)

If the class doesn't have any user-defined constructors, the C++ compiler automatically provides
an implicit public default constructor.

If you define any other constructor (even a parameterized one), the compiler does not generate a default one.

```cpp
class Player {
  std::string name;
  int score;
};

Player p; // calls the default constructor
```

#### 2. User-Defined

```cpp
class Player {
  std::string name;
  int score;

  Player() {
    name = "Unknown";
    score = 0;
  }
};

Player p; // calls the default constructor
```

#### 3. Defaulted Constructor (C++11)

Useful if you have a parameterized constructor, but still want the native,
highly optimized, compiler-generated constructor.

```cpp
class Player {
  std::string name;
  int score;

  Player(std::string n, int s): name(n), score(s) {}

  Player() = default; // forces the default constructor to be generated.
};
```

#### 4. Parameterized with Default Arguments

A constructor with parameters can still act as a default constructor,
as long as every single parameter is provided with a default value.

```cpp
class Player {
  std::string name;
  int score;

  Player(std::string n = "Unknown", int s = 0): name(n), score(s) {}
};

// both of these statements are valid
Player p1; // defaults to name = "Unknown", score = 0.
Player p2("Peter", 10);
```

#### Note

When calling a default constructor, do not use empty parentheses because
the compiler will interpret it as a function declaration.

```cpp
Player p(); // ❌ compiler thinks this is a declaration of a function named p that returns a Player object.
Player p; // ✅
```

### Parameterized constructor

#### Member initialization

There are two types of member initialization with parameterized constructors in C++.

1. Member initialization list

- Runs before the constructor body executes.
- Directly invokes the appropriate constructor.
- One-step process, avoids temporaries, faster.
- Mandatory for: const members, references, and types without default constructors.

```cpp
class Point {
  int x;
  int y;

  Point(int xVal, int yVal): x(xVal), y(yVal) {}
}
```

2. Assignment in the constructor body

- Runs inside the constructor body.
- Default-constructs the member first, then overwrites it via an assignment operator.
- Slower for user-defined types (two-step process).

```cpp
class Point {
  int x;
  int y;

  Point(int xVal, int yVal) {
    x = xVal;
    y = yVal;
  }
}
```

#### Constructor overloading

You can define multiple parameterized constructors in a single class as long as they have different parameter counts and/or data types.

```cpp
class Point {
    int x, y;
public:
    Point(int val) : x(val), y(val) {}      // Takes one argument
    Point(int xVal, int yVal) : x(xVal), y(yVal) {} // Takes two arguments
};
```

#### Default Arguments

You can assign default values to constructor parameters. If an argument is missing during object creation, the default value is applied. A constructor where all parameters have default values can also function as a default constructor.

```cpp
class Color {
    int r, g, b;
public:
    // Functions as both a parameterized and a default constructor
    Color(int red = 0, int green = 0, int blue = 0) : r(red), g(green), b(blue) {}
};
```

#### Inheritance Context

When working with derived classes, the derived class's constructor must explicitly forward the necessary values to the base class's parameterized constructor using the initializer list syntax.

```cpp
class Base {
    int data;
public:
    Base(int d) : data(d) {}
};

class Derived : public Base {
    int childData;
public:
    // Forwarding argument 'd' to Base constructor
    Derived(int d, int cd) : Base(d), childData(cd) {}
};
```

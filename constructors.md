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
- One-step process, avoids temporaries - faster.
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

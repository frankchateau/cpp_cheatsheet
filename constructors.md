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
}

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
}

Player p; // calls the default constructor
```

#### 3. Defaulted Constructor (C++11)

Useful if you have a parameterized constructor, but still want the native,
highly optimized, compiler-generated constructor.

```cpp
class Player {
  std::string name;
  int score;

  Player(std::string name_val, int score_val): name(name_val), score(score_val) {}

  Player() = default; // forces the default constructor to be generated.
}
```

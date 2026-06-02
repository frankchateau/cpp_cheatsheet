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

  Player(std::string name_val, int score_val): name(name_val), score(score_val) {}

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

  Player(std::string name_val = "Unknown", int score_val = 0): name(name_val), score(score_val) {}
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

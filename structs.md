## Struct initialization

```cpp
struct Player {
    std::string name;
    int score;
    double health;
};
```

#### 1. Aggregate Initialization (C++11)

```cpp
Player p1{"Alice", 100, 53.23}; // order matches the declaration
Player p2{"Bob"}; // score = 0, health = 0
```

#### 2. Designated Initializers (C++20)

```cpp
// the order of values must be the order of declaration, but you can skip members.
Player p3{.name = "Charlie", .score = 250, .health = 80.0};
Player p4{.name = "Diana", .health = 100.0}; // score = 0
```

#### 3. Default Member Initializers (C++11)

```cpp
struct Enemy {
  int damage = 10;
  int speed = 5;
};

Enemy e1; // damage = 10, speed = 5
Enemy e2{20}; // damage = 20, speed = 5
```

#### 4. Zero-Initialization / Empty Braces (C++11)

```cpp
Player p5{}; // name = "", score = 0, health = 0.0
```

#### 5. Traditional Constructors (Class-like Initialization)

```cpp
struct Point {
  int x;
  int y;
  Point(int x_val, int y_val): x(x_val), y(y_val) {}
};

Point p(20, 10);  // Initialized via constructor
```

#### 6. Classic C-Style Initialization

Supported for backwards compatibility, less common in modern C++ codebases.

```cpp
Player p6 = {"Eve", 400, 50.0};
```

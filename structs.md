## Struct initialization

```cpp
struct Player {
    std::string name;
    int score;
    double health;
};
```

#### Aggregate Initialization (C++11 and later)

```cpp
Player player1{"Alice", 100, 53.23}; // order matches the declaration
Player player2{"Bob"}; // score = 0, health = 0
```

#### Designated Initializers (C++20)

```cpp
// the order of values must be the order of declaration, but you can skip members.
Player player3{.name = "Charlie", .score = 250, .health = 80.0};
Player player4{.name = "Diana", .health = 100.0}; // score = 0
```

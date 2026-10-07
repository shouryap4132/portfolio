---
layout: post
codemirror: True
title: 3.09 Developing Algorithms (Peppa Maze) HW
categories: ['Python']
lesson_language: Python
lesson_topic: Developing-Algorithms HW
lesson_part: interactive
lesson_type: lesson
permalink: /python/developing-algorithms-peppa-hw
author: Shourya Patel
---

# 3.09 Developing Algorithms — Peppa Pig Maze Homework

This lesson ends with "try modifying the examples to see how algorithm changes affect behavior." Below I work through **every** example in the lesson: I run it, modify it, and add my own algorithm for the same problem, then build Peppa's maze algorithm in Python.

## 1. Two (now three) algorithms to add numbers


```python
# Example 1 modified: three different algorithms that add two numbers
a = 3
b = 5

def add_numbers_manual(x, y):
    total = 0
    total += x
    total += y
    return total

def add_numbers_direct(x, y):
    return x + y

def add_numbers_counting(x, y):
    # My algorithm: start at x and count up one at a time, y times
    total = x
    for _ in range(y):
        total += 1
    return total

for x, y in [(a, b), (10, 0), (7, 12)]:
    print(x, "+", y, "->", add_numbers_manual(x, y), add_numbers_direct(x, y), add_numbers_counting(x, y))
```

    3 + 5 -> 8 8 8
    10 + 0 -> 10 10 10
    7 + 12 -> 19 19 19


All three agree for every pair I tried, so they're equivalent for non-negative numbers. **But** the counting algorithm only works when `y` is a non-negative whole number (`range(-2)` does nothing), which shows that algorithms that look like they do the same thing can behave differently on some inputs — and it does more work as `y` grows.

## 2. Boolean expressions and conditionals


```python
# Example 2 modified: test all three relationships between x and y
def compare(x, y):
    if x > y:
        return "x is greater than y"
    elif x < y:
        return "y is greater than x"
    else:
        return "x and y are equal"

for x, y in [(10, 5), (5, 10), (7, 7)]:
    print(x, y, "->", compare(x, y))

# The same decision written as a Boolean expression
x, y = 10, 5
print("Boolean result of x > y:", x > y)
```

    10 5 -> x is greater than y
    5 10 -> y is greater than x
    7 7 -> x and y are equal
    Boolean result of x > y: True


The original only had two outputs, so it said "y is greater or equal" even when they were equal. I split the equal case into its own branch.

## 3. isEven — JavaScript example translated and modified in Python


```python
def is_even(num):
    return num % 2 == 0      # returns True or False

for value in [7, 10, 0, -3]:
    result = is_even(value)
    if result:
        print(value, "is even")
    else:
        print(value, "is odd")
    print("Is", value, "even?", result)
```

    7 is odd
    Is 7 even? False
    10 is even
    Is 10 even? True
    0 is even
    Is 0 even? True
    -3 is odd
    Is -3 even? False


The same modified JavaScript version (loops over several values instead of one):

```javascript
function isEven(num) {
  return num % 2 === 0;
}

for (const value of [7, 10, 0, -3]) {
  const result = isEven(value);
  console.log(value + (result ? " is even" : " is odd"));
}
// 7 is odd
// 10 is even
// 0 is even
// -3 is odd
```

Note: in JavaScript `-3 % 2` is `-1`, not `1`, but `-1 === 0` is still false, so -3 is correctly reported as odd.

## 4. Peppa's maze algorithm (Python version)

The lesson's demo draws a 5×5 maze and checks every move before Peppa takes it. Here is the same algorithm in Python: before each step it checks the **Boolean condition** "is the next cell inside the grid and not a wall?", **updates** Peppa's position only if the move is valid, and **redraws** the maze.


```python
MAZE = [
    "P.#..",
    ".##.#",
    "...#.",
    "#.#..",
    "#...E",
]
MOVES = {"up": (-1, 0), "down": (1, 0), "left": (0, -1), "right": (0, 1)}

def find(symbol):
    for r in range(len(MAZE)):
        for c in range(len(MAZE[r])):
            if MAZE[r][c] == symbol:
                return r, c

def can_move(row, col):
    # Boolean condition: inside the grid AND not a wall
    inside = 0 <= row < len(MAZE) and 0 <= col < len(MAZE[0])
    return inside and MAZE[row][col] != "#"

def draw(pos):
    for r in range(len(MAZE)):
        line = ""
        for c in range(len(MAZE[r])):
            if (r, c) == pos:
                line += "🐷"
            elif MAZE[r][c] == "#":
                line += "⬛"
            elif MAZE[r][c] == "E":
                line += "🏁"
            else:
                line += "⬜"
        print(line)
    print()

def run_algorithm(steps):
    pos = find("P")
    for step in steps:
        dr, dc = MOVES[step]
        new_row, new_col = pos[0] + dr, pos[1] + dc
        if can_move(new_row, new_col):
            pos = (new_row, new_col)
            print("Moved", step)
        else:
            print("Blocked moving", step, "- Peppa stays put")
    draw(pos)
    if pos == find("E"):
        print("Peppa reached the end of the maze!")
    else:
        print("Peppa did not reach the end yet.")

# A correct algorithm (sequence of steps) through the maze
run_algorithm(["down", "down", "right", "down", "down", "right", "right", "right"])
```

    Moved down
    Moved down
    Moved right
    Moved down
    Moved down
    Moved right
    Moved right
    Moved right
    ⬜⬜⬛⬜⬜
    ⬜⬛⬛⬜⬛
    ⬜⬜⬜⬛⬜
    ⬛⬜⬛⬜⬜
    ⬛⬜⬜⬜🐷
    
    Peppa reached the end of the maze!


**Modification — a buggy algorithm:** this version starts by going right twice instead of down twice. The second move hits a wall, and the validity check blocks it. The rest of the steps then run from the wrong square and keep hitting walls, so she never reaches the end. Changing the order of the steps changes the result.


```python
run_algorithm(["right", "right", "down", "down", "right", "down", "down", "right"])
```

    Moved right
    Blocked moving right - Peppa stays put
    Blocked moving down - Peppa stays put
    Blocked moving down - Peppa stays put
    Blocked moving right - Peppa stays put
    Blocked moving down - Peppa stays put
    Blocked moving down - Peppa stays put
    Blocked moving right - Peppa stays put
    ⬜🐷⬛⬜⬜
    ⬜⬛⬛⬜⬛
    ⬜⬜⬜⬛⬜
    ⬛⬜⬛⬜⬜
    ⬛⬜⬜⬜🏁
    
    Peppa did not reach the end yet.


**Another algorithm for the same problem:** instead of a fixed list of moves, a search algorithm (breadth-first search) lets the computer *find* a path by itself. Same goal, very different algorithm.


```python
def find_path():
    start, end = find("P"), find("E")
    queue = [(start, [])]
    visited = [start]
    while len(queue) > 0:
        pos, path = queue.pop(0)
        if pos == end:
            return path
        for name in MOVES:
            dr, dc = MOVES[name]
            nxt = (pos[0] + dr, pos[1] + dc)
            if can_move(nxt[0], nxt[1]) and nxt not in visited:
                visited.append(nxt)
                queue.append((nxt, path + [name]))
    return None

path = find_path()
print("Path found by search:", path)
run_algorithm(path)
```

    Path found by search: ['down', 'down', 'right', 'down', 'down', 'right', 'right', 'right']
    Moved down
    Moved down
    Moved right
    Moved down
    Moved down
    Moved right
    Moved right
    Moved right
    ⬜⬜⬛⬜⬜
    ⬜⬛⬛⬜⬛
    ⬜⬜⬜⬛⬜
    ⬛⬜⬛⬜⬜
    ⬛⬜⬜⬜🐷
    
    Peppa reached the end of the maze!


## 5. Different algorithms for the same problem (max)


```python
def max_if(a, b):
    if a > b:
        return a
    return b

def max_loop(values):
    # My algorithm: works for any number of values, not just two
    largest = values[0]
    for v in values:
        if v > largest:
            largest = v
    return largest

for a, b in [(7, 9), (12, 3), (4, 4)]:
    print(a, b, "->", max_if(a, b), max(a, b), max_loop([a, b]))
print("max_loop on a list:", max_loop([3, 17, 8, 21, 5]))
```

    7 9 -> 9 9 9
    12 3 -> 12 12 12
    4 4 -> 4 4 4
    max_loop on a list: 21


## Key takeaways (in my own words)

- An algorithm is a precise, step-by-step list of instructions — Peppa's move list is one, and so is the search that finds the path.
- The same problem (add, compare, find the max, solve the maze) can be solved by very different algorithms. Some are simpler, some handle more inputs (`max_loop` works for any list), and some do more work (`add_numbers_counting`).
- Boolean conditions (`can_move`, `is_even`, `x > y`) are how algorithms make decisions.
- Changing one step in an algorithm (swapping two moves) can completely change the result, so algorithms must be tested, not assumed correct.

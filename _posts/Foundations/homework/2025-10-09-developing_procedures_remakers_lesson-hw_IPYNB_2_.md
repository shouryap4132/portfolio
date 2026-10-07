---
layout: post
codemirror: True
title: 3.13 Developing Procedures HW
categories: ['Python']
lesson_language: Python
lesson_topic: Developing-Procedures HW
lesson_part: interactive
lesson_type: lesson
permalink: /python/developing-procedures-hw
author: Shourya Patel
---

# 3.13 Developing Procedures — Homework

Completed the Dessert Robot examples, the naming mini-game, and all three exercises from "Teaching tips and exercises."

## Python example — Dessert Robot


```python
def make_dessert():
    measure_flour()
    mix_ingredients()
    bake()

def measure_flour():
    print("Measuring 2 cups of flour.")

def mix_ingredients():
    print("Mixing flour, sugar, eggs.")

def bake():
    print("Baking at 350°F for 25 minutes.")

make_dessert()
```

    Measuring 2 cups of flour.
    Mixing flour, sugar, eggs.
    Baking at 350°F for 25 minutes.


## Mini-game: Name the Procedures

The original game uses `input()`, which can't be answered when the notebook runs automatically, so I made the two typed answers **parameters** instead. The logic is the same, and I played it twice: once with a good name and once with `do_step`.


```python
import random

def choose_ingredient():
    return random.choice(['flour', 'sugar', 'eggs', 'milk'])

def mix(item):
    print(f"Mixing {item} into the bowl.")

def heat():
    print('Heating the oven to a friendly temperature...')

def finish():
    print('Dessert is ready!')

def play_game(name, run):
    print('Mini-game: Name a procedure for choosing an ingredient, mixing, baking, and finishing the dessert')
    print('Typed name:', name)
    if not name:
        name = 'prepare_ingredient'

    def dynamic_procedure():
        ingr = choose_ingredient()
        mix(ingr)
        heat()
        finish()

    globals()[name] = dynamic_procedure
    print(f'Created a procedure called {name}() that does multiple steps.')
    print('Good name (readable):   bake_dessert_from_random_ingredient()')
    print('Poor name (confusing):  do_step()')
    if run == 'run':
        print('Running the procedure...')
        globals()[name]()
    else:
        print('Canceled. You can run the procedure later by calling it by name.')

play_game('bake_dessert_from_random_ingredient', 'run')
print()
play_game('do_step', 'run')
```

    Mini-game: Name a procedure for choosing an ingredient, mixing, baking, and finishing the dessert
    Typed name: bake_dessert_from_random_ingredient
    Created a procedure called bake_dessert_from_random_ingredient() that does multiple steps.
    Good name (readable):   bake_dessert_from_random_ingredient()
    Poor name (confusing):  do_step()
    Running the procedure...
    Mixing flour into the bowl.
    Heating the oven to a friendly temperature...
    Dessert is ready!
    
    Mini-game: Name a procedure for choosing an ingredient, mixing, baking, and finishing the dessert
    Typed name: do_step
    Created a procedure called do_step() that does multiple steps.
    Good name (readable):   bake_dessert_from_random_ingredient()
    Poor name (confusing):  do_step()
    Running the procedure...
    Mixing flour into the bowl.
    Heating the oven to a friendly temperature...
    Dessert is ready!


**What I noticed:** both runs do exactly the same thing, but when I read `bake_dessert_from_random_ingredient()` I know what will happen before it runs. With `do_step()` I'd have to open the function to find out. The name is for the humans reading the code, not the computer.

## Exercise 1: Rename the functions to be more descriptive


```python
# Exercise 1: more descriptive names that include the key detail of each step
def bake_chocolate_cake():
    measure_two_cups_flour()
    mix_flour_sugar_and_eggs()
    bake_at_350_for_25_minutes()

def measure_two_cups_flour():
    print("Measuring 2 cups of flour.")

def mix_flour_sugar_and_eggs():
    print("Mixing flour, sugar, eggs.")

def bake_at_350_for_25_minutes():
    print("Baking at 350°F for 25 minutes.")

bake_chocolate_cake()
```

    Measuring 2 cups of flour.
    Mixing flour, sugar, eggs.
    Baking at 350°F for 25 minutes.


Now each name says **what** is happening and the important details, so a collaborator reading `bake_chocolate_cake()` knows the full recipe without opening any function.

## Exercise 2: Convert the Python functions to Java methods

```java
public class DessertRobot {

    // public: other classes (like a Kitchen or Main class) are allowed to call this
    public void makeDessert() {
        measureFlour();
        mixIngredients();
        bake();
    }

    // private: helper steps that only DessertRobot itself should call
    private void measureFlour() {
        System.out.println("Measuring 2 cups of flour.");
    }

    private void mixIngredients() {
        System.out.println("Mixing flour, sugar, eggs.");
    }

    private void bake() {
        System.out.println("Baking at 350°F for 25 minutes.");
    }

    public static void main(String[] args) {
        DessertRobot robot = new DessertRobot();
        robot.makeDessert();
    }
}
```

Output:

```text
Measuring 2 cups of flour.
Mixing flour, sugar, eggs.
Baking at 350°F for 25 minutes.
```

**Access (public vs. private):** `makeDessert()` is **public** because it is the procedure the outside world should use: "make me a dessert." `measureFlour()`, `mixIngredients()` and `bake()` are **private** because they are internal steps. Another class shouldn't be able to call `bake()` without measuring and mixing first. Making them private hides those details (abstraction) and protects the correct order of steps. Python has no enforced `private`; by convention a leading underscore (`_bake`) marks a function as internal.

## Exercise 3: Split a long procedure into smaller ones and test them

**Before:** one long procedure that does everything, which can only be checked by reading all of its printed output.


```python
def make_order_long(flour_cups, sugar_cups, eggs, oven_temp):
    print("Measuring " + str(flour_cups) + " cups of flour")
    print("Measuring " + str(sugar_cups) + " cups of sugar")
    total_cups = flour_cups + sugar_cups
    if eggs < 2:
        print("Not enough eggs!")
        return
    print("Mixing " + str(total_cups) + " cups of dry ingredients with " + str(eggs) + " eggs")
    if oven_temp < 300 or oven_temp > 400:
        print("Oven temperature unsafe!")
        return
    minutes = 25 if oven_temp >= 350 else 35
    print("Baking at " + str(oven_temp) + "°F for " + str(minutes) + " minutes")

make_order_long(2, 1, 3, 350)
```

    Measuring 2 cups of flour
    Measuring 1 cups of sugar
    Mixing 3 cups of dry ingredients with 3 eggs
    Baking at 350°F for 25 minutes


**After:** each step is its own small procedure that **returns** a value, so each one can be tested on its own with `assert`.


```python
def total_dry_cups(flour_cups, sugar_cups):
    return flour_cups + sugar_cups

def has_enough_eggs(eggs):
    return eggs >= 2

def oven_is_safe(oven_temp):
    return 300 <= oven_temp <= 400

def bake_minutes(oven_temp):
    if oven_temp >= 350:
        return 25
    return 35

def make_order(flour_cups, sugar_cups, eggs, oven_temp):
    if not has_enough_eggs(eggs):
        return "Not enough eggs!"
    if not oven_is_safe(oven_temp):
        return "Oven temperature unsafe!"
    cups = total_dry_cups(flour_cups, sugar_cups)
    return f"Mix {cups} cups with {eggs} eggs, bake at {oven_temp}°F for {bake_minutes(oven_temp)} minutes"

# Small tests for each small procedure
assert total_dry_cups(2, 1) == 3
assert has_enough_eggs(2) and not has_enough_eggs(1)
assert oven_is_safe(350) and not oven_is_safe(450) and oven_is_safe(300)
assert bake_minutes(350) == 25 and bake_minutes(325) == 35
assert make_order(2, 1, 1, 350) == "Not enough eggs!"
assert make_order(2, 1, 3, 500) == "Oven temperature unsafe!"
print("All tests passed!")
print(make_order(2, 1, 3, 350))
print(make_order(3, 2, 4, 325))
```

    All tests passed!
    Mix 3 cups with 3 eggs, bake at 350°F for 25 minutes
    Mix 5 cups with 4 eggs, bake at 325°F for 35 minutes


**Why testing got easier:** in the long version the only way to check the egg rule was to run the whole recipe and read its output. After splitting, each rule is a tiny procedure with a clear name and a return value, so one `assert` line checks it directly. When a test fails, the name of the failing procedure tells me exactly where the bug is.

## Demonstration of poor naming: fixed


```python
# The confusing do_step() from the lesson, renamed so a collaborator knows what it does
def choose_mix_heat_and_finish_dessert():
    print('Choosing ingredient...')
    print('Mixing...')
    print('Heating...')
    print('Finished!')

print('Calling choose_mix_heat_and_finish_dessert() (clear name):')
choose_mix_heat_and_finish_dessert()
```

    Calling choose_mix_heat_and_finish_dessert() (clear name):
    Choosing ingredient...
    Mixing...
    Heating...
    Finished!


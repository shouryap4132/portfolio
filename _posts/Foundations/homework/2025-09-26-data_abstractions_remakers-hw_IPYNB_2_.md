---
layout: post
codemirror: True
title: UESL 3.2 Homework
categories: ['Python']
lesson_language: Python
lesson_topic: Data-Abstraction HW
lesson_part: interactive
lesson_type: lesson
permalink: /homework/3-2/
author: Shourya Patel
---

# UESL 3.2 Data Abstraction — Homework

All parts of the 3.2 lesson are completed below: the warm-up, the graded Popcorn checkpoint, the copying check, Example C, the MCQ, the Homework Hack, both tests and the design-thinking note.

## Popcorn

### A. Warm-up · Find the level

**Prediction:** `10` (first level), `20` (second level), `3` (number of levels).



{% capture challenge0 %}
{% raw %}
UESL 3.2 Warm-up - Find the level (original, then first value changed to 14)
{% endraw %}
{% endcapture %}

{% capture code0 %}
{% raw %}
level_stars = [10, 20, 15]
print(level_stars[0])
print(level_stars[1])
print(len(level_stars))

level_stars = [14, 20, 15]      # change only the first value
print(level_stars[0])
print(level_stars[1])
print(len(level_stars))
{% endraw %}
{% endcapture %}

{% capture source0 %}
{% raw %}
```python
# CODE_RUNNER: UESL 3.2 Warm-up - Find the level (original, then first value changed to 14)
level_stars = [10, 20, 15]
print(level_stars[0])
print(level_stars[1])
print(len(level_stars))

level_stars = [14, 20, 15]      # change only the first value
print(level_stars[0])
print(level_stars[1])
print(len(level_stars))
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="homework-3-2-0"
   language="python"
   challenge=challenge0
   code=code0
   source=source0
%}


**Actual:** `10, 20, 3`, then `14, 20, 3`. Only the first output changed because I replaced one element; replacing a value does not add a level, so the length stays 3. Python index `1` and AP index `2` both select the second level.

### B. Popcorn checkpoint · Extend the level sequence

**Prediction (before running):** `level_stars[1]` is 9, plus 3 → 12. Appending 5 adds a fourth level. I predict `[6, 12, 12, 5]` and `4`.

**AP index for the same second level:** `2` (AP lists start at 1, Python at 0).



{% capture challenge1 %}
{% raw %}
UESL 3.2 Popcorn - Extend the level sequence
{% endraw %}
{% endcapture %}

{% capture code1 %}
{% raw %}
level_stars = [6, 9, 12]
level_stars[1] = level_stars[1] + 3
level_stars.append(5)
print(level_stars)
print(len(level_stars))
{% endraw %}
{% endcapture %}

{% capture source1 %}
{% raw %}
```python
# CODE_RUNNER: UESL 3.2 Popcorn - Extend the level sequence
level_stars = [6, 9, 12]
level_stars[1] = level_stars[1] + 3
level_stars.append(5)
print(level_stars)
print(len(level_stars))
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="homework-3-2-1"
   language="python"
   challenge=challenge1
   code=code1
   source=source1
%}


**Actual output:** `[6, 12, 12, 5]` and `4` — matches.

**Changed version (append 8 instead of 5):**



{% capture challenge2 %}
{% raw %}
UESL 3.2 Popcorn - Changed version, append 8
{% endraw %}
{% endcapture %}

{% capture code2 %}
{% raw %}
level_stars = [6, 9, 12]
level_stars[1] = level_stars[1] + 3
level_stars.append(8)
print(level_stars)
print(len(level_stars))
{% endraw %}
{% endcapture %}

{% capture source2 %}
{% raw %}
```python
# CODE_RUNNER: UESL 3.2 Popcorn - Changed version, append 8
level_stars = [6, 9, 12]
level_stars[1] = level_stars[1] + 3
level_stars.append(8)
print(level_stars)
print(len(level_stars))
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="homework-3-2-2"
   language="python"
   challenge=challenge2
   code=code2
   source=source2
%}


**Actual:** `[6, 12, 12, 8]`, still `4`. **Explanation:** updating an element (`level_stars[1] = ...`) replaces a value in an existing slot, so the length stays the same; `append` creates a new slot at the end, so the length grows by one.

Pseudocode version:


{% capture challenge3 %}
{% raw %}
UESL 3.2 - Shared list vs copy
{% endraw %}
{% endcapture %}

{% capture code3 %}
{% raw %}
level_stars = [10, 20, 15]
other = level_stars          # same list, two names
other[0] = 99
print("After changing other[0]:", level_stars)

level_stars = [10, 20, 15]
separate = level_stars.copy()   # separate shallow copy
separate[0] = 99
print("After changing the copy:", level_stars)
{% endraw %}
{% endcapture %}

{% capture source3 %}
{% raw %}
```text
level_stars ← [6, 9, 12]
level_stars[2] ← level_stars[2] + 3     // AP index 2 = second level
APPEND(level_stars, 5)
DISPLAY(level_stars)                    // [6, 12, 12, 5]
DISPLAY(LENGTH(level_stars))            // 4
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="homework-3-2-3"
   language="python"
   challenge=challenge3
   code=code3
   source=source3
%}


### Quick partner check · Copying

**Question:** If Python uses `other = level_stars`, does changing `other[0]` affect `level_stars`?

**My answer:** Yes — both names refer to the same list object. `.copy()` makes a separate list.



{% capture challenge4 %}
{% raw %}
UESL 3.2 - Total the level collection for three different lists
{% endraw %}
{% endcapture %}

{% capture code4 %}
{% raw %}
for level_stars in [[10, 20, 15], [10, 20, 15, 12], []]:
    total_stars = 0                       # reset before every calculation
    for stars in level_stars:
        total_stars = total_stars + stars
    print(len(level_stars))
    print(total_stars)
{% endraw %}
{% endcapture %}

{% capture source4 %}
{% raw %}
```python
# CODE_RUNNER: UESL 3.2 - Shared list vs copy
level_stars = [10, 20, 15]
other = level_stars          # same list, two names
other[0] = 99
print("After changing other[0]:", level_stars)

level_stars = [10, 20, 15]
separate = level_stars.copy()   # separate shallow copy
separate[0] = 99
print("After changing the copy:", level_stars)
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="homework-3-2-4"
   language="python"
   challenge=challenge4
   code=code4
   source=source4
%}


### C. Apply the abstraction · Total the whole game

**Prediction:** `[10, 20, 15]` → `3`, `45`; `[10, 20, 15, 12]` → `4`, `57`; `[]` → `0`, `0`.



{% capture challenge5 %}
{% raw %}
UESL 3.2 Homework - Comet Quest level collection
{% endraw %}
{% endcapture %}

{% capture code5 %}
{% raw %}
level_names = ["Launch Pad", "Asteroid Belt", "Moon Base"]   # labels so players never need indices
level_stars = [12, 18, 10]       # one star count per level, in level order

level_stars[1] = level_stars[1] + 5    # bonus of 5 on the second level
level_names.append("Comet Tail")
level_stars.append(7)                  # new fourth level

total_stars = 0
for stars in level_stars:              # Example C's traversal
    total_stars = total_stars + stars

print(level_stars)
print(len(level_stars))
print(total_stars)

for i in range(len(level_stars)):      # friendly labels for players
    print(f"Level {i + 1} - {level_names[i]}: {level_stars[i]} stars")
{% endraw %}
{% endcapture %}

{% capture source5 %}
{% raw %}
```python
# CODE_RUNNER: UESL 3.2 - Total the level collection for three different lists
for level_stars in [[10, 20, 15], [10, 20, 15, 12], []]:
    total_stars = 0                       # reset before every calculation
    for stars in level_stars:
        total_stars = total_stars + stars
    print(len(level_stars))
    print(total_stars)
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="homework-3-2-5"
   language="python"
   challenge=challenge5
   code=code5
   source=source5
%}


**Actual:** `3, 45`, `4, 57`, `0, 0`. The loop needs no new line for a fourth level because `for stars in level_stars` visits however many elements the list has — only the data changed, not the traversal.

## MCQ

| # | Question | My answer | Why |
|---|---|---|---|
| 1 | Which AP index selects the first level? | **B** 1 | AP lists start at 1. |
| 2 | Replacing one count changes the length by | **A** 0 | Replacement keeps the same number of elements. |
| 3 | `APPEND(level_stars, 5)` does | **C** Add one element with value 5 | APPEND adds one item at the end. |
| 4 | Why a list + traversal for 100 levels? | **B** Avoids a separate variable and sum edit for every level | The benefit is simpler maintenance, not guaranteed speed. |

**MCQ 3.2: 4/4 | answers: B,A,C,B**

## Homework

### Homework Hack · Grow my UESL game

`level_stars = [12, 18, 10]` — **each element is one level's collected stars, stored in level order** (element 0 is level 1, element 1 is level 2, …). This replaces the three separate variables from my 3.1 Comet Quest prototype.

**Prediction:** second level becomes 23, appending 7 adds a fourth level → `[12, 23, 10, 7]`, `4`, `52`.



{% capture challenge6 %}
{% raw %}
UESL 3.2 Tests - main collection and empty project
{% endraw %}
{% endcapture %}

{% capture code6 %}
{% raw %}
def run_test(level_stars):
    if len(level_stars) >= 2:          # only update a second level if one exists
        level_stars[1] = level_stars[1] + 5
        level_stars.append(7)
        print(level_stars)
    total_stars = 0
    for stars in level_stars:
        total_stars = total_stars + stars
    print(len(level_stars))
    print(total_stars)

print("Main test:")
run_test([12, 18, 10])   # expect [12, 23, 10, 7], 4, 52
print("Empty test:")
run_test([])             # expect 0, 0
{% endraw %}
{% endcapture %}

{% capture source6 %}
{% raw %}
```python
# CODE_RUNNER: UESL 3.2 Homework - Comet Quest level collection
level_names = ["Launch Pad", "Asteroid Belt", "Moon Base"]   # labels so players never need indices
level_stars = [12, 18, 10]       # one star count per level, in level order

level_stars[1] = level_stars[1] + 5    # bonus of 5 on the second level
level_names.append("Comet Tail")
level_stars.append(7)                  # new fourth level

total_stars = 0
for stars in level_stars:              # Example C's traversal
    total_stars = total_stars + stars

print(level_stars)
print(len(level_stars))
print(total_stars)

for i in range(len(level_stars)):      # friendly labels for players
    print(f"Level {i + 1} - {level_names[i]}: {level_stars[i]} stars")
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="homework-3-2-6"
   language="python"
   challenge=challenge6
   code=code6
   source=source6
%}


Pseudocode version of the homework:

```text
level_stars ← [12, 18, 10]
level_stars[2] ← level_stars[2] + 5
APPEND(level_stars, 7)
total_stars ← 0
FOR EACH stars IN level_stars
{
    total_stars ← total_stars + stars
}
DISPLAY(level_stars)            // [12, 23, 10, 7]
DISPLAY(LENGTH(level_stars))    // 4
DISPLAY(total_stars)            // 52
```

## Tests

Both tests start fresh. The empty test runs the **total-only** code and skips the second-level update when there is no second element.


```python
# CODE_RUNNER: UESL 3.2 Tests - main collection and empty project
def run_test(level_stars):
    if len(level_stars) >= 2:          # only update a second level if one exists
        level_stars[1] = level_stars[1] + 5
        level_stars.append(7)
        print(level_stars)
    total_stars = 0
    for stars in level_stars:
        total_stars = total_stars + stars
    print(len(level_stars))
    print(total_stars)

print("Main test:")
run_test([12, 18, 10])   # expect [12, 23, 10, 7], 4, 52
print("Empty test:")
run_test([])             # expect 0, 0
```

| Test | Prediction | Actual |
|---|---|---|
| Main `[12, 18, 10]` | `[12, 23, 10, 7]`, `4`, `52` | `[12, 23, 10, 7]`, `4`, `52` |
| Empty `[]` | `0`, `0` | `0`, `0` |

**Complexity explanation:** With 100 separate variables (`level_1_stars` … `level_100_stars`), adding a level means writing a new variable *and* editing the long total line; reordering levels means renaming variables. With a list, adding a level is one `append`, and the same 3-line loop totals 3 levels, 100 levels, or none. The list removes the per-level edits, which is where mistakes (a forgotten name, a typo) would come from.

**Connection to 3.1:** changing the list still doesn't update an old total — I have to run the traversal again.

## Design Thinking

- **Player/maker need:** A new game maker wants to add or reorder Comet Quest levels without losing track of each level's stars.
- **Goal:** One understandable collection, in level order, that I can read, update and extend.
- **Representation considered:** Separate variables (3.1) vs. a list. I also considered a single list of `["name", stars]` pairs, but kept two parallel lists so every `level_stars` element stays numeric and the addition works.
- **Prototype:** `level_stars` plus the Example C traversal, with a `level_names` list for friendly labels.
- **Test / revision:** My first empty-list test crashed with `IndexError` because it tried to add to `level_stars[1]`. I revised it to check `len(level_stars) >= 2` before updating, and the empty test now prints `0`, `0`.
- **Clear labels:** Players see "Level 2 - Asteroid Belt: 23 stars" instead of "index 1", so they never need to understand indices.

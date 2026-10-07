---
layout: post
codemirror: True
title: 3.09 Developing Algorithms HW
categories: ['Python']
lesson_language: Python
lesson_topic: Developing-Algorithms HW
lesson_part: interactive
lesson_type: lesson
permalink: /python/developing-algorithms-hw
author: Shourya Patel
---

# 3.09 Developing Algorithms — Safe Passage Heals Homework

Includes the Participation Moments, all three Popcorn Hacks (predictions + output), the MCQ result and the supply-closet Homework Hack.

## Participation 1: Program a Human Robot

My class's robot algorithm: `STAND UP` → `REPEAT UNTIL (at the corner of the table) { IF (chair in the way) { STEP around it } ELSE { STEP FORWARD 1 } }` → `TURN LEFT` → `REPEAT UNTIL (at the other side) { STEP FORWARD 1 }` → `STOP`.

- **Sequencing:** STAND UP, then the first loop, then TURN LEFT, then the second loop, then STOP, always in that order.
- **Selection:** `IF (chair in the way)`.
- **Iteration:** both `REPEAT UNTIL` loops.

## Example A check

I changed the goal to 600 in the pseudocode runner: the total is 575, so it prints "Still need $25" instead of "Goal met!"



{% capture challenge0 %}
{% raw %}
3.09 Example A - goal 500 vs goal 600
{% endraw %}
{% endcapture %}

{% capture code0 %}
{% raw %}
donations = [25, 150, 40, 100, 10, 250]
for goal in [500, 600]:
    total = 0
    for amount in donations:
        total = total + amount
    if total >= goal:
        print(f"Goal {goal}: Goal met! Safe Nights raised ${total}.")
    else:
        print(f"Goal {goal}: Still need ${goal - total} to reach the goal.")
{% endraw %}
{% endcapture %}

{% capture source0 %}
{% raw %}
```python
# CODE_RUNNER: 3.09 Example A - goal 500 vs goal 600
donations = [25, 150, 40, 100, 10, 250]
for goal in [500, 600]:
    total = 0
    for amount in donations:
        total = total + amount
    if total >= goal:
        print(f"Goal {goal}: Goal met! Safe Nights raised ${total}.")
    else:
        print(f"Goal {goal}: Still need ${goal - total} to reach the goal.")
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-developing-algorithms-hw-0"
   language="python"
   challenge=challenge0
   code=code0
   source=source0
%}


## Popcorn Hack 1: Translate pseudocode to Python



{% capture challenge1 %}
{% raw %}
3.09 Popcorn 1 - Translate the pseudocode into Python
{% endraw %}
{% endcapture %}

{% capture code1 %}
{% raw %}
# Step 1: make the hours list
hours = [3, 5, 2, 4]

# Step 2: start total at 0
total = 0

# Step 3: FOR EACH -> for ... in ...: add each h to total
for h in hours:
    total = total + h

# Step 4: LENGTH(hours) -> len(hours): compute the average
average = total / len(hours)

# Step 5: print total, then average
print(total)
print(average)
{% endraw %}
{% endcapture %}

{% capture source1 %}
{% raw %}
```python
# CODE_RUNNER: 3.09 Popcorn 1 - Translate the pseudocode into Python

# Step 1: make the hours list
hours = [3, 5, 2, 4]

# Step 2: start total at 0
total = 0

# Step 3: FOR EACH -> for ... in ...: add each h to total
for h in hours:
    total = total + h

# Step 4: LENGTH(hours) -> len(hours): compute the average
average = total / len(hours)

# Step 5: print total, then average
print(total)
print(average)
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-developing-algorithms-hw-1"
   language="python"
   challenge=challenge1
   code=code1
   source=source1
%}


Prints `14` and `3.5`, as expected.

## Example B/C check — equivalence and the one-line bug

**My prediction for Example C:** Algorithm A counts the gifts ≥ $100: 150, 100, 250 → **3**. Algorithm B also adds 1 for every donation (6 of them) → 3 + 6 = **9**.



{% capture challenge2 %}
{% raw %}
3.09 Example B + C - boundary tests and the indentation bug
{% endraw %}
{% endcapture %}

{% capture code2 %}
{% raw %}
def has_seat_a(signed_up):
    if signed_up < 12:
        return True
    else:
        return False

def has_seat_b(signed_up):
    if signed_up >= 12:
        return False
    else:
        return True

def has_seat_c(signed_up):
    return signed_up < 12

for n in [11, 12, 13]:          # below, AT, and above the limit
    print(n, has_seat_a(n), has_seat_b(n), has_seat_c(n))

donations = [25, 150, 40, 100, 10, 250]
count_a = 0
for amount in donations:
    if amount >= 100:
        count_a = count_a + 1
count_b = 0
for amount in donations:
    if amount >= 100:
        count_b = count_b + 1
    count_b = count_b + 1
print("Algorithm A counted:", count_a)
print("Algorithm B counted:", count_b)
{% endraw %}
{% endcapture %}

{% capture source2 %}
{% raw %}
```python
# CODE_RUNNER: 3.09 Example B + C - boundary tests and the indentation bug
def has_seat_a(signed_up):
    if signed_up < 12:
        return True
    else:
        return False

def has_seat_b(signed_up):
    if signed_up >= 12:
        return False
    else:
        return True

def has_seat_c(signed_up):
    return signed_up < 12

for n in [11, 12, 13]:          # below, AT, and above the limit
    print(n, has_seat_a(n), has_seat_b(n), has_seat_c(n))

donations = [25, 150, 40, 100, 10, 250]
count_a = 0
for amount in donations:
    if amount >= 100:
        count_a = count_a + 1
count_b = 0
for amount in donations:
    if amount >= 100:
        count_b = count_b + 1
    count_b = count_b + 1
print("Algorithm A counted:", count_a)
print("Algorithm B counted:", count_b)
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-developing-algorithms-hw-2"
   language="python"
   challenge=challenge2
   code=code2
   source=source2
%}


My predictions were right: A = 3, B = 9. All three seat checks agree at 11, 12 and 13, so they are equivalent.

## Popcorn Hack 2: Predict, then fix

**My prediction before running:** `1`, because `count > capacity` is False for exactly 12, so only Fitness (15) is counted.



{% capture challenge3 %}
{% raw %}
3.09 Popcorn 2 - Predict, then fix the full-workshop counter
{% endraw %}
{% endcapture %}

{% capture code3 %}
{% raw %}
signed_up = [12, 7, 15, 9]   # Self-Defense, Parenting Skills, Fitness, Self-Sufficiency
capacity = 12

# Buggy version (as given)
full = 0
for count in signed_up:
    if count > capacity:
        full = full + 1
print("Buggy - Full workshops:", full)

# Fixed version: one character, > becomes >=
full = 0
for count in signed_up:
    if count >= capacity:     # a workshop with EXACTLY 12 is full
        full = full + 1
print("Full workshops:", full)

# My prediction before running: 1 (the boundary value 12 was not counted)
{% endraw %}
{% endcapture %}

{% capture source3 %}
{% raw %}
```python
# CODE_RUNNER: 3.09 Popcorn 2 - Predict, then fix the full-workshop counter

signed_up = [12, 7, 15, 9]   # Self-Defense, Parenting Skills, Fitness, Self-Sufficiency
capacity = 12

# Buggy version (as given)
full = 0
for count in signed_up:
    if count > capacity:
        full = full + 1
print("Buggy - Full workshops:", full)

# Fixed version: one character, > becomes >=
full = 0
for count in signed_up:
    if count >= capacity:     # a workshop with EXACTLY 12 is full
        full = full + 1
print("Full workshops:", full)

# My prediction before running: 1 (the boundary value 12 was not counted)
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-developing-algorithms-hw-3"
   language="python"
   challenge=challenge3
   code=code3
   source=source3
%}


## Participation 2: Table Talk

**Are Robot A (`STEP FORWARD 5`) and Robot B (`REPEAT UNTIL (touching the table) { STEP FORWARD 1 }`) equivalent?** Only if the table is exactly 5 steps away. If it's 6 steps away A stops short while B still arrives, and if it's 3 steps away A walks into the table. One matching test doesn't prove two algorithms are equivalent; you have to test different inputs.

## Popcorn Hack 3: Modify the counter into a collector



{% capture challenge4 %}
{% raw %}
3.09 Popcorn 3 - Modify the counter into a collector
{% endraw %}
{% endcapture %}

{% capture code4 %}
{% raw %}
workshops = ["Self-Defense", "Parenting Skills", "Fitness", "Self-Sufficiency"]
signed_up = [12, 7, 15, 9]     # signed_up[0] goes with workshops[0], and so on
capacity = 12

open_workshops = []            # COLLECT names instead of counting

for i in range(len(workshops)):          # i = 0, 1, 2, 3
    # TODO 1: an if that is True when signed_up[i] < capacity
    if signed_up[i] < capacity:
        # TODO 2: append workshops[i] to open_workshops
        open_workshops.append(workshops[i])

# TODO 3: print how many there are, then the list
print("Workshops with open seats:", len(open_workshops))
print(open_workshops)
{% endraw %}
{% endcapture %}

{% capture source4 %}
{% raw %}
```python
# CODE_RUNNER: 3.09 Popcorn 3 - Modify the counter into a collector

workshops = ["Self-Defense", "Parenting Skills", "Fitness", "Self-Sufficiency"]
signed_up = [12, 7, 15, 9]     # signed_up[0] goes with workshops[0], and so on
capacity = 12

open_workshops = []            # COLLECT names instead of counting

for i in range(len(workshops)):          # i = 0, 1, 2, 3
    # TODO 1: an if that is True when signed_up[i] < capacity
    if signed_up[i] < capacity:
        # TODO 2: append workshops[i] to open_workshops
        open_workshops.append(workshops[i])

# TODO 3: print how many there are, then the list
print("Workshops with open seats:", len(open_workshops))
print(open_workshops)
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-developing-algorithms-hw-4"
   language="python"
   challenge=challenge4
   code=code4
   source=source4
%}


## Participation 3: Fastest Table

Modify Robot B so it reports how many steps it took:


{% capture challenge5 %}
{% raw %}
3.09 Homework - Safe Passage Heals supply restock report
{% endraw %}
{% endcapture %}

{% capture code5 %}
{% raw %}
def restock_report(items, in_stock, target):
    # Step 1: COLLECT items below target, and how many of each are needed
    short_items = []
    short_amounts = []
    for i in range(len(items)):
        if in_stock[i] < target[i]:              # strictly below: exactly at target is NOT short
            short_items.append(items[i])
            short_amounts.append(target[i] - in_stock[i])

    # Step 2: SUM the shortages with a loop (no sum())
    total_needed = 0
    for amount in short_amounts:
        total_needed = total_needed + amount

    # Step 3: FIND THE MAX shortage, tracking its position for the item name
    max_index = 0
    for i in range(len(short_amounts)):
        if short_amounts[i] > short_amounts[max_index]:
            max_index = i

    # Step 4: COMBINE: "Fully stocked!" if nothing is short, otherwise the report
    if len(short_items) == 0:
        print("Fully stocked!")
    else:
        print("Restock needed:")
        for i in range(len(short_items)):
            print(f"{short_items[i]}: need {short_amounts[i]}")
        print(f"Total items needed: {total_needed}")
        print(f"Most urgent: {short_items[max_index]} (short by {short_amounts[max_index]})")

# Main test (lesson data)
items    = ["Toothbrushes", "Blankets", "Socks", "Shampoo", "Notebooks"]
in_stock = [40, 8, 25, 5, 30]      # in the closet now
target   = [30, 20, 25, 15, 30]    # what staff want on hand
restock_report(items, in_stock, target)

# Edge test: everything at or above target -> "Fully stocked!"
print()
restock_report(items, [40, 20, 25, 15, 31], target)
{% endraw %}
{% endcapture %}

{% capture source5 %}
{% raw %}
```text
steps ← 0
REPEAT UNTIL (touching the table)
{
    STEP FORWARD 1
    steps ← steps + 1
}
DISPLAY(steps)
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-developing-algorithms-hw-5"
   language="python"
   challenge=challenge5
   code=code5
   source=source5
%}


The loop stays the same and only what it tracks changes. That is **modifying** an existing algorithm (AAP-2.M).

## MCQ Check

| # | Question | Answer | Why |
|---|---|---|---|
| 1 | Output of the gifts counter with the line outside the `if` | **C** 4 | 3 (every gift) + 1 (the $120 gift) |
| 2 | Which one has a side effect on the list? | **B** `top_b` | `.sort()` reorders the caller's list |
| 3 | Input that proves `< 10` and `<= 10` are not equivalent | **C** 10 | only the boundary disagrees |
| 4 | Count → collect low supplies is | **B** Modified an existing algorithm | same loop + condition, different tracking |

**MCQ 3.09: 4/4 | answers: C,B,C,B**

## Homework Hack: Supply closet restock report


```python
# CODE_RUNNER: 3.09 Homework - Safe Passage Heals supply restock report

def restock_report(items, in_stock, target):
    # Step 1: COLLECT items below target, and how many of each are needed
    short_items = []
    short_amounts = []
    for i in range(len(items)):
        if in_stock[i] < target[i]:              # strictly below: exactly at target is NOT short
            short_items.append(items[i])
            short_amounts.append(target[i] - in_stock[i])

    # Step 2: SUM the shortages with a loop (no sum())
    total_needed = 0
    for amount in short_amounts:
        total_needed = total_needed + amount

    # Step 3: FIND THE MAX shortage, tracking its position for the item name
    max_index = 0
    for i in range(len(short_amounts)):
        if short_amounts[i] > short_amounts[max_index]:
            max_index = i

    # Step 4: COMBINE: "Fully stocked!" if nothing is short, otherwise the report
    if len(short_items) == 0:
        print("Fully stocked!")
    else:
        print("Restock needed:")
        for i in range(len(short_items)):
            print(f"{short_items[i]}: need {short_amounts[i]}")
        print(f"Total items needed: {total_needed}")
        print(f"Most urgent: {short_items[max_index]} (short by {short_amounts[max_index]})")

# Main test (lesson data)
items    = ["Toothbrushes", "Blankets", "Socks", "Shampoo", "Notebooks"]
in_stock = [40, 8, 25, 5, 30]      # in the closet now
target   = [30, 20, 25, 15, 30]    # what staff want on hand
restock_report(items, in_stock, target)

# Edge test: everything at or above target -> "Fully stocked!"
print()
restock_report(items, [40, 20, 25, 15, 31], target)
```

**Output matches exactly:**

```text
Restock needed:
Blankets: need 12
Shampoo: need 10
Total items needed: 22
Most urgent: Blankets (short by 12)
```

Socks (25 of 25) is correctly **not** listed because of the boundary (`<`, not `<=`), and the second test prints `Fully stocked!`. This homework **combines** three known algorithms: collect (filter), sum, and find-the-max.

### Submission notes

```text
Lesson: CSP 3.09 Developing Algorithms
MCQ 3.09: 4/4 | answers: C,B,C,B
Popcorn Hacks 1-3 completed in class and copied to notebook: yes
Participation: Table Talk answer (Robot A vs Robot B)
Homework output: Restock needed: / Blankets: need 12 / Shampoo: need 10 / Total items needed: 22 / Most urgent: Blankets (short by 12)
```

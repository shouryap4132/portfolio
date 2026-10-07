---
layout: post
codemirror: True
title: 3.10 Lists HW
categories: ['Python']
lesson_language: Python
lesson_topic: Lists HW
lesson_part: interactive
lesson_type: lesson
permalink: /csp/big-idea-3/lists/
author: Shourya Patel
---

## Lists

Homework for Big Idea 3.10 (Shoreline Outreach theme): all three Popcorn Hacks with the fixes applied, and the Homework Task. Every cell uses explicit loops (no list comprehensions, no `sum()`).

### Popcorn Hack 1 — predict, run, fix the crash

Predictions are written as comments next to each print. The fourth line crashes with `IndexError` because Python's valid indexes are 0–3. Pseudocode `items_needed[5]` is out of range too (valid AP indexes are 1–4).



{% capture challenge0 %}
{% raw %}
Lists Popcorn 1 - predict, run, fix the crash
{% endraw %}
{% endcapture %}

{% capture code0 %}
{% raw %}
items_needed = ["blankets", "socks", "water", "meals"]

print(items_needed[0])                     # prediction: blankets   (AP items_needed[1])
print(items_needed[len(items_needed) - 1]) # prediction: meals      (AP items_needed[LENGTH(items_needed)])
print(len(items_needed))                   # prediction: 4

# Original translation of DISPLAY(items_needed[5]) -> crashes
try:
    print(items_needed[4])                 # prediction: IndexError
except IndexError as error:
    print("IndexError:", error)

# Part 2 fix: the last valid Python index is 3 (AP index 4)
print(items_needed[3])                     # prediction: meals
{% endraw %}
{% endcapture %}

{% capture source0 %}
{% raw %}
```python
# CODE_RUNNER: Lists Popcorn 1 - predict, run, fix the crash
items_needed = ["blankets", "socks", "water", "meals"]

print(items_needed[0])                     # prediction: blankets   (AP items_needed[1])
print(items_needed[len(items_needed) - 1]) # prediction: meals      (AP items_needed[LENGTH(items_needed)])
print(len(items_needed))                   # prediction: 4

# Original translation of DISPLAY(items_needed[5]) -> crashes
try:
    print(items_needed[4])                 # prediction: IndexError
except IndexError as error:
    print("IndexError:", error)

# Part 2 fix: the last valid Python index is 3 (AP index 4)
print(items_needed[3])                     # prediction: meals
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="csp-big-idea-3-lists-0"
   language="python"
   challenge=challenge0
   code=code0
   source=source0
%}


**Why the fix works:** Python indexes 0 through `len - 1` = 3, so `items_needed[3]` is the last item. In the pseudocode version the equivalent fix is `items_needed[4]`, because AP indexes 1 through 4.

### Popcorn Hack 2 — volunteer hours accumulator



{% capture challenge1 %}
{% raw %}
Lists Popcorn 2
{% endraw %}
{% endcapture %}

{% capture code1 %}
{% raw %}
def report_hours(volunteer_hours):
    if len(volunteer_hours) == 0:          # guard: avoid ZeroDivisionError
        print("No data yet")
        return
    total = 0                               # 1. initialize before the loop
    for hours in volunteer_hours:           # 2. add each element inside the loop
        total += hours
    average = total / len(volunteer_hours)  # 3. use the total after the loop
    print("Total volunteer hours:", total)
    print("Average volunteer hours:", average)

report_hours([7, 6, 8, 5, 7, 9])   # expected 42 and 7.0
report_hours([])                   # expected "No data yet"
{% endraw %}
{% endcapture %}

{% capture source1 %}
{% raw %}
```python
# CODE_RUNNER: Lists Popcorn 2
def report_hours(volunteer_hours):
    if len(volunteer_hours) == 0:          # guard: avoid ZeroDivisionError
        print("No data yet")
        return
    total = 0                               # 1. initialize before the loop
    for hours in volunteer_hours:           # 2. add each element inside the loop
        total += hours
    average = total / len(volunteer_hours)  # 3. use the total after the loop
    print("Total volunteer hours:", total)
    print("Average volunteer hours:", average)

report_hours([7, 6, 8, 5, 7, 9])   # expected 42 and 7.0
report_hours([])                   # expected "No data yet"
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="csp-big-idea-3-lists-1"
   language="python"
   challenge=challenge1
   code=code1
   source=source1
%}


### Popcorn Hack 3 — count then filter

I used a class survey of items people said they would donate.



{% capture challenge2 %}
{% raw %}
Lists Popcorn 3 - count then filter
{% endraw %}
{% endcapture %}

{% capture code2 %}
{% raw %}
items_requested = ["blankets", "socks", "meals", "socks", "water", "socks", "meals",
                   "toothpaste", "blankets", "hygiene kits", "socks"]   # class survey responses

frequency = {}
for item in items_requested:
    if item in frequency:
        frequency[item] += 1
    else:
        frequency[item] = 1

print(frequency)

# 1. Build a list of items with 2 or more votes
popular = []
for item in frequency:
    if frequency[item] >= 2:
        popular.append(item)

# 2. Print that list
print(popular)
print("Responses:", len(items_requested), "| sum of counts:", sum(frequency.values()))
{% endraw %}
{% endcapture %}

{% capture source2 %}
{% raw %}
```python
# CODE_RUNNER: Lists Popcorn 3 - count then filter

items_requested = ["blankets", "socks", "meals", "socks", "water", "socks", "meals",
                   "toothpaste", "blankets", "hygiene kits", "socks"]   # class survey responses

frequency = {}
for item in items_requested:
    if item in frequency:
        frequency[item] += 1
    else:
        frequency[item] = 1

print(frequency)

# 1. Build a list of items with 2 or more votes
popular = []
for item in frequency:
    if frequency[item] >= 2:
        popular.append(item)

# 2. Print that list
print(popular)
print("Responses:", len(items_requested), "| sum of counts:", sum(frequency.values()))
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="csp-big-idea-3-lists-2"
   language="python"
   challenge=challenge2
   code=code2
   source=source2
%}


The counts add up to the number of responses (11), and the filtered list (`socks`, `meals`, `blankets`) is shorter than the number of unique items (6) because not every item got 2 votes.

Pseudocode for the filter I added:


{% capture challenge3 %}
{% raw %}
Lists Homework - indexing, accumulator, count and filter on one dataset
{% endraw %}
{% endcapture %}

{% capture code3 %}
{% raw %}
donations_by_item = ["blankets", "socks", "blankets", "water", "socks", "blankets",
                      "meals", "socks", "blankets", "water", "blankets", "socks"]

costs = [2, 3, 2, 4, 3, 2, 1, 3, 2, 4, 2, 3]

# LESSON 1 - indexing
# 1. How many donations were made
print(len(donations_by_item))
# 2. The last donation, using len() - 1 (not a hardcoded index)
print(donations_by_item[len(donations_by_item) - 1])

# LESSON 2 - sum and average
# 3. Total costs with a loop (no sum())
total = 0
for cost in costs:
    total += cost
# 4. Print total and average as integers
average = total / len(costs)
print("Total: " + str(int(total)))
print("Average: " + str(int(average)))

# LESSON 3 - count and filter
# 5. Frequency dictionary
frequency = {}
for item in donations_by_item:
    if item in frequency:
        frequency[item] += 1
    else:
        frequency[item] = 1
print(frequency)

# 6. Items with 3 or more donations (new list; original list untouched)
top_items = []
for item in frequency:
    if frequency[item] >= 3:
        top_items.append(item)
print(top_items)
{% endraw %}
{% endcapture %}

{% capture source3 %}
{% raw %}
```text
popular ← []
FOR EACH item IN frequency
{
  IF (frequency[item] ≥ 2)
  {
    APPEND(popular, item)
  }
}
DISPLAY(popular)
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="csp-big-idea-3-lists-3"
   language="python"
   challenge=challenge3
   code=code3
   source=source3
%}


### Homework — indexing, accumulator, count and filter on one dataset


```python
# CODE_RUNNER: Lists Homework - indexing, accumulator, count and filter on one dataset

donations_by_item = ["blankets", "socks", "blankets", "water", "socks", "blankets",
                      "meals", "socks", "blankets", "water", "blankets", "socks"]

costs = [2, 3, 2, 4, 3, 2, 1, 3, 2, 4, 2, 3]

# LESSON 1 - indexing
# 1. How many donations were made
print(len(donations_by_item))
# 2. The last donation, using len() - 1 (not a hardcoded index)
print(donations_by_item[len(donations_by_item) - 1])

# LESSON 2 - sum and average
# 3. Total costs with a loop (no sum())
total = 0
for cost in costs:
    total += cost
# 4. Print total and average as integers
average = total / len(costs)
print("Total: " + str(int(total)))
print("Average: " + str(int(average)))

# LESSON 3 - count and filter
# 5. Frequency dictionary
frequency = {}
for item in donations_by_item:
    if item in frequency:
        frequency[item] += 1
    else:
        frequency[item] = 1
print(frequency)

# 6. Items with 3 or more donations (new list; original list untouched)
top_items = []
for item in frequency:
    if frequency[item] >= 3:
        top_items.append(item)
print(top_items)
```

The output matches the expected shape exactly:

```text
12
socks
Total: 31
Average: 2
{'blankets': 5, 'socks': 4, 'water': 2, 'meals': 1}
['blankets', 'socks']
```

**Checklist:** `total = 0` before the loop ✔ · empty `{}` before counting ✔ · empty `[]` before filtering ✔ · no `sum()` or list comprehensions in the homework ✔ · last element found with `len() - 1` ✔ · `donations_by_item` not modified ✔

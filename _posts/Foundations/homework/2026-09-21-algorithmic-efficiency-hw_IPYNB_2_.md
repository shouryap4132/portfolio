---
layout: post
codemirror: True
title: Library 3.17 Algorithmic Efficiency Homework
categories: ['Python']
lesson_language: Python
lesson_topic: Algorithmic-Efficiency HW
lesson_part: interactive
lesson_type: lesson
permalink: /homework/3-17/
author: Shourya Patel
---

# 3.17 Algorithmic Efficiency — Librarian Homework

Sections: Popcorn, MCQ, Homework, Tests, Design Thinking. The warm-up, partner checks, and the heuristic question are answered too.

## Popcorn

### A. Warm-up · Find the book (practice)

**Prediction for book 15:** linear 5, binary 3, saved 2. **For book 3:** linear 1; binary checks 12, then 6, then 3, so 3 checks. That gives `1, 3, -2`.



{% capture challenge0 %}
{% raw %}
Library 3.17 Warm-up - book 15, then book 3
{% endraw %}
{% endcapture %}

{% capture code0 %}
{% raw %}
for target, linear_checks, binary_checks in [(15, 5, 3), (3, 1, 3)]:
    print("Target book", target)
    print(linear_checks)
    print(binary_checks)
    print(linear_checks - binary_checks)
{% endraw %}
{% endcapture %}

{% capture source0 %}
{% raw %}
```python
# CODE_RUNNER: Library 3.17 Warm-up - book 15, then book 3
for target, linear_checks, binary_checks in [(15, 5, 3), (3, 1, 3)]:
    print("Target book", target)
    print(linear_checks)
    print(binary_checks)
    print(linear_checks - binary_checks)
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="homework-3-17-0"
   language="python"
   challenge=challenge0
   code=code0
   source=source0
%}


For book 3, **linear search wins** (1 check vs 3). One easy case doesn't describe every search. Both methods are correct; they just do different amounts of work depending on where the target is.

To double-check the hand counts, I wrote both searches and counted the checks they actually make:



{% capture challenge1 %}
{% raw %}
Verify the hand counts with real searches
{% endraw %}
{% endcapture %}

{% capture code1 %}
{% raw %}
catalog = [3, 6, 9, 12, 15, 18, 21]

def linear_search(items, target):
    checks = 0
    for item in items:
        checks += 1
        if item == target:
            return checks
    return checks

def binary_search(items, target):
    low, high, checks = 0, len(items) - 1, 0
    while low <= high:
        mid = (low + high) // 2
        checks += 1
        if items[mid] == target:
            return checks
        elif items[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    return checks

for target in [15, 3, 21, 10]:
    print(f"book {target}: linear {linear_search(catalog, target)} checks, binary {binary_search(catalog, target)} checks")
{% endraw %}
{% endcapture %}

{% capture source1 %}
{% raw %}
```python
# CODE_RUNNER: Verify the hand counts with real searches
catalog = [3, 6, 9, 12, 15, 18, 21]

def linear_search(items, target):
    checks = 0
    for item in items:
        checks += 1
        if item == target:
            return checks
    return checks

def binary_search(items, target):
    low, high, checks = 0, len(items) - 1, 0
    while low <= high:
        mid = (low + high) // 2
        checks += 1
        if items[mid] == target:
            return checks
        elif items[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    return checks

for target in [15, 3, 21, 10]:
    print(f"book {target}: linear {linear_search(catalog, target)} checks, binary {binary_search(catalog, target)} checks")
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="homework-3-17-1"
   language="python"
   challenge=challenge1
   code=code1
   source=source1
%}


Book 10 isn't in the catalog. Linear search has to check all 7 entries (its worst case), while binary search needs only 3.

### B. Popcorn checkpoint · Expand the catalog (graded)

**Prediction:** for 8 books, linear worst case 8 and binary worst case 4. For 16 books, linear **doubles** to 16 and binary goes up **by one** to 5.



{% capture challenge2 %}
{% raw %}
Library 3.17 Popcorn - Expand the catalog (n = 8, then edited to n = 16)
{% endraw %}
{% endcapture %}

{% capture code2 %}
{% raw %}
import math

for n in [8, 16]:
    linear_checks = n
    binary_checks = 0 if n == 0 else math.floor(math.log2(n)) + 1
    print(n)
    print(linear_checks)
    print(binary_checks)
{% endraw %}
{% endcapture %}

{% capture source2 %}
{% raw %}
```python
# CODE_RUNNER: Library 3.17 Popcorn - Expand the catalog (n = 8, then edited to n = 16)
import math

for n in [8, 16]:
    linear_checks = n
    binary_checks = 0 if n == 0 else math.floor(math.log2(n)) + 1
    print(n)
    print(linear_checks)
    print(binary_checks)
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="homework-3-17-2"
   language="python"
   challenge=challenge2
   code=code2
   source=source2
%}


**Actual output:** `8, 8, 4` then `16, 16, 5`. That matches my prediction.

**Recommendation:** for a large **sorted** catalog, use binary search. Its worst-case work grows by only one check each time the catalog doubles, while linear search's work doubles.

### Heuristic partner check

Choosing short books first builds a reading list quickly and fits a lot of books into the time budget, but short books aren't necessarily the most enjoyable, so it can miss the best combination. Checking every possible selection guarantees the best list, but 10 books means 2¹⁰ = 1,024 selections and 20 books means 1,048,576, which is exponential growth.

### C. Compare growth (Example C)



{% capture challenge3 %}
{% raw %}
Library 3.17 - Compare catalog growth for n = 10, 20, 0
{% endraw %}
{% endcapture %}

{% capture code3 %}
{% raw %}
for n in [10, 20, 0]:
    visits = n
    pairs = n * n
    print(n)
    print(visits)
    print(pairs)
{% endraw %}
{% endcapture %}

{% capture source3 %}
{% raw %}
```python
# CODE_RUNNER: Library 3.17 - Compare catalog growth for n = 10, 20, 0
for n in [10, 20, 0]:
    visits = n
    pairs = n * n
    print(n)
    print(visits)
    print(pairs)
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="homework-3-17-3"
   language="python"
   challenge=challenge3
   code=code3
   source=source3
%}


`10, 10, 100` → `20, 20, 400` → `0, 0, 0`. Doubling n doubles the visits (linear) but multiplies pairs by 4 (quadratic), because `(2n) × (2n) = 4n²`.

## MCQ

| # | Question | Answer |
|---|---|---|
| 1 | Binary search requires | **A** a sorted catalog with direct access to entries |
| 2 | Compare two correct searches by | **B** work and memory as input grows |
| 3 | Quadratic: 100 checks at n = 10 → n = 20 | **B** 400 |
| 4 | Short-books-first heuristic | **C** can be useful without guaranteeing the best list |

**MCQ 3.17: 4/4 | answers: A,B,B,C**

## Homework

### Homework Hack · Advise the librarian

**Predictions:** n = 12 → `12, 12, 144`; n = 24 → `24, 24, 576`; n = 0 → `0, 0, 0`.



{% capture challenge4 %}
{% raw %}
Library 3.17 Homework - labeled growth calculator
{% endraw %}
{% endcapture %}

{% capture code4 %}
{% raw %}
def growth_report(n):
    visits = n
    pairs = n * n
    print("Books in catalog:", n)
    print("Visits to scan every book once:", visits)
    print("Ordered pairs to compare every book with every book:", pairs)
    print()

growth_report(12)   # main
growth_report(24)   # doubled
{% endraw %}
{% endcapture %}

{% capture source4 %}
{% raw %}
```python
# CODE_RUNNER: Library 3.17 Homework - labeled growth calculator
def growth_report(n):
    visits = n
    pairs = n * n
    print("Books in catalog:", n)
    print("Visits to scan every book once:", visits)
    print("Ordered pairs to compare every book with every book:", pairs)
    print()

growth_report(12)   # main
growth_report(24)   # doubled
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="homework-3-17-4"
   language="python"
   challenge=challenge4
   code=code4
   source=source4
%}


**Growth explanation:** going from 12 to 24 books **doubles** the visits (12 → 24) but **quadruples** the pairs (144 → 576 = 4 × 144). Scanning is linear work; comparing every pair is quadratic work, so the pair task becomes expensive much faster as the library grows.

### Search recommendation for 1,000 books



{% capture challenge5 %}
{% raw %}
Library 3.17 Homework - checkpoint B for 1,000 books
{% endraw %}
{% endcapture %}

{% capture code5 %}
{% raw %}
import math

n = 1000
linear_checks = n
binary_checks = 0 if n == 0 else math.floor(math.log2(n)) + 1
print("Books:", n)
print("Linear search, worst-case checks:", linear_checks)
print("Binary search, worst-case checks:", binary_checks)
{% endraw %}
{% endcapture %}

{% capture source5 %}
{% raw %}
```python
# CODE_RUNNER: Library 3.17 Homework - checkpoint B for 1,000 books
import math

n = 1000
linear_checks = n
binary_checks = 0 if n == 0 else math.floor(math.log2(n)) + 1
print("Books:", n)
print("Linear search, worst-case checks:", linear_checks)
print("Binary search, worst-case checks:", binary_checks)
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="homework-3-17-5"
   language="python"
   challenge=challenge5
   code=code5
   source=source5
%}


**Recommendation:** for **repeated searches of an already sorted catalog**, use **binary search**: at most 10 checks per search instead of up to 1,000.

**If the catalog is unsorted:** binary search doesn't work until the catalog is sorted, and sorting costs extra work. For a single search of an unsorted catalog, linear search (at most 1,000 checks) is cheaper than sorting first. For many repeated searches, it's worth paying to sort once, because each later search then costs about 10 checks.

**If I must keep an extra sorted copy:** that is a **time/memory trade-off**. Each search gets faster, but the library needs roughly twice the storage for the catalog, and the copy has to be kept updated whenever books are added or removed.

## Tests

Each test starts fresh with only `n` changed.



{% capture challenge6 %}
{% raw %}
Library 3.17 Tests - main and empty catalog
{% endraw %}
{% endcapture %}

{% capture code6 %}
{% raw %}
for n in [12, 0]:
    visits = n
    pairs = n * n
    print(f"n={n}: visits={visits}, pairs={pairs}")
{% endraw %}
{% endcapture %}

{% capture source6 %}
{% raw %}
```python
# CODE_RUNNER: Library 3.17 Tests - main and empty catalog
for n in [12, 0]:
    visits = n
    pairs = n * n
    print(f"n={n}: visits={visits}, pairs={pairs}")
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="homework-3-17-6"
   language="python"
   challenge=challenge6
   code=code6
   source=source6
%}


| Test | Prediction | Actual output |
|---|---|---|
| Main (n = 12) | 12, 12, 144 | 12, 12, 144 |
| Doubled (n = 24) | 24, 24, 576 | 24, 24, 576 |
| Empty (n = 0) | 0, 0, 0 | 0, 0, 0 |

**Connection to the warm-up:** binary search has better worst-case growth, but for book 3 it still used more checks than linear search. Correctness, individual cases and growth are three separate questions.

## Design Thinking

- **Librarian need:** find a book quickly, even when the catalog has thousands of entries, without needing to understand formulas.
- **Goal:** recommend the search method that does the least work as the catalog grows, and explain what it requires.
- **Methods considered:** linear search (works on any catalog, and work grows with n), binary search (needs a sorted catalog, and work grows by one per doubling), and keeping an extra sorted copy (faster searches but more memory).
- **Prototype:** the labeled growth calculator and checkpoint-B calculator above, plus real `linear_search` / `binary_search` functions that count checks.
- **Test / revision:** my first calculator only printed bare numbers (`12`, `12`, `144`), which a librarian couldn't interpret. I revised it to print labels like "Visits to scan every book once" and re-ran it. The output now explains itself. I also added real search functions after noticing that my hand count for book 3 needed checking, and they confirmed the counts.

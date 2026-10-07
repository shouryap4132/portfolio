---
layout: post
codemirror: True
title: 3.15 Random Values HW
categories: ['Python']
lesson_language: Python
lesson_topic: Random-Values HW
lesson_part: interactive
lesson_type: lesson
permalink: /python/random-hw
author: Shourya Patel
---

# 3.15 Random Values — SFI Backend QA Homework

All three Popcorn Hacks, the MCQ result, the pseudocode check, and the QA simulator homework with multiple test runs.

## Popcorn Hack 1: Random SFI Record Number

**Prediction:** each run prints a record number from 1 to 4 (both endpoints included), and repeats are allowed.



{% capture challenge0 %}
{% raw %}
Popcorn Hack 1 - Random SFI Record Number
{% endraw %}
{% endcapture %}

{% capture code0 %}
{% raw %}
import random

record_count = 4

picks = []
for run in range(10):
    record_id = random.randint(1, record_count)     # 1 through record_count, inclusive
    picks.append(record_id)
    print("Run", run + 1, "-> SFI record selected for QA:", record_id)

print("All picks valid:", min(picks) >= 1 and max(picks) <= record_count)
print("Possible outputs:", list(range(1, record_count + 1)))
{% endraw %}
{% endcapture %}

{% capture source0 %}
{% raw %}
```python
# CODE_RUNNER: Popcorn Hack 1 - Random SFI Record Number

import random

record_count = 4

picks = []
for run in range(10):
    record_id = random.randint(1, record_count)     # 1 through record_count, inclusive
    picks.append(record_id)
    print("Run", run + 1, "-> SFI record selected for QA:", record_id)

print("All picks valid:", min(picks) >= 1 and max(picks) <= record_count)
print("Possible outputs:", list(range(1, record_count + 1)))
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-random-hw-0"
   language="python"
   challenge=challenge0
   code=code0
   source=source0
%}


**Why repeats are allowed:** every call to `randint` is independent. It doesn't remember earlier picks, so the same record can come up twice in a row. That's normal random behavior, not a bug. All four records are reachable because `randint(1, 4)` includes both 1 and 4. Using `randint(0, 4)` would be a bug, since there is no record 0.

## Popcorn Hack 2: Random Structured SFI Car Part



{% capture challenge1 %}
{% raw %}
Popcorn Hack 2 - Random SFI Part Record
{% endraw %}
{% endcapture %}

{% capture code1 %}
{% raw %}
import random

parts = [
    {"product_name": "Replacement Flywheels and Clutch Assemblies", "category": "Auto Racing", "spec_number": "1.1"},
    {"product_name": "Multiple Disc Clutch Assemblies", "category": "Drag Racing", "spec_number": "1.2"},
    {"product_name": "Racing Flywheel Record", "category": "Auto Racing", "spec_number": "2.1"}
]

for run in range(3):
    selected = random.choice(parts)      # choose the WHOLE record, so fields stay together
    print(f"Run {run + 1}: {selected['product_name']} | {selected['category']} | Spec {selected['spec_number']}")
{% endraw %}
{% endcapture %}

{% capture source1 %}
{% raw %}
```python
# CODE_RUNNER: Popcorn Hack 2 - Random SFI Part Record

import random

parts = [
    {"product_name": "Replacement Flywheels and Clutch Assemblies", "category": "Auto Racing", "spec_number": "1.1"},
    {"product_name": "Multiple Disc Clutch Assemblies", "category": "Drag Racing", "spec_number": "1.2"},
    {"product_name": "Racing Flywheel Record", "category": "Auto Racing", "spec_number": "2.1"}
]

for run in range(3):
    selected = random.choice(parts)      # choose the WHOLE record, so fields stay together
    print(f"Run {run + 1}: {selected['product_name']} | {selected['category']} | Spec {selected['spec_number']}")
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-random-hw-1"
   language="python"
   challenge=challenge1
   code=code1
   source=source1
%}


Choosing the whole dictionary keeps the product name, category and spec number together. If I had picked a random name, a random category and a random spec **separately**, I could get a record that doesn't exist, like "Multiple Disc Clutch Assemblies | Auto Racing | Spec 2.1."

## Popcorn Hack 3: Random SFI API Test

**Two possible outcomes I predicted:** `GET/search` → "Found record …", and `POST/create` on spec 1.1 → rejected as a duplicate.



{% capture challenge2 %}
{% raw %}
Popcorn Hack 3 - Random SFI API Test
{% endraw %}
{% endcapture %}

{% capture code2 %}
{% raw %}
import random

parts = [
    {"product_name": "Replacement Flywheels", "spec_number": "1.1"},
    {"product_name": "Multiple Disc Clutch Assemblies", "spec_number": "1.2"},
    {"product_name": "Racing Flywheel Record", "spec_number": "2.1"}
]

actions = ["GET/search", "POST/create", "PUT/update"]
existing_specs = ["1.1", "2.1"]

for run in range(6):
    part = random.choice(parts)
    action = random.choice(actions)
    if action == "GET/search":
        result = "200 OK - found " + part["product_name"]
    elif action == "POST/create":
        if part["spec_number"] in existing_specs:
            result = "409 Conflict - spec " + part["spec_number"] + " already exists"
        else:
            result = "201 Created - " + part["product_name"]
    else:
        result = "200 OK - updated spec " + part["spec_number"]
    print(f"Test {run + 1}: {action:12} {part['spec_number']} -> {result}")
{% endraw %}
{% endcapture %}

{% capture source2 %}
{% raw %}
```python
# CODE_RUNNER: Popcorn Hack 3 - Random SFI API Test

import random

parts = [
    {"product_name": "Replacement Flywheels", "spec_number": "1.1"},
    {"product_name": "Multiple Disc Clutch Assemblies", "spec_number": "1.2"},
    {"product_name": "Racing Flywheel Record", "spec_number": "2.1"}
]

actions = ["GET/search", "POST/create", "PUT/update"]
existing_specs = ["1.1", "2.1"]

for run in range(6):
    part = random.choice(parts)
    action = random.choice(actions)
    if action == "GET/search":
        result = "200 OK - found " + part["product_name"]
    elif action == "POST/create":
        if part["spec_number"] in existing_specs:
            result = "409 Conflict - spec " + part["spec_number"] + " already exists"
        else:
            result = "201 Created - " + part["product_name"]
    else:
        result = "200 OK - updated spec " + part["spec_number"]
    print(f"Test {run + 1}: {action:12} {part['spec_number']} -> {result}")
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-random-hw-2"
   language="python"
   challenge=challenge2
   code=code2
   source=source2
%}


## MCQ

| # | Question | Answer |
|---|---|---|
| 1 | Values from `random.randint(2, 5)` | **C** 2, 3, 4, 5 |
| 2 | Record A appears twice in a row | **B** Repeats are allowed in random selection |
| 3 | Python match for `RANDOM(1, 4)` | **B** `random.randint(1, 4)` |
| 4 | Why is one test run insufficient? | **B** One run may show only one of many possible outcomes |

**MCQ 3.15: 4/4 | answers: C,B,B,B**

## Pseudocode Check

I picked `recordIndex = 2` and `actionNumber = 3` and traced by hand. `selectedPart ← parts[2]` is the **second** record (Multiple Disc Clutch, spec 1.2), because AP lists start at 1. `actionNumber = 1` is false, `= 2` is false, and `= 3` is true, so it displays **"PUT/update"**. In Python the same record is `parts[1]`. With 3 records and 4 actions there are 3 × 4 = **12** possible pairs.

## Homework Hack: SFI Backend QA Simulator



{% capture challenge3 %}
{% raw %}
Homework Hack - SFI Backend QA Simulator
{% endraw %}
{% endcapture %}

{% capture code3 %}
{% raw %}
import random

parts = [
    {"product_name": "Replacement Flywheels", "category": "Auto Racing", "spec_number": "1.1"},
    {"product_name": "Multiple Disc Clutch Assemblies", "category": "Drag Racing", "spec_number": "1.2"},
    {"product_name": "Racing Flywheel Record", "category": "Auto Racing", "spec_number": "2.1"}
]

actions = ["GET/search", "POST/create", "PUT/update", "DELETE/remove"]

def run_qa(test_count, existing_spec_numbers):
    """Run test_count random record/action pairs against a simulated backend."""
    database = list(existing_spec_numbers)      # copy so each simulation starts fresh
    actions_seen = []
    print(f"Starting QA with specs in database: {database}")
    for test in range(1, test_count + 1):
        part = random.choice(parts)
        action = random.choice(actions)
        spec = part["spec_number"]
        stored = spec in database

        if action == "GET/search":
            result = "200 OK - found" if stored else "404 Not Found"
        elif action == "POST/create":
            if stored:
                result = "409 Conflict - duplicate spec, not created"
            else:
                database.append(spec)
                result = "201 Created"
        elif action == "PUT/update":
            result = "200 OK - updated" if stored else "404 Not Found - nothing to update"
        else:  # DELETE/remove
            if stored:
                database.remove(spec)
                result = "204 Removed"
            else:
                result = "404 Not Found - nothing to remove"

        if action not in actions_seen:
            actions_seen.append(action)
        print(f"Test {test}: {action:14} | {part['product_name']} (spec {spec}) -> {result}")

    print(f"Final database specs: {database}")
    print(f"Actions exercised: {len(actions_seen)} of {len(actions)} -> {actions_seen}")
    print()

existing_spec_numbers = ["1.1", "2.1"]
test_count = 5

run_qa(test_count, existing_spec_numbers)   # required 5-test run
run_qa(test_count, existing_spec_numbers)   # repeat: results differ run to run
run_qa(20, existing_spec_numbers)           # longer run exercises more paths
{% endraw %}
{% endcapture %}

{% capture source3 %}
{% raw %}
```python
# CODE_RUNNER: Homework Hack - SFI Backend QA Simulator

import random

parts = [
    {"product_name": "Replacement Flywheels", "category": "Auto Racing", "spec_number": "1.1"},
    {"product_name": "Multiple Disc Clutch Assemblies", "category": "Drag Racing", "spec_number": "1.2"},
    {"product_name": "Racing Flywheel Record", "category": "Auto Racing", "spec_number": "2.1"}
]

actions = ["GET/search", "POST/create", "PUT/update", "DELETE/remove"]

def run_qa(test_count, existing_spec_numbers):
    """Run test_count random record/action pairs against a simulated backend."""
    database = list(existing_spec_numbers)      # copy so each simulation starts fresh
    actions_seen = []
    print(f"Starting QA with specs in database: {database}")
    for test in range(1, test_count + 1):
        part = random.choice(parts)
        action = random.choice(actions)
        spec = part["spec_number"]
        stored = spec in database

        if action == "GET/search":
            result = "200 OK - found" if stored else "404 Not Found"
        elif action == "POST/create":
            if stored:
                result = "409 Conflict - duplicate spec, not created"
            else:
                database.append(spec)
                result = "201 Created"
        elif action == "PUT/update":
            result = "200 OK - updated" if stored else "404 Not Found - nothing to update"
        else:  # DELETE/remove
            if stored:
                database.remove(spec)
                result = "204 Removed"
            else:
                result = "404 Not Found - nothing to remove"

        if action not in actions_seen:
            actions_seen.append(action)
        print(f"Test {test}: {action:14} | {part['product_name']} (spec {spec}) -> {result}")

    print(f"Final database specs: {database}")
    print(f"Actions exercised: {len(actions_seen)} of {len(actions)} -> {actions_seen}")
    print()

existing_spec_numbers = ["1.1", "2.1"]
test_count = 5

run_qa(test_count, existing_spec_numbers)   # required 5-test run
run_qa(test_count, existing_spec_numbers)   # repeat: results differ run to run
run_qa(20, existing_spec_numbers)           # longer run exercises more paths
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-random-hw-3"
   language="python"
   challenge=challenge3
   code=code3
   source=source3
%}


**What the simulator shows:**

- The record and the action are picked independently each test, so any of the 3 × 4 = 12 pairs is possible and repeats are normal.
- **Duplicate-spec handling:** `POST/create` on a spec already in the database returns `409 Conflict` and isn't added again. Creating a new spec (1.2) adds it, and a later create of 1.2 is then rejected.
- `DELETE` removes a spec, so a later `GET` on it returns `404`. The simulator keeps a realistic state instead of accepting impossible actions.
- The five-test run might not hit every action, which is why I also ran a 20-test simulation. As MCQ 4 says, one short run doesn't prove every path works. The "Actions exercised" line shows how many paths each run covered.
- Every random pick is always valid, because `random.choice` only chooses from items that exist in the list.

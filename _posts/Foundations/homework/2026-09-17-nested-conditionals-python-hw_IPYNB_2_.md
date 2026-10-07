---
layout: post
codemirror: True
title: 3.07 Nested Conditionals HW
categories: ['Python']
lesson_language: Python
lesson_topic: Nested-Conditionals HW
lesson_part: interactive
lesson_type: lesson
permalink: /python/nested-conditionals-hw
author: Shourya Patel
---

# 3.07 Nested Conditionals — Student Life Homework

All three Popcorn Hacks and the Homework Hack (daily routine dashboard), with every path tested.

## Popcorn Hack 1: After-School Homework Plan

1. **Message that prints** (with `is_weekday = True`, `homework_finished = False`): **"Finish homework"**.
2. **Branches followed:** outer branch = `if is_weekday` (True); inner branch = the inner `else` (because `homework_finished` is False).
3. **Other outcomes** — tested below by changing the values.



{% capture challenge0 %}
{% raw %}
Popcorn Hack 1 - Test the after-school homework plan
{% endraw %}
{% endcapture %}

{% capture code0 %}
{% raw %}
def after_school(is_weekday, homework_finished):
    if is_weekday:
        if homework_finished:
            print("Free time")
        else:
            print("Finish homework")
    else:
        print("Weekend plan")

after_school(True, False)    # original values -> Finish homework
after_school(True, True)     # -> Free time
after_school(False, False)   # -> Weekend plan (inner check is skipped entirely)
{% endraw %}
{% endcapture %}

{% capture source0 %}
{% raw %}
```python
# CODE_RUNNER: Popcorn Hack 1 - Test the after-school homework plan

def after_school(is_weekday, homework_finished):
    if is_weekday:
        if homework_finished:
            print("Free time")
        else:
            print("Finish homework")
    else:
        print("Weekend plan")

after_school(True, False)    # original values -> Finish homework
after_school(True, True)     # -> Free time
after_school(False, False)   # -> Weekend plan (inner check is skipped entirely)
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-nested-conditionals-hw-0"
   language="python"
   challenge=challenge0
   code=code0
   source=source0
%}


## Popcorn Hack 2: Repair the Student Account Check

**Why the original isn't nested:** `if has_permission:` starts at the same indentation as `if logged_in:`, so it is a separate, independent decision. It runs even for a student who is **not** logged in, which could print "Page opened" to someone who never logged in.

**Fixed:** the permission check is indented inside the logged-in branch and an outer `else` was added.



{% capture challenge1 %}
{% raw %}
Popcorn Hack 2 - Repair the student account check
{% endraw %}
{% endcapture %}

{% capture code1 %}
{% raw %}
def open_page(logged_in, has_permission):
    if logged_in:
        print("Account found")
        if has_permission:
            print("Page opened")
        else:
            print("Permission needed")
    else:
        print("Log in first")

print("Test 1:"); open_page(True, True)     # Page opened
print("Test 2:"); open_page(True, False)    # Permission needed
print("Test 3:"); open_page(False, True)    # Log in first (permission never checked)
{% endraw %}
{% endcapture %}

{% capture source1 %}
{% raw %}
```python
# CODE_RUNNER: Popcorn Hack 2 - Repair the student account check

def open_page(logged_in, has_permission):
    if logged_in:
        print("Account found")
        if has_permission:
            print("Page opened")
        else:
            print("Permission needed")
    else:
        print("Log in first")

print("Test 1:"); open_page(True, True)     # Page opened
print("Test 2:"); open_page(True, False)    # Permission needed
print("Test 3:"); open_page(False, True)    # Log in first (permission never checked)
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-nested-conditionals-hw-1"
   language="python"
   challenge=challenge1
   code=code1
   source=source1
%}


## Popcorn Hack 3: Lunch and Sports Practice



{% capture challenge2 %}
{% raw %}
Popcorn Hack 3 - Test the lunch and sports-practice plan
{% endraw %}
{% endcapture %}

{% capture code2 %}
{% raw %}
def lunch_plan(lunch_packed, practice_after_school):
    if lunch_packed:
        if practice_after_school:
            print("Packed lunch + practice: eat your lunch and pack an extra snack for practice.")
        else:
            print("Packed lunch, no practice: your packed lunch is enough today.")
    else:
        if practice_after_school:
            print("Buy lunch + practice: buy lunch and grab an extra snack at the cafeteria for practice.")
        else:
            print("Buy lunch, no practice: just buy lunch at the cafeteria.")

for packed in [True, False]:
    for practice in [True, False]:
        lunch_plan(packed, practice)
{% endraw %}
{% endcapture %}

{% capture source2 %}
{% raw %}
```python
# CODE_RUNNER: Popcorn Hack 3 - Test the lunch and sports-practice plan

def lunch_plan(lunch_packed, practice_after_school):
    if lunch_packed:
        if practice_after_school:
            print("Packed lunch + practice: eat your lunch and pack an extra snack for practice.")
        else:
            print("Packed lunch, no practice: your packed lunch is enough today.")
    else:
        if practice_after_school:
            print("Buy lunch + practice: buy lunch and grab an extra snack at the cafeteria for practice.")
        else:
            print("Buy lunch, no practice: just buy lunch at the cafeteria.")

for packed in [True, False]:
    for practice in [True, False]:
        lunch_plan(packed, practice)
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-nested-conditionals-hw-2"
   language="python"
   challenge=challenge2
   code=code2
   source=source2
%}


**Same structure in JavaScript:**


{% capture challenge3 %}
{% raw %}
Homework Hack - Build a high school daily routine dashboard
{% endraw %}
{% endcapture %}

{% capture code3 %}
{% raw %}
student = {
    "logged_in": True,
    "homework_finished": False,
    "lunch_packed": True,
    "practice_today": True
}

def daily_dashboard(student):
    # Outer decision: account access comes first
    if student["logged_in"]:
        print("Welcome back! Loading your schedule...")

        # Nested decision 1: meals
        if student["lunch_packed"]:
            if student["practice_today"]:
                print("Lunch: eat your packed lunch and save a snack for practice.")
            else:
                print("Lunch: eat your packed lunch.")
        else:
            print("Lunch: stop by the cafeteria to buy lunch.")

        # Nested decision 2: practice and homework
        if student["practice_today"]:
            if student["homework_finished"]:
                print("After school: head to practice, then relax after dinner.")
            else:
                print("After school: go to practice, then finish homework right after dinner.")
        else:
            if student["homework_finished"]:
                print("After school: homework is done - enjoy your free time!")
            else:
                print("After school: no practice today, so finish homework before dinner.")
    else:
        print("Please log in to see your daily routine.")
    print("-" * 60)

daily_dashboard(student)   # starter data

# Test every meaningful outcome
tests = [
    {"logged_in": False, "homework_finished": True,  "lunch_packed": True,  "practice_today": True},
    {"logged_in": True,  "homework_finished": True,  "lunch_packed": True,  "practice_today": True},
    {"logged_in": True,  "homework_finished": False, "lunch_packed": False, "practice_today": True},
    {"logged_in": True,  "homework_finished": True,  "lunch_packed": False, "practice_today": False},
    {"logged_in": True,  "homework_finished": False, "lunch_packed": True,  "practice_today": False},
]
for t in tests:
    print(t)
    daily_dashboard(t)
{% endraw %}
{% endcapture %}

{% capture source3 %}
{% raw %}
```javascript
let lunchPacked = true;
let practiceAfterSchool = true;

if (lunchPacked) {
    if (practiceAfterSchool) {
        console.log("Packed lunch + practice: eat your lunch and pack an extra snack for practice.");
    } else {
        console.log("Packed lunch, no practice: your packed lunch is enough today.");
    }
} else {
    if (practiceAfterSchool) {
        console.log("Buy lunch + practice: buy lunch and grab an extra snack at the cafeteria for practice.");
    } else {
        console.log("Buy lunch, no practice: just buy lunch at the cafeteria.");
    }
}
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-nested-conditionals-hw-3"
   language="python"
   challenge=challenge3
   code=code3
   source=source3
%}


**Same structure in College Board pseudocode:**

```text
IF (lunchPacked)
{
    IF (practiceAfterSchool)
    {
        DISPLAY("Packed lunch + practice: eat your lunch and pack an extra snack")
    }
    ELSE
    {
        DISPLAY("Packed lunch, no practice: your packed lunch is enough")
    }
}
ELSE
{
    IF (practiceAfterSchool)
    {
        DISPLAY("Buy lunch + practice: buy lunch and grab an extra snack")
    }
    ELSE
    {
        DISPLAY("Buy lunch, no practice: just buy lunch")
    }
}
```

**Execution order:** `lunch_packed` (the outer condition) is checked first. Only after it picks a branch is `practice_after_school` checked, inside that branch. That gives 2 × 2 = 4 possible recommendations.

## Homework Hack: High School Daily Routine Dashboard


```python
# CODE_RUNNER: Homework Hack - Build a high school daily routine dashboard

student = {
    "logged_in": True,
    "homework_finished": False,
    "lunch_packed": True,
    "practice_today": True
}

def daily_dashboard(student):
    # Outer decision: account access comes first
    if student["logged_in"]:
        print("Welcome back! Loading your schedule...")

        # Nested decision 1: meals
        if student["lunch_packed"]:
            if student["practice_today"]:
                print("Lunch: eat your packed lunch and save a snack for practice.")
            else:
                print("Lunch: eat your packed lunch.")
        else:
            print("Lunch: stop by the cafeteria to buy lunch.")

        # Nested decision 2: practice and homework
        if student["practice_today"]:
            if student["homework_finished"]:
                print("After school: head to practice, then relax after dinner.")
            else:
                print("After school: go to practice, then finish homework right after dinner.")
        else:
            if student["homework_finished"]:
                print("After school: homework is done - enjoy your free time!")
            else:
                print("After school: no practice today, so finish homework before dinner.")
    else:
        print("Please log in to see your daily routine.")
    print("-" * 60)

daily_dashboard(student)   # starter data

# Test every meaningful outcome
tests = [
    {"logged_in": False, "homework_finished": True,  "lunch_packed": True,  "practice_today": True},
    {"logged_in": True,  "homework_finished": True,  "lunch_packed": True,  "practice_today": True},
    {"logged_in": True,  "homework_finished": False, "lunch_packed": False, "practice_today": True},
    {"logged_in": True,  "homework_finished": True,  "lunch_packed": False, "practice_today": False},
    {"logged_in": True,  "homework_finished": False, "lunch_packed": True,  "practice_today": False},
]
for t in tests:
    print(t)
    daily_dashboard(t)
```

**Outcomes covered:** "Please log in", all three lunch messages, and all four after-school messages (practice and done, practice and not done, no practice and done, no practice and not done). That is more than four clear recommendations, and every one appears in the test output.

**Why the inner checks depend on the outer decisions:** The schedule, meal, and homework checks sit inside the `logged_in` branch because a student's personal information should only be shown after they log in. If the account check fails, none of the inner questions are asked. In the same way, whether to save a snack depends on first knowing that lunch was packed, and the homework plan changes depending on whether practice is taking up the afternoon, so those checks are nested under the decisions they depend on.

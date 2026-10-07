---
layout: post
codemirror: True
title: UESL 3.1 Homework
categories: ['Python']
lesson_language: Python
lesson_topic: Variables-and-Assignments HW
lesson_part: interactive
lesson_type: lesson
permalink: /homework/3-1/
author: Shourya Patel
---

# UESL 3.1 Variables and Assignments — Homework

Completed every part of the 3.1 lesson: the Popcorn checkpoint, the MCQ, the Homework Hack (star counter), both required tests and the design-thinking note. Each piece of code is shown in Python and College Board pseudocode, with my prediction and the actual output.

## Popcorn

### Popcorn Hack · Checkpoint challenge

**Prediction (before running):** `stars` starts at 8, the checkpoint copies 8, then only `stars` gains 4. I predict `12`, then `8`.



{% capture challenge0 %}
{% raw %}
UESL 3.1 Popcorn - Keep the checkpoint
{% endraw %}
{% endcapture %}

{% capture code0 %}
{% raw %}
stars = 8
checkpoint_stars = stars
stars = stars + 4
print(stars)
print(checkpoint_stars)
{% endraw %}
{% endcapture %}

{% capture source0 %}
{% raw %}
```python
# CODE_RUNNER: UESL 3.1 Popcorn - Keep the checkpoint
stars = 8
checkpoint_stars = stars
stars = stars + 4
print(stars)
print(checkpoint_stars)
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="homework-3-1-0"
   language="python"
   challenge=challenge0
   code=code0
   source=source0
%}


**Actual output:** `12`, then `8` — matches my prediction.

**Why they differ:** `checkpoint_stars = stars` copies the *value* 8 at the moment it runs. Later assignments to `stars` replace the value stored in `stars` only; they never go back and change `checkpoint_stars`. A checkpoint is a snapshot, not a live link.

Same program in College Board pseudocode:


{% capture challenge1 %}
{% raw %}
UESL 3.1 - Playtest the star counter (bonus 5, then bonus 0)
{% endraw %}
{% endcapture %}

{% capture code1 %}
{% raw %}
for bonus in [5, 0]:
    game_title = "UESL Star Trail"
    level_one_stars = 10
    level_two_stars = 20
    level_three_stars = 15
    total_stars = level_one_stars + level_two_stars + level_three_stars
    print(game_title, "| bonus =", bonus)
    print(total_stars)
    level_two_stars = level_two_stars + bonus
    print(total_stars)
    total_stars = level_one_stars + level_two_stars + level_three_stars
    print(total_stars)
{% endraw %}
{% endcapture %}

{% capture source1 %}
{% raw %}
```text
stars ← 8
checkpoint_stars ← stars
stars ← stars + 4
DISPLAY(stars)              // 12
DISPLAY(checkpoint_stars)   // 8
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="homework-3-1-1"
   language="python"
   challenge=challenge1
   code=code1
   source=source1
%}


### Example C playtest (bonus 5, then bonus 0)

**Prediction:** original total 45, stored total still 45 after the bonus (it was not recalculated), then 50 after recalculating. With a bonus of 0 all three print 45.



{% capture challenge2 %}
{% raw %}
UESL 3.1 Homework - Comet Quest star counter
{% endraw %}
{% endcapture %}

{% capture code2 %}
{% raw %}
game_title = "Comet Quest"          # str: the game's name is text
reduced_motion = True               # bool: a player's on/off accessibility setting
bonus = 5                           # int: stars awarded on level two

level_one_stars = 12                # int: whole stars collected per level
level_two_stars = 18
level_three_stars = 10

total_stars = level_one_stars + level_two_stars + level_three_stars
print("Game:", game_title)
print("Reduced motion:", reduced_motion)
print("Original total:", total_stars)

level_two_stars = level_two_stars + bonus       # evaluate right side first, then store
print("Stored total after bonus (not recalculated):", total_stars)

total_stars = level_one_stars + level_two_stars + level_three_stars   # recalculate
print("Updated total:", total_stars)
{% endraw %}
{% endcapture %}

{% capture source2 %}
{% raw %}
```python
# CODE_RUNNER: UESL 3.1 - Playtest the star counter (bonus 5, then bonus 0)
for bonus in [5, 0]:
    game_title = "UESL Star Trail"
    level_one_stars = 10
    level_two_stars = 20
    level_three_stars = 15
    total_stars = level_one_stars + level_two_stars + level_three_stars
    print(game_title, "| bonus =", bonus)
    print(total_stars)
    level_two_stars = level_two_stars + bonus
    print(total_stars)
    total_stars = level_one_stars + level_two_stars + level_three_stars
    print(total_stars)
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="homework-3-1-2"
   language="python"
   challenge=challenge2
   code=code2
   source=source2
%}


**Actual output:** `45, 45, 50` with a bonus of 5 and `45, 45, 45` with a bonus of 0. The middle line never changes, because displaying a total does not recalculate it.

## MCQ

| # | Question | My answer | Why |
|---|---|---|---|
| 1 | Best type for player tag `"007"` | **B** string | Text keeps the leading zeros; an integer would become 7. |
| 2 | `stars ← 8`, `checkpoint ← stars`, `stars ← 12` → `checkpoint`? | **A** 8 | The checkpoint copied 8 before `stars` changed. |
| 3 | Which AP operator assigns? | **C** `←` | In pseudocode `=` tests equality. |
| 4 | When does a stored total change? | **B** When reassigned/recalculated | A total is a stored result, not a live formula. |

**MCQ 3.1: 4/4 | answers: B,A,C,B**

## Homework

### Homework Hack · Build my UESL star counter

My game is **Comet Quest**. Players can turn on reduced motion so stars don't streak across the screen.

**Predictions:** original total `12 + 18 + 10 = 40`; after a bonus of 5 on level two, the *stored* total is still `40`; after recalculating it is `45`.



{% capture challenge3 %}
{% raw %}
UESL 3.1 Tests - bonus 5 and bonus 0, each starting fresh
{% endraw %}
{% endcapture %}

{% capture code3 %}
{% raw %}
def playtest(bonus):
    level_one_stars = 12
    level_two_stars = 18
    level_three_stars = 10
    total_stars = level_one_stars + level_two_stars + level_three_stars
    original = total_stars
    level_two_stars = level_two_stars + bonus
    stored = total_stars
    total_stars = level_one_stars + level_two_stars + level_three_stars
    print(f"bonus={bonus}: original={original}, stored={stored}, updated={total_stars}")

playtest(5)   # predicted: 40, 40, 45
playtest(0)   # predicted: 40, 40, 40
{% endraw %}
{% endcapture %}

{% capture source3 %}
{% raw %}
```python
# CODE_RUNNER: UESL 3.1 Homework - Comet Quest star counter
game_title = "Comet Quest"          # str: the game's name is text
reduced_motion = True               # bool: a player's on/off accessibility setting
bonus = 5                           # int: stars awarded on level two

level_one_stars = 12                # int: whole stars collected per level
level_two_stars = 18
level_three_stars = 10

total_stars = level_one_stars + level_two_stars + level_three_stars
print("Game:", game_title)
print("Reduced motion:", reduced_motion)
print("Original total:", total_stars)

level_two_stars = level_two_stars + bonus       # evaluate right side first, then store
print("Stored total after bonus (not recalculated):", total_stars)

total_stars = level_one_stars + level_two_stars + level_three_stars   # recalculate
print("Updated total:", total_stars)
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="homework-3-1-3"
   language="python"
   challenge=challenge3
   code=code3
   source=source3
%}


The same homework in College Board pseudocode:

```text
game_title ← "Comet Quest"
reduced_motion ← true
level_one_stars ← 12
level_two_stars ← 18
level_three_stars ← 10
total_stars ← level_one_stars + level_two_stars + level_three_stars
DISPLAY(game_title)
DISPLAY(reduced_motion)
DISPLAY(total_stars)                 // 40
level_two_stars ← level_two_stars + 5
DISPLAY(total_stars)                 // still 40
total_stars ← level_one_stars + level_two_stars + level_three_stars
DISPLAY(total_stars)                 // 45
```

## Tests

Each test starts from fresh starting values (12, 18, 10) so no earlier run leaks into it.


```python
# CODE_RUNNER: UESL 3.1 Tests - bonus 5 and bonus 0, each starting fresh
def playtest(bonus):
    level_one_stars = 12
    level_two_stars = 18
    level_three_stars = 10
    total_stars = level_one_stars + level_two_stars + level_three_stars
    original = total_stars
    level_two_stars = level_two_stars + bonus
    stored = total_stars
    total_stars = level_one_stars + level_two_stars + level_three_stars
    print(f"bonus={bonus}: original={original}, stored={stored}, updated={total_stars}")

playtest(5)   # predicted: 40, 40, 45
playtest(0)   # predicted: 40, 40, 40
```

| Test | Prediction | Actual | Explanation |
|---|---|---|---|
| Bonus 5 | 40, 40, 45 | 40, 40, 45 | The stored total only changes when it is reassigned. |
| Bonus 0 | 40, 40, 40 | 40, 40, 40 | Adding 0 changes nothing, so recalculating gives the same total. |

**Assignment vs. comparison:** in Python `total_stars = ...` *stores* a value, while `total_stars == 40` *asks* whether it equals 40. In AP pseudocode `←` stores and `=` asks.

**Next mission question — what would 100 separate variables cost?** Every new level would need a new variable, and the total line would have to be edited to add all 100 names by hand. Forgetting one name silently gives a wrong total. A list (3.2) lets one loop add every level no matter how many there are.

## Design Thinking

- **Player need:** Some UESL players find fast, flashing motion uncomfortable, and every player wants to see exactly how many stars they earned.
- **Goal:** Show a clear star total that updates correctly after a bonus, and let players choose reduced motion.
- **Representation considered:** I considered storing reduced motion as a string like `"on"`/`"off"`, but a Boolean (`True`/`False`) can't be misspelled and matches a yes/no choice. Stars are `int` because you can't collect half a star.
- **Prototype:** The Comet Quest counter above, with separate level variables and an explicit recalculation step.
- **Test / revision:** My first version printed the total only once, after the bonus, so the stale total was hidden. I revised it to print the stored total and the recalculated total separately so a player (and I) can see what changed.
- **Why reduced motion should be a player choice:** Players have different needs — motion that is fun for one player can be distracting or uncomfortable for another, so the game should respect the setting the player picks instead of forcing one experience.

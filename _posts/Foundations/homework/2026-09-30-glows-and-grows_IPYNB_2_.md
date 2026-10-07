---
layout: post
title: Glows and Grows - Big Idea 3 Lessons
categories: ['Python']
permalink: /python/glows-and-grows
author: Shourya Patel
---

# Glows and Grows

Two glows and one grow for each lesson. Each lesson is in its own block so it can be copied and pasted on its own.

## 3.01 Variables and Assignments

Homework notebook: `2026-07-21-variables_python_instructor-hw.ipynb`

```text
Lesson: 3.01 Variables and Assignments
Glow 1: The UESL Star Trail theme made variables feel useful, and the checkpoint vs. live stars example clearly showed that assignment copies a value instead of linking two variables.
Glow 2: Having every example in both Python and College Board pseudocode, with a comment on each pseudocode line, made it easy to see that `=` in Python means `←` on the AP exam.
Grow: The homework asks for a separate Markdown page in navigation/homework while other lessons use an _notebooks/homework notebook. Using one submission format for every lesson would cut down on confusion.
```

## 3.02 Data Abstraction

Homework notebook: `2025-09-26-data_abstractions_remakers-hw.ipynb`

```text
Lesson: 3.02 Data Abstraction
Glow 1: The index map table (level label, Python index, AP index) made the 0-based vs. 1-based difference easy to remember.
Glow 2: The shared-list vs. .copy() partner check was a great addition, because it's a bug most people would never notice until it broke their code.
Grow: The empty-list test tells us to skip the second-level update but doesn't show how. A short guard example like `if len(level_stars) >= 2:` would help students who get an IndexError.
```

## 3.04 Strings

Homework notebook: `2026-09-15-strings_intercepters-hw.ipynb`

```text
Lesson: 3.04 Strings
Glow 1: The signal-interceptor theme made indexing and slicing feel like decoding a real message, and the hidden-message popcorn hack was fun to solve.
Glow 2: The homework uses real formats (CSV, Markdown table rows, JSON), so the string skills carry over to things I'll actually use outside the class.
Grow: Popcorn Hack 2 says to 'remove' `>` and `-`, but removing them glues AGENT, Falcon, and reports into one word. A hint to replace them with spaces would keep the word count from being confusing.
```

## 3.05 Boolean Expressions

Homework notebook: `2026-09-15-boolean_scratchers_py_hw-hw.ipynb`

```text
Lesson: 3.05 Boolean Expressions
Glow 1: Using one SFI backend theme the whole time built up nicely, from checking a single field to validating a full record.
Glow 2: The College Board pseudocode validator next to the Python operator table made it clear how `=`, `≠`, AND, OR and NOT map to Python.
Grow: The popcorn starter cells only say 'Build and test your solution below.' One or two TODO hints would help students finish them in the 2-minute in-class window.
```

## 3.06 Conditionals

Homework notebook: `2026-09-25-conditionals-python-hw.ipynb`

```text
Lesson: 3.06 Conditionals
Glow 1: Counting the outcomes and then counting the answers is a simple method I can actually use to catch a missing else.
Glow 2: Popcorn Hack 2 (the elif chain in the wrong order) was the most eye-opening part. It runs, prints confidently, and is still wrong, which I had never thought about before.
Grow: The lesson is very long, with a lot of reference tables before any code runs. Moving the big three-language table further down, or collapsing it, would get students coding sooner.
```

## 3.07 Nested Conditionals

Homework notebook: `2026-09-17-nested-conditionals-python-hw.ipynb`

```text
Lesson: 3.07 Nested Conditionals
Glow 1: The student-life theme (accounts, homework, lunch, practice) is relatable, so it was easy to reason about which check should come first.
Glow 2: The three popcorn hacks build up well: trace complete code, then fix broken indentation, then finish a partial solution.
Grow: There's no MCQ or quick check. Adding a few questions about which branch runs for given values would help students check their understanding before the homework.
```

## 3.08 Iterations

Homework notebook: `2025-09-26-iterations_scratchers_lesson-hw.ipynb`

```text
Lesson: 3.08 Iterations
Glow 1: The fill-in-the-blank SFSRC dispatch scanner made me actually think about where continue and break go, instead of just copying finished code.
Glow 2: The interactive MCQ that gives an answer line to paste into the submission notes made submitting easy.
Grow: A notebook cell marker (`#%% vscode.cell ...`) got pasted into the homework code cell, so the grading plan shows up inside the code block. That cell should be split back into code and Markdown.
```

## 3.09 Developing Algorithms (Peppa Pig Maze)

Homework notebook: `2025-10-09-developing-algorithms_crashers-hw.ipynb`

```text
Lesson: 3.09 Developing Algorithms (Peppa Pig Maze)
Glow 1: The Peppa Pig maze is a fun, visual way to show that an algorithm is a series of steps with checks before each move.
Glow 2: Showing two different algorithms that solve the same problem (manual vs. direct addition, if/else vs. max()) introduces the idea of equivalent algorithms.
Grow: The lesson has no popcorn hacks, MCQ, or homework, and the maze is controlled one button press at a time. A hack where students write Peppa's full list of moves as an algorithm, then test whether it reaches the end, would make students design an algorithm instead of just clicking.
```

## 3.09 Developing Algorithms (Safe Passage Heals)

Homework notebook: `2026-09-18-developing-algorithms-hw.ipynb`

```text
Lesson: 3.09 Developing Algorithms (Safe Passage Heals)
Glow 1: Example C (one line moved changes the count from 3 to 9) clearly shows that similar-looking algorithms can give different results.
Glow 2: The Participation Moments (human robot, table talk, fastest table) kept the lesson active and connected the pseudocode to real movement.
Grow: The homework expects an exact output, but it doesn't say what to do when two items tie for the most urgent shortage. One sentence on ties would make the expected output fully clear.
```

## 3.10 Lists

Homework notebook: `2025-09-30-lists_scratchers_lesson-hw.ipynb`

```text
Lesson: 3.10 Lists
Glow 1: The predict-then-run popcorn hack, with a deliberate IndexError, was a memorable way to learn the last valid index is len - 1.
Glow 2: The homework puts indexing, the accumulator, frequency counting, and filtering all on one dataset, and the expected output shape made it easy to check my work.
Grow: Popcorn Hack 3 depends on live class survey data, so students working at home don't have it. Providing a backup sample list would make it doable anywhere.
```

## 3.12 Calling Procedures

Homework notebook: `2025-10-08-calling_procedures_remakers_lesson-hw.ipynb`

```text
Lesson: 3.12 Calling Procedures
Glow 1: The vocabulary table separating parameter from argument, with an example of each, cleared up a common mix-up.
Glow 2: The Poway emergency-response theme made helper procedures make sense: one procedure decides priority and the other dispatches.
Grow: The pseudocode reference is in a code cell marked CODE_RUNNER, so it shows up as runnable Python and errors if run. It would be better as a Markdown block, and the 5-question knowledge check could include an answer key.
```

## 3.13 Developing Procedures

Homework notebook: `2025-10-09-developing_procedures_remakers_lesson-hw.ipynb`

```text
Lesson: 3.13 Developing Procedures
Glow 1: The Dessert Robot story showed why procedure names matter: makeDessert() with clear sub-steps is much easier to read than doIt().
Glow 2: Comparing the do_step() examples side by side showed how vague names make debugging harder.
Grow: The 'Java example' is actually JavaScript, and the mini-game uses input(), which doesn't work in the code runner. The lesson also has no graded hacks, so clear popcorn/homework tasks would help.
```

## 3.14 Libraries

Homework notebook: `2026-09-16-libraries_python-hw.ipynb`

```text
Lesson: 3.14 Libraries
Glow 1: Connecting libraries to the real Open Coding Society stack (Flask, SQLAlchemy, nbconvert) showed that these are tools we actually use.
Glow 2: Writing a Flask route and testing it with app.test_client() without running a server was a great hands-on activity.
Grow: The homework is a fully worked example, so it's easy to just change the numbers. Leaving parts of summarize_season as TODOs would make students build more of it themselves.
```

## 3.15 Random Values

Homework notebook: `2026-09-15-random_py_sprinters-hw.ipynb`

```text
Lesson: 3.15 Random Values
Glow 1: The QA-testing theme gave randomness a real purpose (testing many backend paths) instead of just dice rolls.
Glow 2: The College Board RANDOM(a, b) to random.randint(a, b) table, plus the 3 × 4 = 12 possible-pairs example, made inclusive ranges and possible outputs clear.
Grow: The popcorn starters have no TODO hints, and the homework doesn't say what each API action should do to the stored specs. A short rule for each action would make expected behavior clearer.
```

## 3.17 Algorithmic Efficiency

Homework notebook: `2026-09-21-algorithmic-efficiency-hw.ipynb`

```text
Lesson: 3.17 Algorithmic Efficiency
Glow 1: The book-search example (linear 5 checks vs. binary 3 checks) and the warm-up where linear wins for book 3 showed that one case doesn't describe overall growth.
Glow 2: The growth table (constant, log, linear, quadratic, exponential), with a library example for each, made abstract growth rates concrete.
Grow: The calculators only model counts with formulas. Having students run a real linear and binary search that counts its checks would make the comparison more convincing.
```

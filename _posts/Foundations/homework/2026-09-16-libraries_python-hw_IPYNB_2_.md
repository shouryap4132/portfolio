---
layout: post
codemirror: True
title: 3.14 Libraries HW
categories: ['Python']
lesson_language: Python
lesson_topic: Libraries HW
lesson_part: interactive
lesson_type: lesson
permalink: /python/libraries-hw
author: Shourya Patel
---

# 3.14 Libraries — Homework

Popcorn Hack 1 (changed), Popcorn Hack 2 (my own route), the import-styles fix, and my own Season Stats Report homework. My sport is **soccer** (goals instead of points).

## Popcorn Hack 1: Read the API, Then Use It

**My changes:** jersey range 1–55, and the square root of a **196** sq ft court.

**Prediction:** jersey is some whole number from 1 to 55 (both included); court side is `14.0` feet; average points = 122 / 5 = `24.4`, rounded up to `25`.



{% capture challenge0 %}
{% raw %}
Popcorn 1 - jersey range changed to 1-55 and a 196 sq ft court
{% endraw %}
{% endcapture %}

{% capture code0 %}
{% raw %}
import math
import random

print("random.randint:", random.randint.__doc__)
print("math.ceil:", math.ceil.__doc__)
print()

points_per_game = [24, 18, 31, 27, 22]

print("Random game to review:", random.choice(points_per_game), "points")

jersey = random.randint(1, 55)          # changed from 1-99
print("Random jersey number:", jersey)

side = math.sqrt(196)                   # changed from 144
print("Square court side:", side, "feet")

average = sum(points_per_game) / len(points_per_game)
rounded_up = math.ceil(average)
print("Points per game:", average, "-> rounded up:", rounded_up)
{% endraw %}
{% endcapture %}

{% capture source0 %}
{% raw %}
```python
# CODE_RUNNER: Popcorn 1 - jersey range changed to 1-55 and a 196 sq ft court

import math
import random

print("random.randint:", random.randint.__doc__)
print("math.ceil:", math.ceil.__doc__)
print()

points_per_game = [24, 18, 31, 27, 22]

print("Random game to review:", random.choice(points_per_game), "points")

jersey = random.randint(1, 55)          # changed from 1-99
print("Random jersey number:", jersey)

side = math.sqrt(196)                   # changed from 144
print("Square court side:", side, "feet")

average = sum(points_per_game) / len(points_per_game)
rounded_up = math.ceil(average)
print("Points per game:", average, "-> rounded up:", rounded_up)
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-libraries-hw-0"
   language="python"
   challenge=challenge0
   code=code0
   source=source0
%}


**Result:** matches the prediction. The jersey changes every run but always stays between 1 and 55 because the API says `randint` includes both endpoints.

## Popcorn Hack 2: Write a Flask Route

I changed the roster to my own players and added two routes of my own: `/coach` and `/record`.



{% capture challenge1 %}
{% raw %}
Popcorn 2 - my roster plus my own /coach and /record routes
{% endraw %}
{% endcapture %}

{% capture code1 %}
{% raw %}
from flask import Flask, jsonify

app = Flask(__name__)

@app.route("/score")
def score():
    return jsonify({"home": 3, "away": 1, "half": 2})

@app.route("/roster")
def roster():
    return jsonify({"players": ["Shourya", "Arjun", "Maya", "Leo"]})

@app.route("/coach")
def coach():
    return jsonify({"coach": "Coach Rivera", "formation": "4-3-3"})

@app.route("/record")
def record():
    return jsonify({"wins": 5, "losses": 1, "ties": 2})

client = app.test_client()

print("/score says:", client.get("/score").get_json())
print("/roster says:", client.get("/roster").get_json())
print("/coach says:", client.get("/coach").get_json())
print("/record says:", client.get("/record").get_json())
{% endraw %}
{% endcapture %}

{% capture source1 %}
{% raw %}
```python
# CODE_RUNNER: Popcorn 2 - my roster plus my own /coach and /record routes

from flask import Flask, jsonify

app = Flask(__name__)

@app.route("/score")
def score():
    return jsonify({"home": 3, "away": 1, "half": 2})

@app.route("/roster")
def roster():
    return jsonify({"players": ["Shourya", "Arjun", "Maya", "Leo"]})

@app.route("/coach")
def coach():
    return jsonify({"coach": "Coach Rivera", "formation": "4-3-3"})

@app.route("/record")
def record():
    return jsonify({"wins": 5, "losses": 1, "ties": 2})

client = app.test_client()

print("/score says:", client.get("/score").get_json())
print("/roster says:", client.get("/roster").get_json())
print("/coach says:", client.get("/coach").get_json())
print("/record says:", client.get("/record").get_json())
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-libraries-hw-1"
   language="python"
   challenge=challenge1
   code=code1
   source=source1
%}


## Three Ways to Import: fix the line that breaks

When the nickname is changed to `import statistics as s`, the line `stats.mean(...)` breaks with `NameError: name 'stats' is not defined`, because the library is now only known as `s`. The fix is to call `s.mean(...)`.



{% capture challenge2 %}
{% raw %}
Import styles - nickname changed to s, broken line fixed
{% endraw %}
{% endcapture %}

{% capture code2 %}
{% raw %}
import math
from random import randint
import statistics as s

print("Hoop circumference:", round(2 * math.pi * 0.75, 2), "feet")
print("Coin toss, 1 means home ball:", randint(1, 2))
print("Points per game:", s.mean([24, 18, 31]))    # was stats.mean -> NameError
{% endraw %}
{% endcapture %}

{% capture source2 %}
{% raw %}
```python
# CODE_RUNNER: Import styles - nickname changed to s, broken line fixed

import math
from random import randint
import statistics as s

print("Hoop circumference:", round(2 * math.pi * 0.75, 2), "feet")
print("Coin toss, 1 means home ball:", randint(1, 2))
print("Points per game:", s.mean([24, 18, 31]))    # was stats.mean -> NameError
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-libraries-hw-2"
   language="python"
   challenge=challenge2
   code=code2
   source=source2
%}


## Homework Hack: Season Stats Report (soccer)

Uses **four** standard-library modules: `json`, `statistics`, `datetime`, and `math`.



{% capture challenge3 %}
{% raw %}
Homework - my soccer season stats report
{% endraw %}
{% endcapture %}

{% capture code3 %}
{% raw %}
import json
import math
import statistics
from datetime import date

games = [
    {"date": "2026-08-29", "opponent": "Westview", "goals": 2, "minutes": 80},
    {"date": "2026-09-05", "opponent": "Mt. Carmel", "goals": 0, "minutes": 65},
    {"date": "2026-09-12", "opponent": "Rancho Bernardo", "goals": 3, "minutes": 80},
    {"date": "2026-09-19", "opponent": "Westview", "goals": 1, "minutes": 72},
    {"date": "2026-09-26", "opponent": "Poway", "goals": 2, "minutes": 78},
]

def summarize_season(season):
    """
    Summarize a list of soccer games for one player.

    Parameters:
        season: list of dictionaries, each with "date" (YYYY-MM-DD string),
                "opponent" (string), "goals" (int), and "minutes" (int)
    Returns:
        dictionary with:
            total_goals (int), average_goals (float, 1 decimal),
            best_game (int, most goals in one game),
            goals_by_opponent (dict of opponent -> total goals),
            minutes_per_goal (int, rounded up with math.ceil)
    """
    goals = []
    total_minutes = 0
    goals_by_opponent = {}
    for game in season:
        goals.append(game["goals"])
        total_minutes += game["minutes"]
        opponent = game["opponent"]
        goals_by_opponent[opponent] = goals_by_opponent.get(opponent, 0) + game["goals"]

    total_goals = sum(goals)
    return {
        "total_goals": total_goals,
        "average_goals": round(statistics.mean(goals), 1),
        "best_game": max(goals),
        "goals_by_opponent": goals_by_opponent,
        "minutes_per_goal": math.ceil(total_minutes / total_goals),
    }

report = summarize_season(games)

# datetime: subtracting two dates gives a timedelta; .days is the whole number of days
next_game = date(2026, 10, 24)
report["next_game"] = next_game.isoformat()
report["days_until_next_game"] = (next_game - date.today()).days

print(json.dumps(report, indent=2))

# requirements.txt for a real version of this app (pandas table + Flask scoreboard page)
requirements_txt = """# External packages only - installed with: pip install -r requirements.txt
# json, datetime, statistics, and math are NOT listed because they are part of
# Python's standard library and come with every Python install.
pandas
Flask
"""
print()
print("requirements.txt:")
print(requirements_txt)
{% endraw %}
{% endcapture %}

{% capture source3 %}
{% raw %}
```python
# CODE_RUNNER: Homework - my soccer season stats report

import json
import math
import statistics
from datetime import date

games = [
    {"date": "2026-08-29", "opponent": "Westview", "goals": 2, "minutes": 80},
    {"date": "2026-09-05", "opponent": "Mt. Carmel", "goals": 0, "minutes": 65},
    {"date": "2026-09-12", "opponent": "Rancho Bernardo", "goals": 3, "minutes": 80},
    {"date": "2026-09-19", "opponent": "Westview", "goals": 1, "minutes": 72},
    {"date": "2026-09-26", "opponent": "Poway", "goals": 2, "minutes": 78},
]

def summarize_season(season):
    """
    Summarize a list of soccer games for one player.

    Parameters:
        season: list of dictionaries, each with "date" (YYYY-MM-DD string),
                "opponent" (string), "goals" (int), and "minutes" (int)
    Returns:
        dictionary with:
            total_goals (int), average_goals (float, 1 decimal),
            best_game (int, most goals in one game),
            goals_by_opponent (dict of opponent -> total goals),
            minutes_per_goal (int, rounded up with math.ceil)
    """
    goals = []
    total_minutes = 0
    goals_by_opponent = {}
    for game in season:
        goals.append(game["goals"])
        total_minutes += game["minutes"]
        opponent = game["opponent"]
        goals_by_opponent[opponent] = goals_by_opponent.get(opponent, 0) + game["goals"]

    total_goals = sum(goals)
    return {
        "total_goals": total_goals,
        "average_goals": round(statistics.mean(goals), 1),
        "best_game": max(goals),
        "goals_by_opponent": goals_by_opponent,
        "minutes_per_goal": math.ceil(total_minutes / total_goals),
    }

report = summarize_season(games)

# datetime: subtracting two dates gives a timedelta; .days is the whole number of days
next_game = date(2026, 10, 24)
report["next_game"] = next_game.isoformat()
report["days_until_next_game"] = (next_game - date.today()).days

print(json.dumps(report, indent=2))

# requirements.txt for a real version of this app (pandas table + Flask scoreboard page)
requirements_txt = """# External packages only - installed with: pip install -r requirements.txt
# json, datetime, statistics, and math are NOT listed because they are part of
# Python's standard library and come with every Python install.
pandas
Flask
"""
print()
print("requirements.txt:")
print(requirements_txt)
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-libraries-hw-3"
   language="python"
   challenge=challenge3
   code=code3
   source=source3
%}


**How each library is used:**

| Library | Procedure | What I used it for |
|---|---|---|
| `statistics` | `mean(data)` | average goals per game |
| `math` | `ceil(x)` | minutes per goal, rounded up |
| `datetime` | `date(y, m, d)` and date subtraction | days until my next game |
| `json` | `dumps(obj, indent=2)` | print the report as JSON a scoreboard page could read |

### Submission notes

```text
Lesson: CSP 3.14 Libraries
Popcorn 1: what I changed = jersey range 1-55 and sqrt(196) court
Popcorn 2: my extra route = /coach (and /record)
Homework: libraries used = json, statistics, datetime (+ math)
Homework: days until my next game = see "days_until_next_game" in the output (next game 2026-10-24)
```

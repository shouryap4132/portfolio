---
layout: post
codemirror: True
title: Iterations HW
categories: ['Python']
lesson_language: Python
lesson_topic: Iterations HW
lesson_part: interactive
lesson_type: lesson
permalink: /python/iterations-hw
author: Shourya Patel
---

# 3.08 Iterations — Homework

Completed Quick Check, Popcorn Hack (all blanks filled), MCQ, and the themed Homework Hack.

## Quick Check (Reference Guide)

| # | Question | Answer |
|---|---|---|
| 1 | Best loop to inspect every value in a list in order | **A** for loop |
| 2 | Ignore a safe value without stopping the loop | **B** continue |
| 3 | What makes a while loop stop eventually? | **B** A condition that changes over time |

Quick check score: 3 / 3

## Popcorn Hack — SFSRC wildfire dispatch scanner

I chose `safe_cutoff = 3` (alerts 1 and 2 are safe) and `critical_cutoff = 9` (the top alert level stops the scan).

**Prediction:** 1 skip, 4 action, 2 skip, 6 action, 3 action, 9 action + critical → stop (5 is never checked). Safe skipped 2, action 4, total 4 + 6 + 3 + 9 = 22, critical found True.



{% capture challenge0 %}
{% raw %}
Popcorn Hack - wildfire dispatch scanner
{% endraw %}
{% endcapture %}

{% capture code0 %}
{% raw %}
# Theme: The SFSRC team scans wildfire alert levels from different zones.
# Goal: skip safe zones, count response zones, total their alert scores, and stop at the first critical zone.

alerts = [1, 4, 2, 6, 3, 9, 5]

# Alerts below this number are safe and skipped.
safe_cutoff = 3

# The loop stops at this number or higher.
critical_cutoff = 9

action_count = 0
safe_count = 0
total_action_score = 0
critical_found = False

for alert in alerts:
    if alert < safe_cutoff:
        safe_count += 1
        print("Alert " + str(alert) + ": safe, skipping")
        continue

    action_count += 1
    total_action_score += alert
    print("Alert " + str(alert) + ": action needed")

    if alert >= critical_cutoff:
        critical_found = True
        print("Critical alert found - stopping scan")
        break

print("Safe alerts skipped: " + str(safe_count))
print("Action alerts: " + str(action_count))
print("Total action score: " + str(total_action_score))
print("Critical found: " + str(critical_found))
{% endraw %}
{% endcapture %}

{% capture source0 %}
{% raw %}
```python
# CODE_RUNNER: Popcorn Hack - wildfire dispatch scanner
# Theme: The SFSRC team scans wildfire alert levels from different zones.
# Goal: skip safe zones, count response zones, total their alert scores, and stop at the first critical zone.

alerts = [1, 4, 2, 6, 3, 9, 5]

# Alerts below this number are safe and skipped.
safe_cutoff = 3

# The loop stops at this number or higher.
critical_cutoff = 9

action_count = 0
safe_count = 0
total_action_score = 0
critical_found = False

for alert in alerts:
    if alert < safe_cutoff:
        safe_count += 1
        print("Alert " + str(alert) + ": safe, skipping")
        continue

    action_count += 1
    total_action_score += alert
    print("Alert " + str(alert) + ": action needed")

    if alert >= critical_cutoff:
        critical_found = True
        print("Critical alert found - stopping scan")
        break

print("Safe alerts skipped: " + str(safe_count))
print("Action alerts: " + str(action_count))
print("Total action score: " + str(total_action_score))
print("Critical found: " + str(critical_found))
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-iterations-hw-0"
   language="python"
   challenge=challenge0
   code=code0
   source=source0
%}


**Actual output matches:** 2 skipped, 4 actions, total 22, critical True. The last alert (5) never prints because `break` ended the loop at 9. `continue` only skipped the rest of *one* pass; `break` stopped the *whole* scan.

## MCQ Check

| # | Question | Answer |
|---|---|---|
| 1 | Best loop when you already have a list | **A** for loop |
| 2 | What does `continue` do? | **B** Skips the rest of the current pass and moves to the next item |
| 3 | What prevents a while loop from running forever? | **A** A condition that eventually changes |
| 4 | Stop as soon as a critical alert is found | **B** break |

**MCQ 3.08 Iterations: 4/4 | answers: A,B,A,B**

## Example check — while loop cooldown

I also traced the `while` example: 85 → 70 → 55 → 40 → 25. The loop stops after 25 because `25 > 30` is False. The update `temperature -= 15` is what makes the condition eventually change.



{% capture challenge1 %}
{% raw %}
While loop trace - SFSRC cooldown
{% endraw %}
{% endcapture %}

{% capture code1 %}
{% raw %}
temperature = 85
safe_temperature = 30
passes = 0
while temperature > safe_temperature:
    temperature -= 15
    passes += 1
    print("Cooling SFSRC equipment: " + str(temperature))
print("Loop ran " + str(passes) + " times")
{% endraw %}
{% endcapture %}

{% capture source1 %}
{% raw %}
```python
# CODE_RUNNER: While loop trace - SFSRC cooldown
temperature = 85
safe_temperature = 30
passes = 0
while temperature > safe_temperature:
    temperature -= 15
    passes += 1
    print("Cooling SFSRC equipment: " + str(temperature))
print("Loop ran " + str(passes) + " times")
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-iterations-hw-1"
   language="python"
   challenge=challenge1
   code=code1
   source=source1
%}


## Homework Hack — Server load monitor

**Theme:** I'm monitoring CPU load (%) across 10 web servers in a data center. Loads under 50% are healthy and skipped. Loads 50%+ need a technician to rebalance traffic. A load of 95%+ is critical — the server is about to crash, so the scan stops and the on-call engineer is paged.

**Prediction:** 32 skip, 47 skip, 68 action, 55 action, 21 skip, 74 action, 97 critical → stop. Checked 7, skipped 3, actions 4, total 68 + 55 + 74 + 97 = 294, critical True.



{% capture challenge2 %}
{% raw %}
Homework Hack - server load monitor
{% endraw %}
{% endcapture %}

{% capture code2 %}
{% raw %}
# Theme: CPU load (%) for each web server in a data center.
# Goal: skip healthy servers, count servers that need rebalancing, total their load,
# and stop at the first server that is about to crash.

server_loads = [32, 47, 68, 55, 21, 74, 97, 88, 40, 61]   # 10 servers

healthy_cutoff = 50     # loads below this are healthy -> continue
critical_cutoff = 95    # loads at or above this -> page on-call engineer and break

checked_count = 0
rebalance_count = 0
healthy_count = 0
total_load = 0
critical_found = False

for load in server_loads:
    checked_count += 1

    if load < healthy_cutoff:
        healthy_count += 1
        print("Server at " + str(load) + "%: healthy, no action")
        continue

    rebalance_count += 1
    total_load += load
    print("Server at " + str(load) + "%: rebalance traffic")

    if load >= critical_cutoff:
        critical_found = True
        print("CRITICAL: server at " + str(load) + "% - paging on-call engineer. Stop checking.")
        break

print("Final Report")
print("Servers checked: " + str(checked_count))
print("Healthy (skipped): " + str(healthy_count))
print("Needed rebalancing: " + str(rebalance_count))
print("Total load of busy servers: " + str(total_load) + "%")
print("Critical server found: " + str(critical_found))
{% endraw %}
{% endcapture %}

{% capture source2 %}
{% raw %}
```python
# CODE_RUNNER: Homework Hack - server load monitor
# Theme: CPU load (%) for each web server in a data center.
# Goal: skip healthy servers, count servers that need rebalancing, total their load,
# and stop at the first server that is about to crash.

server_loads = [32, 47, 68, 55, 21, 74, 97, 88, 40, 61]   # 10 servers

healthy_cutoff = 50     # loads below this are healthy -> continue
critical_cutoff = 95    # loads at or above this -> page on-call engineer and break

checked_count = 0
rebalance_count = 0
healthy_count = 0
total_load = 0
critical_found = False

for load in server_loads:
    checked_count += 1

    if load < healthy_cutoff:
        healthy_count += 1
        print("Server at " + str(load) + "%: healthy, no action")
        continue

    rebalance_count += 1
    total_load += load
    print("Server at " + str(load) + "%: rebalance traffic")

    if load >= critical_cutoff:
        critical_found = True
        print("CRITICAL: server at " + str(load) + "% - paging on-call engineer. Stop checking.")
        break

print("Final Report")
print("Servers checked: " + str(checked_count))
print("Healthy (skipped): " + str(healthy_count))
print("Needed rebalancing: " + str(rebalance_count))
print("Total load of busy servers: " + str(total_load) + "%")
print("Critical server found: " + str(critical_found))
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-iterations-hw-2"
   language="python"
   challenge=challenge2
   code=code2
   source=source2
%}


**Second test — no critical server.** Replacing the 97 with 80 shows that the loop visits every value when `break` never runs:



{% capture challenge3 %}
{% raw %}
Homework test 2 - no critical server, loop checks all 10
{% endraw %}
{% endcapture %}

{% capture code3 %}
{% raw %}
server_loads = [32, 47, 68, 55, 21, 74, 80, 88, 40, 61]
healthy_cutoff = 50
critical_cutoff = 95
checked_count = 0
rebalance_count = 0
healthy_count = 0
total_load = 0
critical_found = False

for load in server_loads:
    checked_count += 1
    if load < healthy_cutoff:
        healthy_count += 1
        continue
    rebalance_count += 1
    total_load += load
    if load >= critical_cutoff:
        critical_found = True
        break

print("Checked: " + str(checked_count) + ", Healthy: " + str(healthy_count)
      + ", Rebalance: " + str(rebalance_count) + ", Total: " + str(total_load)
      + ", Critical: " + str(critical_found))
{% endraw %}
{% endcapture %}

{% capture source3 %}
{% raw %}
```python
# CODE_RUNNER: Homework test 2 - no critical server, loop checks all 10
server_loads = [32, 47, 68, 55, 21, 74, 80, 88, 40, 61]
healthy_cutoff = 50
critical_cutoff = 95
checked_count = 0
rebalance_count = 0
healthy_count = 0
total_load = 0
critical_found = False

for load in server_loads:
    checked_count += 1
    if load < healthy_cutoff:
        healthy_count += 1
        continue
    rebalance_count += 1
    total_load += load
    if load >= critical_cutoff:
        critical_found = True
        break

print("Checked: " + str(checked_count) + ", Healthy: " + str(healthy_count)
      + ", Rebalance: " + str(rebalance_count) + ", Total: " + str(total_load)
      + ", Critical: " + str(critical_found))
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-iterations-hw-3"
   language="python"
   challenge=challenge3
   code=code3
   source=source3
%}


**Why each tool:** a `for` loop because the list of servers is known; `continue` because a healthy server should be ignored without stopping the scan; `break` because once one server is about to crash the team must focus on it immediately; the counters and running total start at 0 before the loop because nothing has been processed yet.

### Submission notes

```text
Lesson: Python 3.08 Iterations
MCQ 3.08: 4/4 | answers: A,B,A,B
Popcorn: completed loop variable, thresholds, counters, continue, and break (yes)
Homework: list length = 10
Homework: thresholds = 50, 95
Homework: final checked count = 7
Homework: final action count = 4
Homework: critical found = yes
```

**Grading checklist:** at least 8 values ✔ · 2 thresholds ✔ · `for` loop ✔ · `continue` skips safe values ✔ · `break` stops at critical ✔ · checked/skipped/action/total/critical tracked and printed ✔

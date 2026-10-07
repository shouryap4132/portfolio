---
layout: post
codemirror: True
title: 3.12 Calling Procedures HW
categories: ['Python', 'Calling-Procedures']
lesson_language: Python
lesson_topic: Calling-Procedures
lesson_part: interactive
lesson_type: lesson
permalink: /csp/python/calling-procedures/hw
author: Shourya Patel
---

# 3.12 Calling Procedures — Homework

Poway Neighborhood Emergency Corps theme. Includes the Quick Knowledge Check, both Popcorn Hacks, and the Homework Hack.

## Quick Knowledge Check

| # | Question | Answer | Why |
|---|---|---|---|
| 1 | What is a procedure (function)? | **B** A named set of reusable code instructions | |
| 2 | Defining vs. calling | **B** Defining creates it, calling executes it | `def` defines; `name()` calls |
| 3 | In `def report_incident(location):`, `location` is | **B** A parameter | it's in the definition |
| 4 | What is an argument? | **B** The actual value passed in when it is called | e.g. `"Poway"` |
| 5 | Why are parameters useful? | **A** Same procedure works with different data | |

**Score: 5/5 | answers: B,B,B,B,A**

## Popcorn Hack 1: Simple Procedure Call & Parameters



{% capture challenge0 %}
{% raw %}
Procedures Popcorn #1
{% endraw %}
{% endcapture %}

{% capture code0 %}
{% raw %}
def report_status(location, status):
    # location and status are PARAMETERS
    print("Status update from " + location + ": " + status)

# "Poway", "All clear", etc. are ARGUMENTS
report_status("Poway", "All clear")
report_status("Rancho Bernardo", "Road closed due to flooding")
{% endraw %}
{% endcapture %}

{% capture source0 %}
{% raw %}
```python
# CODE_RUNNER: Procedures Popcorn #1

def report_status(location, status):
    # location and status are PARAMETERS
    print("Status update from " + location + ": " + status)

# "Poway", "All clear", etc. are ARGUMENTS
report_status("Poway", "All clear")
report_status("Rancho Bernardo", "Road closed due to flooding")
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="csp-python-calling-procedures-hw-0"
   language="python"
   challenge=challenge0
   code=code0
   source=source0
%}


## Popcorn Hack 2: Decomposition & Helper Procedures



{% capture challenge1 %}
{% raw %}
Popcorn Hack 2 - Decomposition & Helper Procedures
{% endraw %}
{% endcapture %}

{% capture code1 %}
{% raw %}
# Helper Procedure
def is_priority(incident_type):
    return incident_type == "Medical Emergency"

# Outer Procedure
def process_report(location, incident_type):
    priority = is_priority(incident_type)      # call the helper, store its returned Boolean
    if priority:
        print("PRIORITY: " + incident_type + " reported in " + location)
    else:
        print("STANDARD REPORT: " + incident_type + " reported in " + location)

process_report("Poway", "Medical Emergency")
process_report("Poway", "Power Outage")
{% endraw %}
{% endcapture %}

{% capture source1 %}
{% raw %}
```python
# CODE_RUNNER: Popcorn Hack 2 - Decomposition & Helper Procedures

# Helper Procedure
def is_priority(incident_type):
    return incident_type == "Medical Emergency"

# Outer Procedure
def process_report(location, incident_type):
    priority = is_priority(incident_type)      # call the helper, store its returned Boolean
    if priority:
        print("PRIORITY: " + incident_type + " reported in " + location)
    else:
        print("STANDARD REPORT: " + incident_type + " reported in " + location)

process_report("Poway", "Medical Emergency")
process_report("Poway", "Power Outage")
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="csp-python-calling-procedures-hw-1"
   language="python"
   challenge=challenge1
   code=code1
   source=source1
%}


## Homework Hack — Emergency Dispatch Program

`check_priority()` returns a Boolean; `dispatch_response()` calls it and prints a different response based on the result. I treat medical emergencies, fires and gas leaks as priority incidents.



{% capture challenge2 %}
{% raw %}
Homework Hack - Poway emergency dispatch
{% endraw %}
{% endcapture %}

{% capture code2 %}
{% raw %}
PRIORITY_INCIDENTS = ["Medical Emergency", "Wildfire", "Gas Leak"]

def check_priority(incident_type):
    """Return True when the incident requires priority handling."""
    return incident_type in PRIORITY_INCIDENTS

def dispatch_response(location, incident_type):
    """Decide and print how PNEC responds to an incident at a location."""
    priority = check_priority(incident_type)       # helper procedure call
    if priority:
        print("PRIORITY DISPATCH: Sending first responders to " + location
              + " for a " + incident_type + ". Notify all volunteers.")
    else:
        print("STANDARD RESPONSE: Logging " + incident_type + " in " + location
              + ". A volunteer will follow up within 24 hours.")

dispatch_response("Poway", "Medical Emergency")
dispatch_response("Green Valley", "Power Outage")
dispatch_response("Old Poway Park", "Wildfire")
dispatch_response("Twin Peaks", "Downed Tree")
dispatch_response("Poway Road", "Gas Leak")
{% endraw %}
{% endcapture %}

{% capture source2 %}
{% raw %}
```python
# CODE_RUNNER: Homework Hack - Poway emergency dispatch

PRIORITY_INCIDENTS = ["Medical Emergency", "Wildfire", "Gas Leak"]

def check_priority(incident_type):
    """Return True when the incident requires priority handling."""
    return incident_type in PRIORITY_INCIDENTS

def dispatch_response(location, incident_type):
    """Decide and print how PNEC responds to an incident at a location."""
    priority = check_priority(incident_type)       # helper procedure call
    if priority:
        print("PRIORITY DISPATCH: Sending first responders to " + location
              + " for a " + incident_type + ". Notify all volunteers.")
    else:
        print("STANDARD RESPONSE: Logging " + incident_type + " in " + location
              + ". A volunteer will follow up within 24 hours.")

dispatch_response("Poway", "Medical Emergency")
dispatch_response("Green Valley", "Power Outage")
dispatch_response("Old Poway Park", "Wildfire")
dispatch_response("Twin Peaks", "Downed Tree")
dispatch_response("Poway Road", "Gas Leak")
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="csp-python-calling-procedures-hw-2"
   language="python"
   challenge=challenge2
   code=code2
   source=source2
%}


**Decomposition explained:** `dispatch_response` handles the main task (deciding and printing the response) and hands the sub-task "is this a priority?" to `check_priority`. If the list of priority incidents changes, I only edit the helper — every call to `dispatch_response` automatically uses the new rule. The same two procedures handled five different incidents with no repeated code; only the arguments changed.

**Checklist:** procedures made with `def` ✔ · parameters ✔ · called with different arguments ✔ · outer procedure calls helper ✔ · helper returns a Boolean ✔ · 5 calls with different locations and incident types ✔

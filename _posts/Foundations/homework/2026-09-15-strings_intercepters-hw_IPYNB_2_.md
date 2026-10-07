---
layout: post
codemirror: True
title: 3.4 Strings HW
categories: ['Python']
lesson_language: Python
lesson_topic: Strings HW
lesson_part: interactive
lesson_type: lesson
permalink: /python/strings-intercepters-hw
author: Shourya Patel
---

# 3.4 Strings — Signal Interceptor Homework

All three Popcorn Hacks and the Homework Hack are complete. Every cell keeps `# CODE_RUNNER:` as its first line, uses no imports, and no `input()`.

## Warm-up: immutability

Trying `message[0] = "J"` raises `TypeError: 'str' object does not support item assignment`, because strings are **immutable**. I caught the error to show it, then built a new string instead.



{% capture challenge0 %}
{% raw %}
Immutability check - editing fails, building a new string works
{% endraw %}
{% endcapture %}

{% capture code0 %}
{% raw %}
message = "HELLO"
try:
    message[0] = "J"
except TypeError as error:
    print("TypeError:", error)

fixed = "J" + message[1:]
print(fixed)
print(message)   # the original is untouched
{% endraw %}
{% endcapture %}

{% capture source0 %}
{% raw %}
```python
# CODE_RUNNER: Immutability check - editing fails, building a new string works
message = "HELLO"
try:
    message[0] = "J"
except TypeError as error:
    print("TypeError:", error)

fixed = "J" + message[1:]
print(fixed)
print(message)   # the original is untouched
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-strings-intercepters-hw-0"
   language="python"
   challenge=challenge0
   code=code0
   source=source0
%}


## Popcorn Hack 1: Extract the Hidden Message

Positions in `"xxSIGNALxxxCONFIRMEDxx77xxDELTA"`: `SIGNAL` is 2–7, `xxx` is 8–10, `CONFIRMED` is 11–19, and `DELTA` is the last 5 characters (26–30). Total length is 31.



{% capture challenge1 %}
{% raw %}
Popcorn Hack 1 - Extract the hidden message using indexing and slicing
{% endraw %}
{% endcapture %}

{% capture code1 %}
{% raw %}
transmission = "xxSIGNALxxxCONFIRMEDxx77xxDELTA"

# TODO 1: "SIGNAL" starts at index 2 and is 6 characters long -> stop at 2 + 6 = 8
word_1 = transmission[2:8]
print("Word 1:", word_1)

# TODO 2: "CONFIRMED" starts right after "SIGNALxxx" (index 11) and is 9 characters long
word_2 = transmission[11:20]
print("Word 2:", word_2)

# TODO 3: negative slicing for the last 5 characters
word_3 = transmission[-5:]
print("Word 3:", word_3)

# TODO 4: total length
print("Total length:", len(transmission))

# TODO 5: every other character
print("Every other character:", transmission[::2])
{% endraw %}
{% endcapture %}

{% capture source1 %}
{% raw %}
```python
# CODE_RUNNER: Popcorn Hack 1 - Extract the hidden message using indexing and slicing

transmission = "xxSIGNALxxxCONFIRMEDxx77xxDELTA"

# TODO 1: "SIGNAL" starts at index 2 and is 6 characters long -> stop at 2 + 6 = 8
word_1 = transmission[2:8]
print("Word 1:", word_1)

# TODO 2: "CONFIRMED" starts right after "SIGNALxxx" (index 11) and is 9 characters long
word_2 = transmission[11:20]
print("Word 2:", word_2)

# TODO 3: negative slicing for the last 5 characters
word_3 = transmission[-5:]
print("Word 3:", word_3)

# TODO 4: total length
print("Total length:", len(transmission))

# TODO 5: every other character
print("Every other character:", transmission[::2])
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-strings-intercepters-hw-1"
   language="python"
   challenge=challenge1
   code=code1
   source=source1
%}


**Is any part of the hidden message still visible with a step of 2?** Only fragments. The output `xSGAxxOFREx7xDLA` keeps `SGA` (from SIGNAL), `OFRE` (from CONFIRMED) and `DLA` (from DELTA), but no full word survives. Each word needs its *consecutive* characters, so skipping every other one breaks it up.

## Popcorn Hack 2: Scrub and Search a Noisy Transmission



{% capture challenge2 %}
{% raw %}
Popcorn Hack 2 - Clean and search a noisy transmission using string methods
{% endraw %}
{% endcapture %}

{% capture code2 %}
{% raw %}
noisy = "   ...AGENT>>>Falcon---reports: the PACKAGE has ARRIVED!!!   "

# TODO 1: remove leading/trailing whitespace
trimmed = noisy.strip()
print("Trimmed:", repr(trimmed))

# TODO 2: remove every ">", "-", and "!" (one .replace() per character)
cleaned = trimmed.replace(">", " ").replace("-", " ").replace("!", "")
print("Cleaned:", cleaned)

# TODO 3: all-lowercase copy
lowered = cleaned.lower()
print("Lowered:", lowered)

# TODO 4: search with `in`
has_arrived = "arrived" in lowered
print("Contains 'arrived':", has_arrived)

# TODO 5: split into words and count them
words = cleaned.split()
print("Words:", words)
print("Word count:", len(words))

# Every method returned a NEW string - the original is unchanged
print("Original still noisy:", repr(noisy))
{% endraw %}
{% endcapture %}

{% capture source2 %}
{% raw %}
```python
# CODE_RUNNER: Popcorn Hack 2 - Clean and search a noisy transmission using string methods

noisy = "   ...AGENT>>>Falcon---reports: the PACKAGE has ARRIVED!!!   "

# TODO 1: remove leading/trailing whitespace
trimmed = noisy.strip()
print("Trimmed:", repr(trimmed))

# TODO 2: remove every ">", "-", and "!" (one .replace() per character)
cleaned = trimmed.replace(">", " ").replace("-", " ").replace("!", "")
print("Cleaned:", cleaned)

# TODO 3: all-lowercase copy
lowered = cleaned.lower()
print("Lowered:", lowered)

# TODO 4: search with `in`
has_arrived = "arrived" in lowered
print("Contains 'arrived':", has_arrived)

# TODO 5: split into words and count them
words = cleaned.split()
print("Words:", words)
print("Word count:", len(words))

# Every method returned a NEW string - the original is unchanged
print("Original still noisy:", repr(noisy))
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-strings-intercepters-hw-2"
   language="python"
   challenge=challenge2
   code=code2
   source=source2
%}


I replaced `>` and `-` with a **space** (instead of an empty string) so `AGENT`, `Falcon`, and `reports:` stay separate words when I call `.split()`. `.split()` with no argument also ignores the extra spaces, so the word count is correct. The `...` at the start stays attached to the first word (`...AGENT`) because the task only asked to remove `>`, `-`, and `!`.

## Popcorn Hack 3: Build a Decoded Report



{% capture challenge3 %}
{% raw %}
Popcorn Hack 3 - Build a decoded report using concatenation and formatting
{% endraw %}
{% endcapture %}

{% capture code3 %}
{% raw %}
agent_name = "Falcon"
target_word = "MIDNIGHT"
confidence = 87          # a percentage, stored as an int
fragments = ["ALPHA", "SEVEN", "DELTA"]

# TODO 1: + concatenation
headline = "Agent " + agent_name + " intercepted: " + target_word
print(headline)

# TODO 2: str() + concatenation (confidence is an int)
confidence_line = "Confidence: " + str(confidence) + "%"
print(confidence_line)

# TODO 3: same line with an f-string
confidence_line_fstring = f"Confidence: {confidence}%"
print(confidence_line_fstring)

# TODO 4: join the fragments with "-"
joined_fragments = "-".join(fragments)
print("Joined fragments:", joined_fragments)

# TODO 5: one final report line with an f-string
final_report = f"REPORT: {headline} | {confidence_line} | Fragments: {joined_fragments}"
print(final_report)

print(confidence_line == confidence_line_fstring)   # both styles build the same string
{% endraw %}
{% endcapture %}

{% capture source3 %}
{% raw %}
```python
# CODE_RUNNER: Popcorn Hack 3 - Build a decoded report using concatenation and formatting

agent_name = "Falcon"
target_word = "MIDNIGHT"
confidence = 87          # a percentage, stored as an int
fragments = ["ALPHA", "SEVEN", "DELTA"]

# TODO 1: + concatenation
headline = "Agent " + agent_name + " intercepted: " + target_word
print(headline)

# TODO 2: str() + concatenation (confidence is an int)
confidence_line = "Confidence: " + str(confidence) + "%"
print(confidence_line)

# TODO 3: same line with an f-string
confidence_line_fstring = f"Confidence: {confidence}%"
print(confidence_line_fstring)

# TODO 4: join the fragments with "-"
joined_fragments = "-".join(fragments)
print("Joined fragments:", joined_fragments)

# TODO 5: one final report line with an f-string
final_report = f"REPORT: {headline} | {confidence_line} | Fragments: {joined_fragments}"
print(final_report)

print(confidence_line == confidence_line_fstring)   # both styles build the same string
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-strings-intercepters-hw-3"
   language="python"
   challenge=challenge3
   code=code3
   source=source3
%}


## Homework Hack: Crack the Final Transmission

Uses all three skills: splitting/indexing, slicing, string methods, and formatting (Markdown row + JSON line).



{% capture challenge4 %}
{% raw %}
Homework - Crack the Final Transmission using slicing, methods, and formatting
{% endraw %}
{% endcapture %}

{% capture code4 %}
{% raw %}
raw_transmission = "  2026-09-15,GHOST,THE-EAGLE-LANDS-AT-DAWN,87  "

# TODO 1: strip outer whitespace, then split the CSV row on ","
segments = raw_transmission.strip().split(",")
print("Segments:", segments)
print("Field count:", len(segments))

# TODO 2: pull each field out by index
date = segments[0]
agent = segments[1]
message_code = segments[2]
confidence_str = segments[3]
print("Date:", date, "| Agent:", agent, "| Message code:", message_code, "| Confidence:", confidence_str)

# TODO 3: SLICING (not a method) to check the year
year_check = date[0:4] == "2026"
print("Year slice:", date[0:4])
print("Year check:", year_check)

# TODO 4: dashes -> spaces
message = message_code.replace("-", " ")
print("Message:", message)

# TODO 5: case-insensitive search for "dawn"
found_dawn = "dawn" in message.lower()
print("Found 'dawn':", found_dawn)

# TODO 6: Markdown table row with "|" separators
markdown_row = f"| {date} | {agent} | {message} | {confidence_str}% |"
print("Markdown row:", markdown_row)

# TODO 7: JSON-style line (lowercase boolean for JSON)
json_line = f'{{"date": "{date}", "agent": "{agent}", "message": "{message}", "confidence": {confidence_str}, "contains_dawn": {str(found_dawn).lower()}}}'
print("JSON line:", json_line)
{% endraw %}
{% endcapture %}

{% capture source4 %}
{% raw %}
```python
# CODE_RUNNER: Homework - Crack the Final Transmission using slicing, methods, and formatting

raw_transmission = "  2026-09-15,GHOST,THE-EAGLE-LANDS-AT-DAWN,87  "

# TODO 1: strip outer whitespace, then split the CSV row on ","
segments = raw_transmission.strip().split(",")
print("Segments:", segments)
print("Field count:", len(segments))

# TODO 2: pull each field out by index
date = segments[0]
agent = segments[1]
message_code = segments[2]
confidence_str = segments[3]
print("Date:", date, "| Agent:", agent, "| Message code:", message_code, "| Confidence:", confidence_str)

# TODO 3: SLICING (not a method) to check the year
year_check = date[0:4] == "2026"
print("Year slice:", date[0:4])
print("Year check:", year_check)

# TODO 4: dashes -> spaces
message = message_code.replace("-", " ")
print("Message:", message)

# TODO 5: case-insensitive search for "dawn"
found_dawn = "dawn" in message.lower()
print("Found 'dawn':", found_dawn)

# TODO 6: Markdown table row with "|" separators
markdown_row = f"| {date} | {agent} | {message} | {confidence_str}% |"
print("Markdown row:", markdown_row)

# TODO 7: JSON-style line (lowercase boolean for JSON)
json_line = f'{{"date": "{date}", "agent": "{agent}", "message": "{message}", "confidence": {confidence_str}, "contains_dawn": {str(found_dawn).lower()}}}'
print("JSON line:", json_line)
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-strings-intercepters-hw-4"
   language="python"
   challenge=challenge4
   code=code4
   source=source4
%}


{% raw %}
**How it works:** `.strip()` removes the outer spaces and `.split(",")` turns the CSV row into exactly 4 fields. Indexing `segments[0]`–`segments[3]` pulls out each field. `date[0:4]` is a slice (no method) that gives `"2026"`. `.replace("-", " ")` and `.lower()` + `in` clean and search the message. In the f-string for JSON, `{{` and `}}` print literal braces, and `str(found_dawn).lower()` turns Python's `True` into JSON's `true`.

**Extra test** — a different transmission to make sure nothing is hard-coded:
{% endraw %}



{% capture challenge5 %}
{% raw %}
Homework extra test - a transmission without "dawn"
{% endraw %}
{% endcapture %}

{% capture code5 %}
{% raw %}
raw_transmission = " 2025-12-01,RAVEN,MEET-AT-THE-DOCKS-AT-NOON,42 "
segments = raw_transmission.strip().split(",")
date, agent, message_code, confidence_str = segments[0], segments[1], segments[2], segments[3]
message = message_code.replace("-", " ")
found_dawn = "dawn" in message.lower()
print("Year check:", date[0:4] == "2026")
print(f"| {date} | {agent} | {message} | {confidence_str}% |")
print(f'{{"date": "{date}", "agent": "{agent}", "message": "{message}", "confidence": {confidence_str}, "contains_dawn": {str(found_dawn).lower()}}}')
{% endraw %}
{% endcapture %}

{% capture source5 %}
{% raw %}
```python
# CODE_RUNNER: Homework extra test - a transmission without "dawn"
raw_transmission = " 2025-12-01,RAVEN,MEET-AT-THE-DOCKS-AT-NOON,42 "
segments = raw_transmission.strip().split(",")
date, agent, message_code, confidence_str = segments[0], segments[1], segments[2], segments[3]
message = message_code.replace("-", " ")
found_dawn = "dawn" in message.lower()
print("Year check:", date[0:4] == "2026")
print(f"| {date} | {agent} | {message} | {confidence_str}% |")
print(f'{{"date": "{date}", "agent": "{agent}", "message": "{message}", "confidence": {confidence_str}, "contains_dawn": {str(found_dawn).lower()}}}')
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-strings-intercepters-hw-5"
   language="python"
   challenge=challenge5
   code=code5
   source=source5
%}


The second test correctly reports `Year check: False` and `"contains_dawn": false`.

**Checklist:** `# CODE_RUNNER:` first line ✔ · slicing without a method (`date[0:4]`) ✔ · at least three string methods (`.strip()`, `.split()`, `.replace()`, `.lower()`, `.join()`) ✔ · Markdown row and JSON line ✔ · no `input()`, no imports ✔

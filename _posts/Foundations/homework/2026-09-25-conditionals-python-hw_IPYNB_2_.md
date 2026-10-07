---
layout: post
codemirror: True
title: 3.6 Conditionals HW
categories: ['Python']
lesson_language: Python
lesson_topic: Conditionals HW
lesson_part: interactive
lesson_type: lesson
permalink: /python/conditionals-hw
author: Shourya Patel
---

# 3.6 Conditionals — Scam Trainer Homework

Both Popcorn Hacks (fixed) and the full Homework Hack: scoring step, reporting chain, count comment, reachability proof, extreme tests, and the stretch question.

## Example A check — comparisons make conditions



{% capture challenge0 %}
{% raw %}
3.6 - Comparisons make conditions. Every line prints True or False.
{% endraw %}
{% endcapture %}

{% capture code0 %}
{% raw %}
message = "URGENT: send $500 in gift cards today to unlock your account"
amount_requested = 500
known_contact = False

print("gift card" in message)
print(amount_requested > 100)
print(amount_requested == 0)
print(known_contact)
print(len(message) > 200)
{% endraw %}
{% endcapture %}

{% capture source0 %}
{% raw %}
```python
# CODE_RUNNER: 3.6 - Comparisons make conditions. Every line prints True or False.
message = "URGENT: send $500 in gift cards today to unlock your account"
amount_requested = 500
known_contact = False

print("gift card" in message)
print(amount_requested > 100)
print(amount_requested == 0)
print(known_contact)
print(len(message) > 200)
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-conditionals-hw-0"
   language="python"
   challenge=challenge0
   code=code0
   source=source0
%}


## Popcorn Hack 1 — the silent failure

**Step 1 — run it unchanged:** with `amount_requested = 0` it prints **nothing**. That is a **bug, not an error**: Python ran it successfully, but one of the two outcomes has no answer, so silence looks like "this is fine."

**Step 2 — fixed:**



{% capture challenge1 %}
{% raw %}
3.6 Popcorn 1 - Both outcomes now print.
{% endraw %}
{% endcapture %}

{% capture code1 %}
{% raw %}
for amount_requested in [0, 500]:     # test both outcomes
    # 1 condition -> 2 outcomes -> 2 answers
    if amount_requested > 100:
        print("This message is asking for a large amount of money.")
    else:
        print("This message is not asking for a large amount of money.")
{% endraw %}
{% endcapture %}

{% capture source1 %}
{% raw %}
```python
# CODE_RUNNER: 3.6 Popcorn 1 - Both outcomes now print.

for amount_requested in [0, 500]:     # test both outcomes
    # 1 condition -> 2 outcomes -> 2 answers
    if amount_requested > 100:
        print("This message is asking for a large amount of money.")
    else:
        print("This message is not asking for a large amount of money.")
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-conditionals-hw-1"
   language="python"
   challenge=challenge1
   code=code1
   source=source1
%}


## Popcorn Hack 2 — the chain in the wrong order

**Step 1:** with `risk_score = 9` the broken chain prints **"Be a little careful, but this is probably fine."** — it tells the person the worst possible scam is probably fine.

**Step 2 — unreachable branches:** the **first `elif` (`>= 6`)** and the **second `elif` (`>= 9`)** can never run. Any score that is 6+ or 9+ is also 3+, so the very first `if risk_score >= 3` catches it first and the `elif`s are never asked.

**Step 3 — fixed (highest threshold first), tested for every score 0–10:**



{% capture challenge2 %}
{% raw %}
3.6 Popcorn 2 - Fixed order, highest threshold first.
{% endraw %}
{% endcapture %}

{% capture code2 %}
{% raw %}
for risk_score in range(0, 11):
    # 3 thresholds -> 4 outcomes -> 4 answers
    if risk_score >= 9:
        advice = "Do not reply. This is almost certainly a scam."
    elif risk_score >= 6:
        advice = "This looks risky. Check with someone you trust before replying."
    elif risk_score >= 3:
        advice = "Be a little careful, but this is probably fine."
    else:
        advice = "Nothing suspicious in this message."
    print(risk_score, "->", advice)
{% endraw %}
{% endcapture %}

{% capture source2 %}
{% raw %}
```python
# CODE_RUNNER: 3.6 Popcorn 2 - Fixed order, highest threshold first.

for risk_score in range(0, 11):
    # 3 thresholds -> 4 outcomes -> 4 answers
    if risk_score >= 9:
        advice = "Do not reply. This is almost certainly a scam."
    elif risk_score >= 6:
        advice = "This looks risky. Check with someone you trust before replying."
    elif risk_score >= 3:
        advice = "Be a little careful, but this is probably fine."
    else:
        advice = "Nothing suspicious in this message."
    print(risk_score, "->", advice)
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-conditionals-hw-2"
   language="python"
   challenge=challenge2
   code=code2
   source=source2
%}


All four answers now appear, and score 9 gets "Do not reply."

## Homework Hack — build the trainer's scoring step



{% capture challenge3 %}
{% raw %}
3.6 Homework - score a message, then advise on it
{% endraw %}
{% endcapture %}

{% capture code3 %}
{% raw %}
def score_and_advise(message, amount_requested, known_contact):
    risk_score = 0

    # Scoring step: one separate if per signal.
    # None of these need an else: when a signal is absent, the right action is
    # "add nothing", and the score already starts at 0. Every signal is checked
    # independently, so a message can trip any combination of them.
    if "gift card" in message.lower():
        risk_score = risk_score + 4
    if amount_requested > 100:
        risk_score = risk_score + 3
    if not known_contact:
        risk_score = risk_score + 2

    print("Message:", message)
    print("Risk score:", risk_score)

    # 3 thresholds -> 4 outcomes -> 4 answers
    if risk_score >= 9:
        print("Advice: Do not reply. This is almost certainly a scam.")
    elif risk_score >= 6:
        print("Advice: This looks risky. Check with someone you trust before replying.")
    elif risk_score >= 3:
        print("Advice: Be a little careful, but this is probably fine.")
    else:
        print("Advice: Nothing suspicious in this message.")
    print()

# Starter data from the lesson
score_and_advise("URGENT: send gift cards now to unlock your account", 500, False)

# Reachability tests - one input per branch
score_and_advise("Please grab a gift card for grandma's birthday", 50, True)     # 4 -> careful
score_and_advise("Can you send the $200 for the concert tickets?", 200, False)   # 5 -> careful
score_and_advise("Buy gift cards and send me $300 today", 300, True)             # 7 -> risky

# Extreme tests
score_and_advise("Hi Mom, are we still on for Sunday?", 0, True)                  # clean -> 0
score_and_advise("URGENT gift card request, send $1000 now", 1000, False)         # every signal -> 9
{% endraw %}
{% endcapture %}

{% capture source3 %}
{% raw %}
```python
# CODE_RUNNER: 3.6 Homework - score a message, then advise on it

def score_and_advise(message, amount_requested, known_contact):
    risk_score = 0

    # Scoring step: one separate if per signal.
    # None of these need an else: when a signal is absent, the right action is
    # "add nothing", and the score already starts at 0. Every signal is checked
    # independently, so a message can trip any combination of them.
    if "gift card" in message.lower():
        risk_score = risk_score + 4
    if amount_requested > 100:
        risk_score = risk_score + 3
    if not known_contact:
        risk_score = risk_score + 2

    print("Message:", message)
    print("Risk score:", risk_score)

    # 3 thresholds -> 4 outcomes -> 4 answers
    if risk_score >= 9:
        print("Advice: Do not reply. This is almost certainly a scam.")
    elif risk_score >= 6:
        print("Advice: This looks risky. Check with someone you trust before replying.")
    elif risk_score >= 3:
        print("Advice: Be a little careful, but this is probably fine.")
    else:
        print("Advice: Nothing suspicious in this message.")
    print()

# Starter data from the lesson
score_and_advise("URGENT: send gift cards now to unlock your account", 500, False)

# Reachability tests - one input per branch
score_and_advise("Please grab a gift card for grandma's birthday", 50, True)     # 4 -> careful
score_and_advise("Can you send the $200 for the concert tickets?", 200, False)   # 5 -> careful
score_and_advise("Buy gift cards and send me $300 today", 300, True)             # 7 -> risky

# Extreme tests
score_and_advise("Hi Mom, are we still on for Sunday?", 0, True)                  # clean -> 0
score_and_advise("URGENT gift card request, send $1000 now", 1000, False)         # every signal -> 9
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-conditionals-hw-3"
   language="python"
   challenge=challenge3
   code=code3
   source=source3
%}


### Reachability proof (one input per branch)

Possible scores are sums of 4, 3 and 2: `0, 2, 3, 4, 5, 6, 7, 9`.

| Branch | Score range | Inputs that reach it | Score |
|---|---|---|---|
| `if risk_score >= 9` → "Do not reply" | 9 | mentions gift cards, asks for $1000, unknown sender | 4 + 3 + 2 = **9** |
| `elif risk_score >= 6` → "Check with someone you trust" | 6–8 | mentions gift cards, asks for $300, **known** sender | 4 + 3 = **7** |
| `elif risk_score >= 3` → "Be a little careful" | 3–5 | mentions gift cards, asks for $50, known sender | **4** |
| `else` → "Nothing suspicious" | 0–2 | no gift cards, $0, known sender (Hi Mom message) | **0** |

Every branch has an input that reaches it, so there is no dead code, and the final `else` catches every score below 3 so nothing falls off the end.

### Extreme tests

- **Clean message** (`"Hi Mom, are we still on for Sunday?"`, $0, known contact) → score 0 → "Nothing suspicious in this message."
- **Every signal** (gift cards, $1000, unknown sender) → score 9 → "Do not reply. This is almost certainly a scam."

Both print a sensible answer.

### Stretch: why is `if` with no `else` fine here?

In the scoring step, the "no" outcome of each signal really is "do nothing" (add 0 points) and the reporting chain still prints for every input, whereas in Example A the missing `else` was the *only* output, so the "no" outcome printed nothing at all.

**Submission note:** 3.6 Conditionals popcorn + homework complete

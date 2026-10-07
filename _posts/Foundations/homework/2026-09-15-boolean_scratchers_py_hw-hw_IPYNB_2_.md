---
layout: post
codemirror: True
title: 3.05 Boolean Expressions HW
categories: ['Python']
lesson_language: Python
lesson_topic: Boolean-Expressions HW
lesson_part: interactive
lesson_type: lesson
permalink: /python/boolean-hw
author: Shourya Patel
---

# 3.05 Boolean Expressions — SFI Backend Homework

Includes all three Popcorn Hacks (with predictions and output), the MCQ result, the pseudocode check and the independent Homework Hack validator with tests.

## Popcorn Hack 1: Check SFI Part Fields

**Prediction:** every field is filled in and `"Auto Racing"` is in the accepted list, so all four checks print `True` and the record is complete.



{% capture challenge0 %}
{% raw %}
Popcorn Hack 1 - Check SFI Part Fields
{% endraw %}
{% endcapture %}

{% capture code0 %}
{% raw %}
part = {
    "product_name": "Replacement Flywheels and Clutch Assemblies",
    "category": "Auto Racing",
    "spec_number": "1.1",
    "effective_date": "Nov. 9, 2001"
}

valid_categories = ["Auto Racing", "Drag Racing"]

def check_fields(part):
    has_product_name = part["product_name"] != ""
    valid_category = part["category"] in valid_categories
    has_spec_number = part["spec_number"] != ""
    has_effective_date = part["effective_date"] != ""
    print("Has product name:", has_product_name)
    print("Valid racing category:", valid_category)
    print("Has spec number:", has_spec_number)
    print("Has effective date:", has_effective_date)
    print("Record complete:", has_product_name and valid_category and has_spec_number and has_effective_date)

check_fields(part)

# Changed input: a Street Car record with no effective date
print("--- changed input ---")
changed = dict(part, category="Street Car", effective_date="")
check_fields(changed)
{% endraw %}
{% endcapture %}

{% capture source0 %}
{% raw %}
```python
# CODE_RUNNER: Popcorn Hack 1 - Check SFI Part Fields

part = {
    "product_name": "Replacement Flywheels and Clutch Assemblies",
    "category": "Auto Racing",
    "spec_number": "1.1",
    "effective_date": "Nov. 9, 2001"
}

valid_categories = ["Auto Racing", "Drag Racing"]

def check_fields(part):
    has_product_name = part["product_name"] != ""
    valid_category = part["category"] in valid_categories
    has_spec_number = part["spec_number"] != ""
    has_effective_date = part["effective_date"] != ""
    print("Has product name:", has_product_name)
    print("Valid racing category:", valid_category)
    print("Has spec number:", has_spec_number)
    print("Has effective date:", has_effective_date)
    print("Record complete:", has_product_name and valid_category and has_spec_number and has_effective_date)

check_fields(part)

# Changed input: a Street Car record with no effective date
print("--- changed input ---")
changed = dict(part, category="Street Car", effective_date="")
check_fields(changed)
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-boolean-hw-0"
   language="python"
   challenge=challenge0
   code=code0
   source=source0
%}


**Actual:** all `True` for the original record. After changing the category to `"Street Car"` and blanking the date, `Valid racing category` and `Has effective date` become `False`, so `Record complete` is `False`.

## Popcorn Hack 2: Backend Create Rule

**Prediction:** spec `1.1` is already stored, so even though every field is valid, the create decision is `False` (rejected). Changing the spec to `1.2` should make it `True`.



{% capture challenge1 %}
{% raw %}
Popcorn Hack 2 - Backend Create Rule
{% endraw %}
{% endcapture %}

{% capture code1 %}
{% raw %}
part = {
    "product_name": "Replacement Flywheels and Clutch Assemblies",
    "category": "Auto Racing",
    "spec_number": "1.1",
    "effective_date": "Nov. 9, 2001"
}

valid_categories = ["Auto Racing", "Drag Racing"]
existing_spec_numbers = ["1.1", "2.1"]

def can_create(part):
    fields_valid = (
        part["product_name"] != ""
        and part["category"] in valid_categories
        and part["spec_number"] != ""
        and part["effective_date"] != ""
    )
    duplicate_spec = part["spec_number"] in existing_spec_numbers
    return fields_valid and not duplicate_spec

# Rejected case: duplicate spec number
print("Spec 1.1 -> create record:", can_create(part))

# Valid case: new spec number
new_part = dict(part, spec_number="1.2")
print("Spec 1.2 -> create record:", can_create(new_part))

# Rejected case: new spec but missing product name
print("Spec 3.0, no name -> create record:", can_create(dict(part, spec_number="3.0", product_name="")))
{% endraw %}
{% endcapture %}

{% capture source1 %}
{% raw %}
```python
# CODE_RUNNER: Popcorn Hack 2 - Backend Create Rule

part = {
    "product_name": "Replacement Flywheels and Clutch Assemblies",
    "category": "Auto Racing",
    "spec_number": "1.1",
    "effective_date": "Nov. 9, 2001"
}

valid_categories = ["Auto Racing", "Drag Racing"]
existing_spec_numbers = ["1.1", "2.1"]

def can_create(part):
    fields_valid = (
        part["product_name"] != ""
        and part["category"] in valid_categories
        and part["spec_number"] != ""
        and part["effective_date"] != ""
    )
    duplicate_spec = part["spec_number"] in existing_spec_numbers
    return fields_valid and not duplicate_spec

# Rejected case: duplicate spec number
print("Spec 1.1 -> create record:", can_create(part))

# Valid case: new spec number
new_part = dict(part, spec_number="1.2")
print("Spec 1.2 -> create record:", can_create(new_part))

# Rejected case: new spec but missing product name
print("Spec 3.0, no name -> create record:", can_create(dict(part, spec_number="3.0", product_name="")))
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-boolean-hw-1"
   language="python"
   challenge=challenge1
   code=code1
   source=source1
%}


**Actual:** `False`, `True`, `False`. The rule is `fields_valid and not duplicate_spec`: every field must pass **and** the spec must be new.

## Popcorn Hack 3: SFI Search Filter

**Prediction:** query `"1.2"` matches only the Multiple Disc Clutch record (by spec number). A query of `"flywheel"` should match both flywheel records by name.



{% capture challenge2 %}
{% raw %}
Popcorn Hack 3 - SFI Search Filter
{% endraw %}
{% endcapture %}

{% capture code2 %}
{% raw %}
query = "1.2"

records = [
    {"product_name": "Replacement Flywheels and Clutch Assemblies", "category": "Auto Racing", "spec_number": "1.1"},
    {"product_name": "Multiple Disc Clutch Assemblies", "category": "Drag Racing", "spec_number": "1.2"},
    {"product_name": "Racing Flywheel Record", "category": "Auto Racing", "spec_number": "2.1"},
    {"product_name": "Street Flywheel", "category": "Street Car", "spec_number": "9.9"}   # extra test record
]

valid_categories = ["Auto Racing", "Drag Racing"]

def search(query, records):
    matches = []
    for record in records:
        name_match = query.lower() in record["product_name"].lower()
        spec_match = query == record["spec_number"]
        accepted = record["category"] in valid_categories
        if (name_match or spec_match) and accepted:
            matches.append(record["product_name"])
    return matches

print("Query '1.2':", search("1.2", records))
print("Query 'flywheel':", search("flywheel", records))
print("Query 'brake':", search("brake", records))
{% endraw %}
{% endcapture %}

{% capture source2 %}
{% raw %}
```python
# CODE_RUNNER: Popcorn Hack 3 - SFI Search Filter

query = "1.2"

records = [
    {"product_name": "Replacement Flywheels and Clutch Assemblies", "category": "Auto Racing", "spec_number": "1.1"},
    {"product_name": "Multiple Disc Clutch Assemblies", "category": "Drag Racing", "spec_number": "1.2"},
    {"product_name": "Racing Flywheel Record", "category": "Auto Racing", "spec_number": "2.1"},
    {"product_name": "Street Flywheel", "category": "Street Car", "spec_number": "9.9"}   # extra test record
]

valid_categories = ["Auto Racing", "Drag Racing"]

def search(query, records):
    matches = []
    for record in records:
        name_match = query.lower() in record["product_name"].lower()
        spec_match = query == record["spec_number"]
        accepted = record["category"] in valid_categories
        if (name_match or spec_match) and accepted:
            matches.append(record["product_name"])
    return matches

print("Query '1.2':", search("1.2", records))
print("Query 'flywheel':", search("flywheel", records))
print("Query 'brake':", search("brake", records))
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-boolean-hw-2"
   language="python"
   challenge=challenge2
   code=code2
   source=source2
%}


**Actual:** `'1.2'` → `['Multiple Disc Clutch Assemblies']`; `'flywheel'` → both Auto Racing flywheel records, but **not** "Street Flywheel" because its category is not accepted; `'brake'` → `[]`. The condition `(name_match or spec_match) and accepted` needs the parentheses: either kind of match is enough, but the category must always be accepted.

## MCQ

| # | Question | Answer |
|---|---|---|
| 1 | `7 >= 7` evaluates to | **A** True |
| 2 | Needs a name AND a spec number | **C** `and` |
| 3 | `duplicate_spec` is False → `not duplicate_spec` | **A** True |
| 4 | Accept either Auto Racing or Drag Racing | **B** `category == 'Auto Racing' or category == 'Drag Racing'` |

**MCQ 3.05: 4/4 | answers: A,C,A,B**

## Pseudocode Check

I traced the College Board pseudocode by hand for my test record *Titanium Bellhousing* (Drag Racing, spec `4.2`, date filled in): `hasProductName` = true, `validCategory` = true (second comparison), `hasSpecNumber` = true, `hasEffectiveDate` = true, `duplicateSpec` = `(4.2 = 1.1) OR (4.2 = 2.1)` = false, so `NOT duplicateSpec` = true and `isValid` = true → **ACCEPT RECORD**. The Python validator below makes the same decision.

## Homework Hack: SFI Backend Validator



{% capture challenge3 %}
{% raw %}
Homework Hack - SFI Backend Validator
{% endraw %}
{% endcapture %}

{% capture code3 %}
{% raw %}
existing_spec_numbers = ["1.1", "2.1"]
valid_categories = ["Auto Racing", "Drag Racing"]

test_records = [
    {"product_name": "Multiple Disc Clutch Assemblies", "category": "Auto Racing", "spec_number": "1.2", "effective_date": "Feb. 9, 2006"},
    {"product_name": "Replacement Flywheels", "category": "Street Car", "spec_number": "3.1", "effective_date": "Jan. 1, 2026"},
    {"product_name": "Existing Flywheel Record", "category": "Drag Racing", "spec_number": "1.1", "effective_date": "Jan. 1, 2026"},
    # my extra tests
    {"product_name": "Titanium Bellhousing", "category": "Drag Racing", "spec_number": "4.2", "effective_date": "Mar. 3, 2026"},
    {"product_name": "", "category": "Auto Racing", "spec_number": "5.0", "effective_date": "Apr. 1, 2026"},
    {"product_name": "Harmonic Balancer", "category": "Auto Racing", "spec_number": "", "effective_date": "Apr. 1, 2026"},
    {"product_name": "Driveshaft Loop", "category": "Auto Racing", "spec_number": "6.1", "effective_date": ""},
]

def validate_record(record, existing_specs, categories):
    """Return (is_valid, reasons) for one candidate SFI record."""
    has_product_name = record["product_name"].strip() != ""
    valid_category = record["category"] in categories
    has_spec_number = record["spec_number"].strip() != ""
    has_effective_date = record["effective_date"].strip() != ""
    duplicate_spec = record["spec_number"] in existing_specs

    is_valid = (has_product_name and valid_category and has_spec_number
                and has_effective_date and not duplicate_spec)

    reasons = []
    if not has_product_name:
        reasons.append("missing product name")
    if not valid_category:
        reasons.append("category '" + record["category"] + "' not accepted")
    if not has_spec_number:
        reasons.append("missing spec number")
    if not has_effective_date:
        reasons.append("missing effective date")
    if duplicate_spec:
        reasons.append("spec " + record["spec_number"] + " already exists")
    return is_valid, reasons

for record in test_records:
    is_valid, reasons = validate_record(record, existing_spec_numbers, valid_categories)
    name = record["product_name"] or "(no name)"
    if is_valid:
        print("ACCEPT RECORD:", name)
    else:
        print("REJECT RECORD:", name, "->", ", ".join(reasons))
{% endraw %}
{% endcapture %}

{% capture source3 %}
{% raw %}
```python
# CODE_RUNNER: Homework Hack - SFI Backend Validator

existing_spec_numbers = ["1.1", "2.1"]
valid_categories = ["Auto Racing", "Drag Racing"]

test_records = [
    {"product_name": "Multiple Disc Clutch Assemblies", "category": "Auto Racing", "spec_number": "1.2", "effective_date": "Feb. 9, 2006"},
    {"product_name": "Replacement Flywheels", "category": "Street Car", "spec_number": "3.1", "effective_date": "Jan. 1, 2026"},
    {"product_name": "Existing Flywheel Record", "category": "Drag Racing", "spec_number": "1.1", "effective_date": "Jan. 1, 2026"},
    # my extra tests
    {"product_name": "Titanium Bellhousing", "category": "Drag Racing", "spec_number": "4.2", "effective_date": "Mar. 3, 2026"},
    {"product_name": "", "category": "Auto Racing", "spec_number": "5.0", "effective_date": "Apr. 1, 2026"},
    {"product_name": "Harmonic Balancer", "category": "Auto Racing", "spec_number": "", "effective_date": "Apr. 1, 2026"},
    {"product_name": "Driveshaft Loop", "category": "Auto Racing", "spec_number": "6.1", "effective_date": ""},
]

def validate_record(record, existing_specs, categories):
    """Return (is_valid, reasons) for one candidate SFI record."""
    has_product_name = record["product_name"].strip() != ""
    valid_category = record["category"] in categories
    has_spec_number = record["spec_number"].strip() != ""
    has_effective_date = record["effective_date"].strip() != ""
    duplicate_spec = record["spec_number"] in existing_specs

    is_valid = (has_product_name and valid_category and has_spec_number
                and has_effective_date and not duplicate_spec)

    reasons = []
    if not has_product_name:
        reasons.append("missing product name")
    if not valid_category:
        reasons.append("category '" + record["category"] + "' not accepted")
    if not has_spec_number:
        reasons.append("missing spec number")
    if not has_effective_date:
        reasons.append("missing effective date")
    if duplicate_spec:
        reasons.append("spec " + record["spec_number"] + " already exists")
    return is_valid, reasons

for record in test_records:
    is_valid, reasons = validate_record(record, existing_spec_numbers, valid_categories)
    name = record["product_name"] or "(no name)"
    if is_valid:
        print("ACCEPT RECORD:", name)
    else:
        print("REJECT RECORD:", name, "->", ", ".join(reasons))
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="python-boolean-hw-3"
   language="python"
   challenge=challenge3
   code=code3
   source=source3
%}


**Test results:**

| Record | Expected | Actual | Why |
|---|---|---|---|
| Multiple Disc Clutch Assemblies | Accept | ACCEPT | every rule passes, spec 1.2 is new |
| Replacement Flywheels | Reject | REJECT | `Street Car` isn't an accepted category |
| Existing Flywheel Record | Reject | REJECT | spec 1.1 is a duplicate (`not duplicate_spec` is False) |
| Titanium Bellhousing | Accept | ACCEPT | matches my pseudocode trace |
| (no name) | Reject | REJECT | empty product name |
| Harmonic Balancer | Reject | REJECT | empty spec number |
| Driveshaft Loop | Reject | REJECT | empty effective date |

**Boolean logic explained:** a record is valid only when **all** requirements are true, so the five checks are joined with `and`. The duplicate rule is written as `not duplicate_spec` because we want to *reject* duplicates — `not` flips "is a duplicate" into "is new." The category check uses `in valid_categories`, which is the same as `category == "Auto Racing" or category == "Drag Racing"`. Breaking the rule into named Booleans made it easy to print exactly which rule failed.

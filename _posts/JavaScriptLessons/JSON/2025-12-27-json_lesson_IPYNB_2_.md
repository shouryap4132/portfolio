---
layout: post
categories: ['CSSE JavaScript']
comments: True
codemirror: True
title: JSON
description: JavaScript Object Notion (JSON) lesson defines key-value pair objects.
permalink: /javascript/json/lesson
author: John Mortensen
---

## All About JavaScript Object and JSON

## What is a JavaScript Object?

JSON is a notation for a data structure that stores key-value pairs in a single variable. It is a container that holds a collection of items in an unordered list.

### Key Features:
- Elements are stored as a hash table
- Each element can be accessed by its key
- You can change values, add key-values, or remove elements
- Usually stores elements as a mix of different data types
- Key-value pairs can be nested

## Why are JavaScript Objects Important?

JavaScript Objects allow you to:
- Store collections of related data with named properties
- Process complex data structures efficiently
- Organize information in a structured, readable way
- Transfer data between systems (JSON format)

## Person Object

Let's start with a basic person object. Notice how we use keys (like "name", "age") to access values.



{% capture challenge0 %}
{% raw %}
Personalize your student record.
{% endraw %}
{% endcapture %}

{% capture code0 %}
{% raw %}
// Simple person object with key-value pairs
const person = {
    name: "Jane",
    age: 16,
    grade: "11th",
    favoriteSubject: "Computer Science"
};

// Access values using keys
console.log("Name:", person.name);
console.log("Age:", person.age);
console.log("Favorite Subject:", person.favoriteSubject);

// Add a new key-value pair
person.school = "Del Norte High School";
console.log("After adding school:");
console.log(person);
{% endraw %}
{% endcapture %}

{% capture source0 %}
{% raw %}
```javascript
%%js

// CODE_RUNNER: Personalize your student record.

// Simple person object with key-value pairs
const person = {
    name: "Jane",
    age: 16,
    grade: "11th",
    favoriteSubject: "Computer Science"
};

// Access values using keys
console.log("Name:", person.name);
console.log("Age:", person.age);
console.log("Favorite Subject:", person.favoriteSubject);

// Add a new key-value pair
person.school = "Del Norte High School";
console.log("After adding school:");
console.log(person);
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="javascript-json-lesson-0"
   language="javascript"
   challenge=challenge0
   code=code0
   source=source0
%}


##  Database Collections

An information database (infoDB) could have multiple use cases:
- Collections of data transmitted between systems, like APIs
- In the backend this data could be received to move data in and out of persistent storage, like databases



{% capture challenge1 %}
{% raw %}
Define your records for the infoDB. One record for you and another for your table partner. Pretend data is fine. Make sure to include a hobby or collection for each person.
{% endraw %}
{% endcapture %}

{% capture code1 %}
{% raw %}
// infoDB is a JavaScript object with Keys and Values
const infoDb = {}
infoDb.id_0001 = {
    "FirstName": "John",
    "LastName": "Mortensen",
    "DOB": "October 21",
    "Residence": "San Diego",
    "Email": "jmortensen@powayusd.com",
    "OwnsCars": ["2015-Fusion", "2011-Ranger", "2003-Excursion", "1997-F350", "1969-Cadillac"]
};
console.log(infoDb);
{% endraw %}
{% endcapture %}

{% capture source1 %}
{% raw %}
```javascript
%%js

// CODE_RUNNER: Define your records for the infoDB. One record for you and another for your table partner. Pretend data is fine. Make sure to include a hobby or collection for each person.

// infoDB is a JavaScript object with Keys and Values
const infoDb = {}
infoDb.id_0001 = {
    "FirstName": "John",
    "LastName": "Mortensen",
    "DOB": "October 21",
    "Residence": "San Diego",
    "Email": "jmortensen@powayusd.com",
    "OwnsCars": ["2015-Fusion", "2011-Ranger", "2003-Excursion", "1997-F350", "1969-Cadillac"]
};
console.log(infoDb);
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="javascript-json-lesson-1"
   language="javascript"
   challenge=challenge1
   code=code1
   source=source1
%}


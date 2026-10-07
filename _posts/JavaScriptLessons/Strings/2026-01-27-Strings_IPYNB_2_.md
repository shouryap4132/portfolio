---
layout: post
categories: ['CSSE JavaScript']
codemirror: True
microblog: True
title: Strings
description: Strings using Code Runner
permalink: /js/strings
author: Seonyoo Pak, Adam Ong, Roger Wang
---

## Introduction

**What Exactly Are Strings?** Strings are essentially sequences of characters used to represent text in programming. They can include letters, numbers, symbols, and spaces.


**Example Code:**

~~~js
// Add two strings together

let fruit1 = "Apple";
let fruit2 = "Banana";
let combinedFruits = fruit1 + " and " + fruit2;
console.log("Fruits to eat: " + combinedFruits);
~~~

In the example above, there are two variables: fruit1 and fruit2. Notice how apple and banana are in quotation marks? That indicates that they are strings. In JavaScript, strings are enclosed in single quotes (' '), double quotes (" "), or backticks (` `). The "and" in between the two fruits is also a string. When we add the strings together using the + operator, we get a new string that combines them.

Now you try:



{% capture challenge0 %}
{% raw %}
Identify and correct the error in the code.
{% endraw %}
{% endcapture %}

{% capture code0 %}
{% raw %}
 let sport1 = "Soccer";
 let sport2 = "Basketball";

 console.log(The sports I play are:  + sport1 + " and " + sport2);
{% endraw %}
{% endcapture %}

{% capture source0 %}
{% raw %}
```javascript
%%js

// CODE_RUNNER: Identify and correct the error in the code.

 let sport1 = "Soccer";
 let sport2 = "Basketball";

 console.log(The sports I play are:  + sport1 + " and " + sport2);
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="js-strings-0"
   language="javascript"
   challenge=challenge0
   code=code0
   source=source0
%}


## String Length and Indexing

**String Lenth:** You can find out how many characters are in a string using the `.length` property. Spaces also count as a character.

**Example:**

~~~js
let message = "Hello World";
console.log(message.length); // Will output 11 because there are 11 characters
~~~

**String Indexing:** Each character in a string has an index, starting from 0 for the first character. You can access individual characters using bracket notation.

**Example:**

~~~js
let greeting = "Hello World";
console.log(greeting[0]); // Will output "H"
console.log(greeting[6]); // Will output "W"
~~~



{% capture challenge1 %}
{% raw %}
Modify this code so that the password requires at least 8 characters and the first character is equal to 3. Remember, the first character is 0, not 1.
{% endraw %}
{% endcapture %}

{% capture code1 %}
{% raw %}
let password = "abc";
if (password.length < 8 || password[0] !== "3") { // FYI, "||" means OR, and "!==" means NOT EQUAL TO
    console.log("Password must be at least 8 characters and start with '3'");
} else {
    console.log("Password is valid!");
}
{% endraw %}
{% endcapture %}

{% capture source1 %}
{% raw %}
```javascript
%%js

// CODE_RUNNER: Modify this code so that the password requires at least 8 characters and the first character is equal to 3. Remember, the first character is 0, not 1.

let password = "abc";
if (password.length < 8 || password[0] !== "3") { // FYI, "||" means OR, and "!==" means NOT EQUAL TO
    console.log("Password must be at least 8 characters and start with '3'");
} else {
    console.log("Password is valid!");
}
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="js-strings-1"
   language="javascript"
   challenge=challenge1
   code=code1
   source=source1
%}


## String Concatenation

**String Concatenation:** is simply the process of combining two or more strings together. In JavaScript, you can concatenate strings using the `+` operator.

**Example:**

~~~js
let firstName = "John";
let lastName = "Smith";
let fullName = firstName + " " + lastName; // Those quotation marks just add a space between the words
console.log(fullName); // Will output "John Smith"
~~~




{% capture challenge2 %}
{% raw %}
Add your own information to the constants below and use concatenation to print a sentence about yourself.
{% endraw %}
{% endcapture %}

{% capture code2 %}
{% raw %}
const name = "x";
const age = y;
const city = "z";

// Your code here
{% endraw %}
{% endcapture %}

{% capture source2 %}
{% raw %}
```javascript
%%js

// CODE_RUNNER: Add your own information to the constants below and use concatenation to print a sentence about yourself.

const name = "x";
const age = y;
const city = "z";

// Your code here


```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="js-strings-2"
   language="javascript"
   challenge=challenge2
   code=code2
   source=source2
%}


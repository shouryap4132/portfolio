---
layout: post
codemirror: True
title: Array Jokes
description: JavaScript jokes using arrays, running in a Jupyter Notebook and on GitHub Pages.
permalink: /js/jokes
author: John Mortensen
---

### Programmer Jokes

An array of key-value pairs (JavaScript objects). Each joke has a "complexity" rating—if you understand the ones rated "3," your teacher will be impressed!



{% capture challenge0 %}
{% raw %}
Computer Science jokes for the programming students.
{% endraw %}
{% endcapture %}

{% capture code0 %}
{% raw %}
var compsci_joke_list = [
    { joke: "Why do programmers prefer dark mode? Because light attracts bugs.", complexity: "1" },
    { joke: "Why do Java developers wear glasses? Because they don't see sharp.", complexity: "2" },
    { joke: "How many programmers does it take to change a light bulb? None, that's a hardware problem.", complexity: "1" },
    { joke: "Why do Python programmers prefer snake_case? Because they can't C.", complexity: "2" },
    { joke: "Why was the JavaScript developer sad? Because he didn't know how to 'null' his feelings.", complexity: "3" },
    { joke: "Why do programmers always mix up Christmas and Halloween? Because Oct 31 == Dec 25.", complexity: "3" },
    { joke: "Why did the programmer quit his job? Because he didn't get arrays.", complexity: "O(n)" },
    { joke: "Why do Linux programmers prefer using the terminal? Because they don't like Windows.", complexity: "1" },
];
var randomIndex = Math.floor(Math.random() * compsci_joke_list.length);
var selectedJoke = compsci_joke_list[randomIndex];
console.log("Joke #" + (randomIndex + 1) + ": " + selectedJoke.joke + " (Complexity: " + selectedJoke.complexity + ")");
{% endraw %}
{% endcapture %}

{% capture source0 %}
{% raw %}
```javascript
%%js

// CODE_RUNNER: Computer Science jokes for the programming students.

var compsci_joke_list = [
    { joke: "Why do programmers prefer dark mode? Because light attracts bugs.", complexity: "1" },
    { joke: "Why do Java developers wear glasses? Because they don't see sharp.", complexity: "2" },
    { joke: "How many programmers does it take to change a light bulb? None, that's a hardware problem.", complexity: "1" },
    { joke: "Why do Python programmers prefer snake_case? Because they can't C.", complexity: "2" },
    { joke: "Why was the JavaScript developer sad? Because he didn't know how to 'null' his feelings.", complexity: "3" },
    { joke: "Why do programmers always mix up Christmas and Halloween? Because Oct 31 == Dec 25.", complexity: "3" },
    { joke: "Why did the programmer quit his job? Because he didn't get arrays.", complexity: "O(n)" },
    { joke: "Why do Linux programmers prefer using the terminal? Because they don't like Windows.", complexity: "1" },
];
var randomIndex = Math.floor(Math.random() * compsci_joke_list.length);
var selectedJoke = compsci_joke_list[randomIndex];
console.log("Joke #" + (randomIndex + 1) + ": " + selectedJoke.joke + " (Complexity: " + selectedJoke.complexity + ")");
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="js-jokes-0"
   language="javascript"
   challenge=challenge0
   code=code0
   source=source0
%}


### Accountant Jokes

A simpler array of strings—these jokes are just plain text, not JavaScript objects.



{% capture challenge1 %}
{% raw %}
Accounting jokes for the finance students.
{% endraw %}
{% endcapture %}

{% capture code1 %}
{% raw %}
var accounting_joke_list = [
    "Why did the accountant cross the road? To bore the people on the other side.",
    "What do accountants do when they're constipated? They work it out with a pencil.",
    "How does an accountant stay out of debt? He learns to act his wage.",
    "Why did the accountant stare at his glass of orange juice for three hours? Because on the box it said 'concentrate'.",
    "Why did the accountant get promoted? Because he knew how to balance his work and play.",
    "Why did the accountant go broke? Because he lost his balance.",
    "Why did the accountant get a job at the bakery? Because he was good at making dough.",
    "Why did the accountant get a job at the zoo? Because he was good with cheetahs.",
    "Why did the accountant get a job at the library? Because he was good at keeping books.",
    "Why did the accountant get a job at the circus? Because he was good at juggling numbers.",
    "Why did the accountant get a job at the gym? Because he was good at working out the numbers.",
    "Why did the accountant get a job at the farm? Because he was good at counting the chickens before they hatched."
]
var randomIndex = Math.floor(Math.random() * accounting_joke_list.length);
console.log("Joke #" + (randomIndex + 1) + ": " + accounting_joke_list[randomIndex]);
{% endraw %}
{% endcapture %}

{% capture source1 %}
{% raw %}
```javascript
%%js

// CODE_RUNNER: Accounting jokes for the finance students.

var accounting_joke_list = [
    "Why did the accountant cross the road? To bore the people on the other side.",
    "What do accountants do when they're constipated? They work it out with a pencil.",
    "How does an accountant stay out of debt? He learns to act his wage.",
    "Why did the accountant stare at his glass of orange juice for three hours? Because on the box it said 'concentrate'.",
    "Why did the accountant get promoted? Because he knew how to balance his work and play.",
    "Why did the accountant go broke? Because he lost his balance.",
    "Why did the accountant get a job at the bakery? Because he was good at making dough.",
    "Why did the accountant get a job at the zoo? Because he was good with cheetahs.",
    "Why did the accountant get a job at the library? Because he was good at keeping books.",
    "Why did the accountant get a job at the circus? Because he was good at juggling numbers.",
    "Why did the accountant get a job at the gym? Because he was good at working out the numbers.",
    "Why did the accountant get a job at the farm? Because he was good at counting the chickens before they hatched."
]
var randomIndex = Math.floor(Math.random() * accounting_joke_list.length);
console.log("Joke #" + (randomIndex + 1) + ": " + accounting_joke_list[randomIndex]);
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="js-jokes-1"
   language="javascript"
   challenge=challenge1
   code=code1
   source=source1
%}


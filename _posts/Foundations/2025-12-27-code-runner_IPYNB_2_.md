---
layout: post
codemirror: True
title: Code Runner - JavaScript
description: Build a lesson using javascript.  This allows you to create in Jupyter Notebook code cell for development, plus interact elements with the lesson on the Web
permalink: /code/javascript
author: John Mortensen
---

## Code-Runner Automation

The notebook (ipynb) to web (html) conversion system automatically generates a "code-runner" web experience from code cells.

## JavaScript Code Cells

- **%%js**: required for code cell testing
- **JavaScript/Java**: `// CODE_RUNNER: <challenge text>`




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
    age: 16
};
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
    age: 16
};
console.log(person);
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="code-javascript-0"
   language="javascript"
   challenge=challenge0
   code=code0
   source=source0
%}


## Practical Example: Fix the Syntax Error

Here's a lesson example to fix a syntax error.



{% capture challenge1 %}
{% raw %}
Fix the syntax errors. Run the code to get a hint!
{% endraw %}
{% endcapture %}

{% capture code1 %}
{% raw %}
console.log(Office hours 10-10:30))
{% endraw %}
{% endcapture %}

{% capture source1 %}
{% raw %}
```javascript
%%js

// CODE_RUNNER: Fix the syntax errors. Run the code to get a hint!

console.log(Office hours 10-10:30))
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="code-javascript-1"
   language="javascript"
   challenge=challenge1
   code=code1
   source=source1
%}


## Practical Example: JavaScript Loop

A JavaScript example where students complete a loop.



{% capture challenge2 %}
{% raw %}
Complete the for loop to print numbers 1 through 5. Fill in the missing parts of the loop.
{% endraw %}
{% endcapture %}

{% capture code2 %}
{% raw %}
// Complete the for loop
for (let i = ???; i <= ???; i++) {
  console.log(i);
}
{% endraw %}
{% endcapture %}

{% capture source2 %}
{% raw %}
```javascript
%%js

// CODE_RUNNER: Complete the for loop to print numbers 1 through 5. Fill in the missing parts of the loop.

// Complete the for loop
for (let i = ???; i <= ???; i++) {
  console.log(i);
}
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="code-javascript-2"
   language="javascript"
   challenge=challenge2
   code=code2
   source=source2
%}


## Build Process

When you run `make` or the notebook conversion script:

1. The script detects CODE_RUNNER comments in code cells
2. Extracts the challenge text from the comment
3. Generates a unique `runner_id` based on the permalink + index
4. Strips magic commands (`%%js`, `%%python`) and CODE_RUNNER comments from the code
5. **Clears Jupyter outputs** from cells with CODE_RUNNER (since code-runner provides interactive execution)
6. Injects a code-runner block after the code cell in the generated markdown

### Testing Notebooks

- **In Notebook**: Run cells normally, see outputs using **Help-Toggle Developer Tools**
- **On Website**: Viewers can modify, run code, and view outputs localhost and deployed
- **No Duplication**: Code exists is in both places, but only requires development in notebook (IPYNB)

### Migrating Notebooks 

If you have existing IPYNB lessons with code cell that only run in VSCode:

- You will need to enable your repo for Code Runner support
- Add to frontmatter of the page `codemirror: true`
- Add a comment to the top of desired code-runner cell `// CODE_RUNNER: <challenge text>`
- Run make, view, and test on localhost
- Commit the change to production

The system will automatically generate the code-runner blocks in the page that enable interaction on the Web.

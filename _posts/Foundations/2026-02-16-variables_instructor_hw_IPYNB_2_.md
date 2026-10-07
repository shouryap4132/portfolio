---
layout: post
codemirror: True
title: JavaScript Variables and HTML DOM Homework
description: Perform variables and HTML DOM homework using this notebook.
author: John Mortensen
breadcrumb: True
permalink: /game/essentials/variables
---

## JavaScript Variables: Homework Notebook`

Use this Notbook to perform JavaScript Variable Homework Hacks.

---



{% capture challenge0 %}
{% raw %}
Class definition with properties, methods, and default values
{% endraw %}
{% endcapture %}

{% capture code0 %}
{% raw %}
/*
Add-Lives Homework Instructions:
- Add a reaction message for the enemy when it reacts (e.g., "Enemy reacts!").
- Add lives to player
  - Reflect: Did adding lives impact the enemy? Why or why not?
- Add lives to enemy 
  - Reflect: How can values be the same for both player and enemy? Without duplicating assignments?
  - Reflect: How can you have default values for lives, but also allow for custom values?
*/


let gameSpeed = 10; // Global game speed variable

// Example of a class representing a game object
class GameObject {
  constructor(data) {
    // Using 'this' to define properties of the class instance
    this.image = data.image;
    this.width = data.width;
    this.height = data.height;
    this.speedRatio = data.speedRatio;
    // Position coordinates of the object are set to default values if arguments are not provided
    this.x = data.x;
    this.y = data.y;
    // Speed is calculated based on the global game speed and the speed ratio
    this.speed = gameSpeed * this.speedRatio;
    // Store the react callback if provided
    this.react = data.react || function() {
      console.log('No reaction defined');
    };
  }
}

const player_data = {
  image: 'player.png',
  width: 50,
  height: 50,
  speedRatio: 1.5,
  x: 0,
  y: 0,
  react: function() {
    console.log(`${this.image} is reacting at position (${this.x}, ${this.y})!`);
  }
};

const player = new GameObject(player_data);

console.log("Player Object (Class Instance):", player, "Type:", typeof player);
// Object reference
console.log("Player Image:", player.image);

// Activate the react callback
player.react();

const enemy_data = {
  image: 'enemy.png',
  width: 40,
  height: 40,
  speedRatio: 1.0,
  x: 100,
  y: 150
};

const enemy = new GameObject(enemy_data);
console.log("Enemy Object (Class Instance):", enemy, "Type:", typeof enemy);

// Object reference
console.log("Enemy Position:", `(${enemy.x}, ${enemy.y})`);
enemy.x += enemy.speed; // Move enemy based on its speed
console.log("Enemy New Position after moving:", `(${enemy.x}, ${enemy.y})`);
enemy.react(); // Enemy has default reaction
{% endraw %}
{% endcapture %}

{% capture source0 %}
{% raw %}
```javascript
%%js

/*
Add-Lives Homework Instructions:
- Add a reaction message for the enemy when it reacts (e.g., "Enemy reacts!").
- Add lives to player
  - Reflect: Did adding lives impact the enemy? Why or why not?
- Add lives to enemy 
  - Reflect: How can values be the same for both player and enemy? Without duplicating assignments?
  - Reflect: How can you have default values for lives, but also allow for custom values?
*/

// CODE_RUNNER: Class definition with properties, methods, and default values

let gameSpeed = 10; // Global game speed variable

// Example of a class representing a game object
class GameObject {
  constructor(data) {
    // Using 'this' to define properties of the class instance
    this.image = data.image;
    this.width = data.width;
    this.height = data.height;
    this.speedRatio = data.speedRatio;
    // Position coordinates of the object are set to default values if arguments are not provided
    this.x = data.x;
    this.y = data.y;
    // Speed is calculated based on the global game speed and the speed ratio
    this.speed = gameSpeed * this.speedRatio;
    // Store the react callback if provided
    this.react = data.react || function() {
      console.log('No reaction defined');
    };
  }
}

const player_data = {
  image: 'player.png',
  width: 50,
  height: 50,
  speedRatio: 1.5,
  x: 0,
  y: 0,
  react: function() {
    console.log(`${this.image} is reacting at position (${this.x}, ${this.y})!`);
  }
};

const player = new GameObject(player_data);

console.log("Player Object (Class Instance):", player, "Type:", typeof player);
// Object reference
console.log("Player Image:", player.image);

// Activate the react callback
player.react();

const enemy_data = {
  image: 'enemy.png',
  width: 40,
  height: 40,
  speedRatio: 1.0,
  x: 100,
  y: 150
};

const enemy = new GameObject(enemy_data);
console.log("Enemy Object (Class Instance):", enemy, "Type:", typeof enemy);

// Object reference
console.log("Enemy Position:", `(${enemy.x}, ${enemy.y})`);
enemy.x += enemy.speed; // Move enemy based on its speed
console.log("Enemy New Position after moving:", `(${enemy.x}, ${enemy.y})`);
enemy.react(); // Enemy has default reaction
```
{% endraw %}
{% endcapture %}

{% include runners/code.html
   runner_id="game-essentials-variables-0"
   language="javascript"
   challenge=challenge0
   code=code0
   source=source0
%}



<div class="ui-runner">


<!--
Add-Button Homework Instructions:
- Comment the code for Button 2 (Size Change) 
- Comment the code for Button 3 (Clicker Box).
- Add a 4th button, and make it do something new when clicked 
  - change background
  - highlight the text 
- Comment your new button code
-->


<!-- Button Container  -->
<div style="display: flex; flex-wrap: wrap; gap: 10px;">
    <a style="text-decoration: none;">
        <!-- Color Change Button with id -->
        <div id="color-btn" style="background-color: #00FF00; color: white; padding: 10px 20px; border-radius: 5px; font-weight: bold; cursor: pointer;">
            Color Change
        </div>
    </a>
    <a style="text-decoration: none;">
        <!-- Size Change Button with id -->
        <div id="size-btn" style="background-color: #FF0000; color: white; padding: 10px 20px; border-radius: 5px; font-weight: bold; cursor: pointer;">
            Size Change
        </div>
    </a>
    <a style="text-decoration: none;">
        <!-- Clicker Box with id -->
        <div id="clicker-box" style="background-color: #12ABFF; color: white; padding: 10px 20px; border-radius: 5px; font-weight: bold; cursor: pointer;">
            Clicks: <span id="click-count">0</span>
        </div>
    </a>
</div>

<script>
(function() {
// All JS code inside a function to allow multiple runs in Jupyter Notebook without conflicts 
(function() {

  // 1. Color Change
  // Define const variable for the color button by its ID
  const colorBtn = document.getElementById('color-btn'); 
  // Define isWhite variable to track current color state
  let isWhite = true;
  // Define an event listener for the button click event
  colorBtn.addEventListener('click', function() {
      // Toggle the button text color between white and black using setProperty with priority
      if (isWhite) {
          colorBtn.style.setProperty('color', 'black', 'important');
      } else {
          colorBtn.style.setProperty('color', 'white', 'important');
      }
      isWhite = !isWhite; // Toggle to opposite state
  });

  // 2. Size Change
  const sizeBtn = document.getElementById('size-btn');
  let isLarge = false;
  sizeBtn.addEventListener('click', function() {
      if (isLarge) {
          sizeBtn.style.padding = '10px 20px';
          sizeBtn.style.fontSize = '1em';
      } else {
          sizeBtn.style.padding = '20px 40px';
          sizeBtn.style.fontSize = '1.5em';
      }
      isLarge = !isLarge;
  });

  // 3. Clicker Box (Cookie Clicker)
  const clickerBox = document.getElementById('clicker-box');
  const clickCount = document.getElementById('click-count');
  let count = 0;
  clickerBox.addEventListener('click', function() {
      clickCount.textContent = ++count; 
  });

})(); // End Jupyter Notebook required function()
})();
</script>
</div>


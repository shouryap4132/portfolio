---
layout: post
codemirror: True
title: Game Runner - GameEngine Examples
description: Build interactive game lessons using the GameEngine framework in Jupyter Notebooks. This allows you to create game code in IPYNB cells for development, then automatically convert them to interactive game runners on the web.
permalink: /gamerunner
author: John Mortensen
---

## Game-Runner Automation

The notebook (ipynb) to web (html) conversion system automatically generates a "game-runner" web experience from JavaScript code cells that use the GameEngine framework.

This allows you to:
- Develop game code in Jupyter Notebooks with immediate testing
- Automatically convert to interactive web experiences for students
- No duplication - code is written once in the notebook, runs both in VS Code and on the web

## JavaScript Game Cells

To create a game-runner from a notebook cell:

- **%%js**: Required for code cell testing in Jupyter
- **// GAME_RUNNER: <challenge text>**: Marks cell as a game-runner and provides the challenge description
- **GameEngine imports**: Use standard GameEngine ES6 module imports
- **Export requirements**: Must export `GameControl` and `gameLevelClasses`

## Example 1: Basic Custom Level

> A simple game with a custom background and player character.



{% capture challenge0 %}
{% raw %}
Run the game, user WASD keys to move the player around.
{% endraw %}
{% endcapture %}

{% capture code0 %}
{% raw %}
// Import for GameRunner
import GameControl from '/assets/js/GameEnginev1/essentials/GameControl.js';
// Level Code
import GameEnvBackground from '/assets/js/GameEnginev1/essentials/GameEnvBackground.js';
import Player from '/assets/js/GameEnginev1/essentials/Player.js';

class CustomLevel {
  constructor(gameEnv) {
    const path = gameEnv.path;
    const width = gameEnv.innerWidth;
    const height = gameEnv.innerHeight;
    
    const bgData = {
        name: 'custom_bg',
        src: path + "/images/gamebuilder/bg/clouds.jpg",
        pixels: { height: 720, width: 1280 }
    };
    const playerData = {
      id: 'Hero',
      src: path + "/images/gamify/chillguy.png",
      SCALE_FACTOR: 5,
      STEP_FACTOR: 1000,
      ANIMATION_RATE: 50,
      INIT_POSITION: { x: 100, y: 300 },
      pixels: { height: 512, width: 384 },
      orientation: { rows: 4, columns: 3 },
      down: { row: 0, start: 0, columns: 3 },
      downRight: { row: 1, start: 0, columns: 3, rotate: Math.PI/16 },
      downLeft: { row: 2, start: 0, columns: 3, rotate: -Math.PI/16 },
      right: { row: 1, start: 0, columns: 3 },
      left: { row: 2, start: 0, columns: 3 },
      up: { row: 3, start: 0, columns: 3 },
      upRight: { row: 1, start: 0, columns: 3, rotate: -Math.PI/16 },
      upLeft: { row: 2, start: 0, columns: 3, rotate: Math.PI/16 },
      hitbox: { widthPercentage: 0.45, heightPercentage: 0.2 },
      keypress: { up: 87, left: 65, down: 83, right: 68 }
    };

    this.classes = [
      { class: GameEnvBackground, data: bgData },
      { class: Player, data: playerData },
    ];
  }
}
export const gameLevelClasses = [CustomLevel];
export { GameControl };
{% endraw %}
{% endcapture %}

{% include runners/game.html
   runner_id="gamerunner-0"
   challenge=challenge0
   code=code0
%}


## Example 2: Multiple Game Levels

> Combine GameLevls for a multi-level experience.



{% capture challenge1 %}
{% raw %}
Transition between water and fish parallax levels using the ESC key.
{% endraw %}
{% endcapture %}

{% capture code1 %}
{% raw %}
import GameControl from "/assets/js/GameEnginev1/essentials/GameControl.js";
import GameLevelWater from "/assets/js/GameEnginev1/GameLevelWater.js";
import GameLevelParallaxFish from "/assets/js/GameEnginev1/GameLevelParallaxFish.js";
export const gameLevelClasses = [GameLevelWater, GameLevelParallaxFish];
export { GameControl };
{% endraw %}
{% endcapture %}

{% include runners/game.html
   runner_id="gamerunner-1"
   challenge=challenge1
   code=code1
%}


## Example 3: Mini-Game Experience (hide_edit)

> Create comic strip-like mini games where players just play without seeing code. Perfect for game experiences embedded in articles or lessons.



{% capture challenge2 %}
{% raw %}
Play the fish underwater adventure!
{% endraw %}
{% endcapture %}

{% capture code2 %}
{% raw %}
import GameControl from "/assets/js/GameEnginev1/essentials/GameControl.js";
import GameLevelParallaxFish from "/assets/js/GameEnginev1/GameLevelParallaxFish.js";
export const gameLevelClasses = [GameLevelParallaxFish];
export { GameControl };
{% endraw %}
{% endcapture %}

{% include runners/game.html
   runner_id="gamerunner-2"
   challenge=challenge2
   code=code2
   hide_edit="true"
%}


## Hide Edit Mode

Use `hide_edit: true` to create mini-game experiences:

```javascript
// GAME_RUNNER: Your challenge | hide_edit: true
```

**This mode:**
- Hides the code editor completely
- Shows only Play, Stop, Reset controls
- Perfect for comic strip-like game experiences
- Players interact with the game without editing code
- Code still runs from the notebook source

**Use cases:**
- Interactive articles with embedded games
- Comic strip-style gaming experiences
- Demonstrations where code editing isn't needed
- Mini-games between lesson sections

## Testing Workflows

### In Jupyter Notebook (VS Code)

1. Write your game code in a JavaScript cell with `%%js`
2. Add `// GAME_RUNNER: <challenge>` at the top
3. Run the cell to test in the notebook
4. Use **Help → Toggle Developer Tools** to see console output and debug

### On Website (After Conversion)

1. Run `make` to convert notebooks to markdown/HTML
2. Open the page in your browser
3. The game-runner provides:
   - Editable code with syntax highlighting
   - Start/Stop/Reset controls
   - Level selector (for multi-level games)
   - Save/Load to localStorage
   - Live game canvas

### Code Editing on Web

Students/viewers can:
- Modify the game code directly in the browser
- Click **Start** to run their modified code
- Use **Reset** to restore original code
- Save their work to browser localStorage
- Switch between levels in multi-level games

## Code Structure Requirements

Your game code must follow these patterns:

### Required Imports

```javascript
import GameControl from '/assets/js/GameEnginev1/essentials/GameControl.js';
// Import other GameEngine classes as needed
```

### Required Exports

```javascript
export { GameControl };
export const gameLevelClasses = [Level1, Level2, ...];
```

### Level Class Structure

Each level class needs:

```javascript
class MyLevel {
  constructor(gameEnv) {
    const path = gameEnv.path;
    const width = gameEnv.innerWidth;
    const height = gameEnv.innerHeight;
    
    // Define game objects
    this.classes = [
      { class: GameEnvBackground, data: bgData },
      { class: Player, data: playerData },
      // ... more objects
    ];
  }
}
```

## Migrating Existing Lessons

If you have existing game lessons in markdown files:

1. Create a new IPYNB file or add to existing one
2. Add frontmatter with `codemirror: true`
3. Create a JavaScript code cell with `%%js`
4. Add `// GAME_RUNNER: <challenge>` at the top
5. Copy your game code (imports, level classes, exports)
6. Run `make` to convert
7. Test on localhost
8. Commit and deploy

The system automatically generates interactive game-runner blocks!

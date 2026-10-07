---
toc: True
microblog: True
assignment: True
layout: post
codemirror: True
title: OCS Game Engine Clicker Mechanics
description: A code-first walkthrough of canvas click capture, object hit testing, and callback-driven score updates in the OCS Game Engine.
courses: {'csse': {'week': 17}}
permalink: /gamerunner/cookie
---

## Game Time!

This is a code-first activity with less talking and more interacting, building, testing, and improving.

---





{% capture container_panel_cookie_intro_game_left %}
<div class="ui-runner">
<div id="cookie-intro-panel" class="cookie-play-panel">
  <h3>How to Play</h3>
  <ol>
    <li>Click Start to begin the game loop.</li>
    <li>Click the cookie sprite to score points.</li>
    <li>Tune values in code directly like <code>SCALE_FACTOR</code>, <code>speed</code>, and <code>hitbox</code>.</li>
    <li>Run again and compare how gameplay changes.</li>
  </ol>
  <p id="cookie-intro-panel-clicks">Clicks: 0</p>
</div>
<script>
(function() {

})();
</script>
</div>

{% endcapture %}

{% capture container_panel_cookie_intro_game_right %}

{% capture challenge0 %}
{% raw %}
Cookie Clicker Mini Game with large cookie
{% endraw %}
{% endcapture %}

{% capture code0 %}
{% raw %}
import GameControl from '@assets/js/GameEnginev1.1/essentials/GameControl.js';
import Clicker from '@assets/js/GameEnginev1.1/essentials/Clicker.js'

class CookieClicker {
  constructor(gameEnv) {
    const path = gameEnv.path;
    const width = gameEnv.innerWidth;
    const height = gameEnv.innerHeight;

    const sprite_src_clicker = path + "/hacks/cookie-clicker/assets/baseCookie.png";

    // This object literal is the "blueprint" the Game Engine uses to build the cookie Game Object.
    const cookie_clicker = {
       id: 'Cookie Clicker',
       greeting: "Click or collide with me to earn points!",
       src: sprite_src_clicker,
       // SCALE_FACTOR of 1 keeps the sprite large on screen (our big cookie lesson setup).
       SCALE_FACTOR: 1,
       pixels: {height: 512, width: 512},
       INIT_POSITION: { x: 0, y: 0},
       orientation: {rows: 1, columns: 1 },
       down: {row: 0, start: 0, columns: 1, wiggle: 0.10 },
       up: {row: 0, start: 0, columns: 1, wiggle: 0.10 },
       left: {row: 0, start: 0, columns: 1, wiggle: 0.10 },
       right: {row: 0, start: 0, columns: 1, wiggle: 0.10 },
       hitbox: { widthPercentage: 0.15, heightPercentage: 0.15 },
       walkingArea: {
          xMin: 0, //left boundary
          xMax: width, //right boundary 
          yMin: 0, //top boundary 
          yMax: height //bottom boundary
       },
       speed: 3,
       direction: { x: 1, y: 1 },
       interact: function(clicks) {
           // When clicked, write the live click count into the Game Runner status bar.
           document.getElementById('gamerunner-cookie-0-metric').textContent = "Clicks: " + clicks;
           document.getElementById('cookie-intro-panel-clicks').textContent = "Clicks: " + clicks;
       },
    };
    this.classes = [{ class: Clicker, data: cookie_clicker}];
  }
}
export const gameLevelClasses = [CookieClicker];
export { GameControl };
{% endraw %}
{% endcapture %}

{% include runners/game.html
   runner_id="gamerunner-cookie-0"
   challenge=challenge0
   code=code0
   hide_edit="true"
   width="100%"
   height="520px"
%}

{% endcapture %}

{% include container-panel.html
   panel_id="cookie_intro_game"
   layout="row"
   gap="1rem"
   left_width="20%"
   right_width="80%"
   left=container_panel_cookie_intro_game_left
   right=container_panel_cookie_intro_game_right
%}


---





{% capture container_panel_cookie_hack_game_left %}
<div class="ui-runner">
<div id="cookie-hack-panel" class="runner-side-panel">
  <h3>Hack IT Goals</h3>
  <ul>
    <li>This version makes the cookie harder to click.</li>
    <li>Adjust movement speed and wiggle behavior.</li>
    <li>Tune hitbox percentages for difficulty.</li>
  </ul>
  <p id="cookie-hack-panel-clicks">Total Clicks: 0</p>
  <div id="cookie-hack-panel-counter-list"></div>
</div>
<script>
(function() {

})();
</script>
</div>

{% endcapture %}

{% capture container_panel_cookie_hack_game_right %}

{% capture challenge1 %}
{% raw %}
Cookie Clicker challenge mode with smaller target
{% endraw %}
{% endcapture %}

{% capture code1 %}
{% raw %}
import GameControl from '@assets/js/GameEnginev1.1/essentials/GameControl.js';
import Clicker from '@assets/js/GameEnginev1.1/essentials/Clicker.js'

class CookieClicker {
  constructor(gameEnv) {
    const path = gameEnv.path;
    const width = gameEnv.innerWidth;
    const height = gameEnv.innerHeight;

    const cookie_src = path + "/hacks/cookie-clicker/assets/baseCookie.png";
    const grandma_src = path + "/hacks/cookie-clicker/assets/grandma.png";

    // Shared score map for all spawned clickers in this runner instance.
    window.cookieHackCounters = window.cookieHackCounters || {};
    // Function to render the counters
    const renderCounters = () => {
      const entries = Object.entries(window.cookieHackCounters);
      const total = entries.reduce((sum, pair) => sum + pair[1], 0);
      // Update total clicks
      const totalEl = document.getElementById('cookie-hack-panel-clicks');
      if (totalEl) totalEl.textContent = "Total Clicks: " + total;
      // Also keep the game-runner metric aligned with the same total.
      const runnerMetric = document.getElementById('gamerunner-cookie-1-metric');
      if (runnerMetric) runnerMetric.textContent = "Total Clicks: " + total;
      // Breakdown clicks by spawned objects
      const listEl = document.getElementById('cookie-hack-panel-counter-list');
      if (!listEl) return;
      if (entries.length === 0) {
        listEl.innerHTML = "<em>No clicks yet.</em>";
        return;
      }

      const rows = entries
        .sort((a, b) => a[0].localeCompare(b[0]))
        .map(function(pair) {
          const id = pair[0];
          const count = pair[1];
          return '<li><code>' + id + '</code>: ' + count + '</li>';
        })
        .join('');

      listEl.innerHTML = '<strong>Per Object:</strong><ul>' + rows + '</ul>';
    };

    // Same object-literal pattern as Runner 1, now tuned for more challenging play.
    const cookie_clicker = {
       id: 'Cookie Clicker',
       greeting: "Click or collide with me to earn points!",
       src: cookie_src,
       SCALE_FACTOR: 8, // Higher value means smaller cookie, division of original size
       pixels: {height: 512, width: 512},
       INIT_POSITION: { x: 0, y: 0},
       orientation: {rows: 1, columns: 1 },
       down: {row: 0, start: 0, columns: 1, wiggle: 0.10 },
       up: {row: 0, start: 0, columns: 1, wiggle: 0.10 },
       left: {row: 0, start: 0, columns: 1, wiggle: 0.10 },
       right: {row: 0, start: 0, columns: 1, wiggle: 0.10 },
       hitbox: { widthPercentage: 0.15, heightPercentage: 0.15 },
       // Walking area uses full container, so motion bounces off all four walls.
       walkingArea: {
          xMin: 0,
          xMax: width,
          yMin: 0,
          yMax: height
       },
       speed: 3,
       direction: { x: 1, y: 1 },
       interact: function(clicks, objectId) {
          // on callback, get objectId
          const id = objectId || (this && this.spriteData && this.spriteData.id) || 'unknown';
          window.cookieHackCounters[id] = clicks; // update map with object count
          renderCounters();
       },
    };
    // Associate Template with Clicker Class, define to spawn multiple instances
    this.classes = [
      { class: Clicker, data: cookie_clicker,
        spawn: {
          count: 3, // object count
          ranges: { // random value from range
            INIT_POSITION: {
              x: [0, Math.max(0, width - 128)],
              y: [0, Math.max(0, height - 128)]
            },
            speed: [1, 5]
          },
          pickOne: { // random pick
            src: [
              cookie_src,
              grandma_src
            ]
          }
        }
      }
    ];

    renderCounters();
  }
}
export const gameLevelClasses = [CookieClicker];
export { GameControl };
{% endraw %}
{% endcapture %}

{% include runners/game.html
   runner_id="gamerunner-cookie-1"
   challenge=challenge1
   code=code1
   hide_edit="true"
   width="100%"
   height="520px"
%}

{% endcapture %}

{% include container-panel.html
   panel_id="cookie_hack_game"
   layout="row"
   gap="1rem"
   left_width="20%"
   right_width="80%"
   left=container_panel_cookie_hack_game_left
   right=container_panel_cookie_hack_game_right
%}


---

## How the Game Engine Rumbles!





{% capture container_panel_cookie_engine_docs_pair_left %}
<div class="ui-runner">
<div id="cookie-engine-flow-panel" class="runner-side-panel">
<h3>Interaction Flow Diagram</h3>
<div class="mermaid">
flowchart TD
  A[Canvas click] --> B[GameControl.js captures click]
  B --> C[GameObject.js hit check]
  C --> D[Clicker.js increments count]
  D --> E[GAME_RUNNER interact: callback updates Status Bar]
</div>
</div>
<script>
(function() {

})();
</script>
</div>

{% endcapture %}

{% capture container_panel_cookie_engine_docs_pair_right %}
<div class="ui-runner">
<div id="cookie-engine-snippets-panel" class="runner-side-panel">
  <h3>Related Code Snippets:</h3>
  <p><strong>GameControl.js</strong> (canvas click wiring)</p>
  <pre><code>this.gameContainer.addEventListener('click', this._boundClick);
const obj = this.gameEnv.gameObjects.find(o =&gt; o.canvas &amp;&amp; o.canvas.id === clickedCanvas.id);
if (obj &amp;&amp; typeof obj.handleClick === 'function') {
    obj.handleClick(event);
}</code></pre>
  <p><strong>GameObject.js</strong> (hitbox test + click hook)</p>
  <pre><code>isPointInside(x, y) {
    const px = this.position?.x ?? this.INIT_POSITION?.x ?? 0;
    const py = this.position?.y ?? this.INIT_POSITION?.y ?? 0;
    return (x &gt;= px &amp;&amp; x &lt;= px + width &amp;&amp; y &gt;= py &amp;&amp; y &lt;= py + height);
}
handleClick() {
    // Default: do nothing. Subclasses can override for interactivity.
}</code></pre>
  <p><strong>Clicker.js</strong> (counter + callback)</p>
  <pre><code>handleClick(event) {
    if (this.interact) {
        this.clcks++;
        this.interact(this.clcks);
    }
}</code></pre>
<p><small>Source path: @assets/js/GameEnginev1.1/essentials</small></p>
</div>

<script>
(function() {

})();
</script>
</div>

{% endcapture %}

{% include container-panel.html
   panel_id="cookie_engine_docs_pair"
   layout="row"
   gap="1rem"
   left_width="45%"
   right_width="55%"
   left=container_panel_cookie_engine_docs_pair_left
   right=container_panel_cookie_engine_docs_pair_right
%}


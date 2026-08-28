---
layout: post
title: About
permalink: /about/
comments: true
---

<style>
  .inline-flag {
    height: 80px;
    margin: 0 8px;
    vertical-align: middle;
    display: inline-block;
  }

  .about-photo {
    display: block;
    width: min(100%, 720px);
    height: auto;
    margin: 1rem auto;
    border-radius: 8px;
  }

  .about-photo-caption {
    margin: -0.5rem auto 1.5rem;
    color: #666;
    text-align: center;
    font-style: italic;
  }

  .grid-container {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
    gap: 10px;
  }

  .grid-item {
    text-align: center;
  }

  .grid-item img {
    width: 100%;
    height: 100px;
    object-fit: contain;
  }

  .grid-item p {
    margin: 5px 0;
  }
</style>

### My Journey

I've been fortunate to travel the world with my parents, experiencing different cultures and beautiful places. My favorite location has to be the <img src="https://upload.wikimedia.org/wikipedia/commons/0/08/Flag_of_Maldives.svg" alt="Flag of Maldives" class="inline-flag"> **Maldives** because of the warm, crystal-clear waters. I swear there's something magical about that place!

Here are some places I have lived.

<div id="grid_container" class="grid-container"></div>


## About Me

My name is **Shourya Patel**. I was born in <img src="https://upload.wikimedia.org/wikipedia/commons/a/a1/Flag_of_Iowa.svg" alt="Flag of Iowa" class="inline-flag"> **Iowa**, but now I live in San Diego, <img src="https://upload.wikimedia.org/wikipedia/commons/0/01/Flag_of_California.svg" alt="Flag of California" class="inline-flag"> **California**. I'm a student with a passion for computer science and exploring the world.

<img src="{{ site.baseurl }}/navigation/WIN_20260618_18_59_02_Pro.jpg" alt="Portrait of Shourya Patel" class="about-photo">
<p class="about-photo-caption">A little about me.</p>



<script>
  const container = document.getElementById("grid_container");
  const wikipediaFlags = "https://upload.wikimedia.org/wikipedia/commons/";
  const livingInTheWorld = [
    { flag: "0/01/Flag_of_California.svg", greeting: "Hey", description: "California - forever" },
    { flag: "b/b9/Flag_of_Oregon.svg", greeting: "Hi", description: "Oregon - 9 years" },
    { flag: "b/be/Flag_of_England.svg", greeting: "Alright mate", description: "England - 2 years" },
    { flag: "e/ef/Flag_of_Hawaii.svg", greeting: "Aloha", description: "Hawaii - 2 years" }
  ];

  for (const location of livingInTheWorld) {
    const gridItem = document.createElement("div");
    gridItem.className = "grid-item";

    const img = document.createElement("img");
    img.src = wikipediaFlags + location.flag;
    img.alt = location.description + " flag";

    const description = document.createElement("p");
    description.textContent = location.description;

    const greeting = document.createElement("p");
    greeting.textContent = location.greeting;

    gridItem.appendChild(img);
    gridItem.appendChild(description);
    gridItem.appendChild(greeting);
    container.appendChild(gridItem);
  }
</script>


### Education

- 🏫 Elementary School: Monterey Ridge
- 🏫 Middle School: Oak Valley
- 🏫 High School: Del Norte

### Family

I come from a close-knit family: it's just me, my mom, and my dad. I don't have any siblings, so it's the three of us, and I'm grateful for the adventures we've shared together.

<p class="about-photo-caption">My family and the people who make every adventure meaningful.</p>

### Languages

I'm fluent in two languages:
- 🗣️ **English**
- 🗣️ **Gujarati**

### My Interests

I'm passionate about computer science and love exploring new technologies. My travels around the world have given me a global perspective, and I'm excited about applying my skills to solve real-world problems.



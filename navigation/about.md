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

I've been fortunate to travel the world with my parents, experiencing different cultures and beautiful places. My favorite location has to be the  **Maldives** because of the warm, crystal-clear waters. I swear there's something magical about that place!

Here are some places I have lived.

<div id="grid_container" class="grid-container"></div>


## About Me

My name is **Shourya Patel**. I was born in  **Iowa**, but now I live in San Diego, <img src="https://upload.wikimedia.org/wikipedia/commons/0/01/Flag_of_California.svg" alt="Flag of California" class="inline-flag"> **California**. I'm a student with a passion for computer science and exploring the world.

<img src="{{ site.baseurl }}/navigation/WIN_20260618_18_59_02_Pro.jpg" alt="Portrait of Shourya Patel" class="about-photo">
<p class="about-photo-caption">A little about me.</p>



<script>
  const container = document.getElementById("grid_container");
  const localFlags = "{{ site.baseurl }}/navigation/flags/";
  const livingInTheWorld = [
    { flag: "Flag_of_Iowa.svg.webp", greeting: "Home", description: "Iowa" },
    { flag: "Flag_of_India.svg.webp", greeting: "Namaste", description: "India" },
    { flag: "Flag_of_Hawaii.svg.webp", greeting: "Aloha", description: "Hawaii" },
    { flag: "https://upload.wikimedia.org/wikipedia/commons/0/01/Flag_of_California.svg", greeting: "Welcome", description: "California" },
    { flag: "Flag_of_Maldives.svg.webp", greeting: "Welcome", description: "Maldives" }
  ];

  for (const location of livingInTheWorld) {
    const gridItem = document.createElement("div");
    gridItem.className = "grid-item";

    const img = document.createElement("img");
    img.src = location.flag.startsWith("http") ? location.flag : localFlags + location.flag;
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

### An Introduction to the Maldives

The Maldives is an island nation in the Indian Ocean known for its bright blue lagoons, coral reefs, and beautiful beaches. It is my favorite place because its warm, crystal-clear waters make every visit feel peaceful and unforgettable.



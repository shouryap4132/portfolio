---
layout: post
title: About
permalink: /about/
comments: true
---

## As a conversation Starter

Hi, I'm **Shourya Patel**. I was born in **Iowa** and now live in **San Diego, California**. I love learning, exploring new places, and building things with technology.

Here are some places I have lived.

<comment>
Flags are made using Wikipedia images
</comment>

<style>
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
        display: block;
        margin: 0 auto;
        border: 1px solid #ddd;
        border-radius: 6px;
        background: #fff;
    }
    .grid-item p {
        margin: 5px 0;
    }

    .image-gallery {
        display: flex;
        flex-wrap: nowrap;
        overflow-x: auto;
        gap: 10px;
        min-height: 140px;
        padding: 8px 0;
    }

    .image-gallery img {
        max-height: 150px;
        object-fit: cover;
        border-radius: 5px;
    }
</style>

<div class="grid-container" id="grid_container"></div>

<script>
    var container = document.getElementById("grid_container");
    var http_source = "https://upload.wikimedia.org/wikipedia/commons/";
    var living_in_the_world = [
        {"flag": "d/d4/Flag_of_India.svg", "greeting": "Namaste", "description": "India"},
        {"flag": "e/ef/Flag_of_Hawaii.svg", "greeting": "Aloha", "description": "Hawaii"},
        {"flag": "7/74/Flag_of_the_Maldives.svg", "greeting": "Welcome", "description": "Maldives"},
        {"flag": "0/01/Flag_of_California.svg", "greeting": "Hey", "description": "California"},
        {"flag": "f/f7/Flag_of_Iowa.svg", "greeting": "Home", "description": "Iowa"}
    ];

    for (const location of living_in_the_world) {
        var gridItem = document.createElement("div");
        gridItem.className = "grid-item";

        var img = document.createElement("img");
        img.src = http_source + location.flag;
        img.alt = location.flag + " Flag";

        var description = document.createElement("p");
        description.textContent = location.description;

        var greeting = document.createElement("p");
        greeting.textContent = location.greeting;

        gridItem.appendChild(img);
        gridItem.appendChild(description);
        gridItem.appendChild(greeting);

        container.appendChild(gridItem);
    }
</script>

### Journey through Life

Here is what I did at those places.

- 🏫 Elementary School: Monterey Ridge
- 🏫 Middle School: Oak Valley
- 🏫 High School: Del Norte
- 🌍 Growing up with a love for travel, different cultures, and new experiences
- 💻 Building a passion for computer science and technology
- 🧭 Exploring life in California and beyond while continuing to learn and grow

### Culture, Family, and Fun

Everything for me revolves around family, culture, and the people who shaped my journey.

- My family is close-knit, and I am grateful for the memories we have shared together.
- I was born in Iowa and now live in California, and that mix of places has shaped who I am.
- My love for travel and technology comes from the many experiences I have had across different places.
- The gallery of pics will be added soon as I upload more family and life memories.

<comment>
Gallery of Pics, coming soon...
</comment>
<div class="image-gallery">
  <!-- Family photos will be uploaded soon -->
</div>

### A Little More About Me

I enjoy learning, exploring, and connecting with people from different backgrounds. My goal is to keep growing, keep traveling, and keep applying my interests in computer science and the world around me.



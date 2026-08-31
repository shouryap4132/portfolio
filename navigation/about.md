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
    var localFlags = "{{ site.baseurl }}/navigation/flags/";
    var living_in_the_world = [
        {"flag": "Flag_of_India.svg.webp", "greeting": "Namaste", "description": "India"},
        {"flag": "Flag_of_Hawaii.svg.webp", "greeting": "Aloha", "description": "Hawaii"},
        {"flag": "Flag_of_Maldives.svg.webp", "greeting": "Welcome", "description": "Maldives"},
        {"flag": "https://upload.wikimedia.org/wikipedia/commons/0/01/Flag_of_California.svg", "greeting": "Hey", "description": "California"},
        {"flag": "Flag_of_Iowa.svg.webp", "greeting": "Home", "description": "Iowa"}
    ];

    for (const location of living_in_the_world) {
        var gridItem = document.createElement("div");
        gridItem.className = "grid-item";

        var img = document.createElement("img");
        img.src = location.flag.startsWith("http") ? location.flag : localFlags + location.flag;
        img.alt = location.description + " flag";

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

- 🏫 Elementary School: Monterey Ridge (MRES)
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
- Here are some family memories from our time together.

<comment>
Gallery of family pics
</comment>
<div class="image-gallery">
  <img src="{{ site.baseurl }}/navigation/familypics/IMG_3091.jpg" alt="Family photo 1">
  <img src="{{ site.baseurl }}/navigation/familypics/IMG_1565.jpg" alt="Family photo 2">
  <img src="{{ site.baseurl }}/navigation/familypics/IMG_7990.jpg" alt="Family photo 3">
  <img src="{{ site.baseurl }}/navigation/familypics/IMG_1746.jpg" alt="Family photo 4">
  <img src="{{ site.baseurl }}/navigation/familypics/IMG_0890.jpg" alt="Family photo 5">
</div>

### A Little More About Me

I enjoy learning, exploring, and connecting with people from different backgrounds. My goal is to keep growing, keep traveling, and keep applying my interests in computer science and the world around me.



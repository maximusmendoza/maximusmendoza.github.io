# Home Page (index.md)
---
layout: home
title: Welcome
---

# Hello, I'm Max Mendoza
[Brief introduction about yourself and what you do]

## Latest Blog Posts
My recent thoughts and experiences:
{% for post in site.posts limit:3 %}
  - [{{ post.title }}]({{ post.url | relative_url }})
    {{ post.excerpt | truncate: 160 }}
{% endfor %}

## Featured Projects
Check out some of my work:
{% for project in site.projects limit:2 %}
  - [{{ project.title }}]({{ project.url | relative_url }})
    {{ project.excerpt | truncate: 160 }}
{% endfor %}

[View All Projects](/projects) | [Read My Blog](/blog) | [See My Resume](/resume)

---

# Blog Page (blog.md)
---
layout: page
title: Blog
permalink: /blog/
---

# My Blog Posts

Welcome to my blog! Here you'll find my thoughts on [your topics of interest].

{% for post in site.posts %}
  <article class="post-preview">
    <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
    <p class="post-meta">{{ post.date | date: "%B %d, %Y" }}</p>
    {{ post.excerpt }}
    <a href="{{ post.url | relative_url }}" class="read-more">Read More...</a>
  </article>
{% endfor %}

---

# Projects Page (projects.md)
---
layout: page
title: Projects
permalink: /projects/
---

# My Projects
Here are some of the projects I've worked on:

{% for project in site.projects %}
  <div class="project-card">
    <h2>{{ project.title }}</h2>
    <img src="{{ project.image | relative_url }}" alt="{{ project.title }}">
    <p>{{ project.description }}</p>
    <div class="project-links">
      {% if project.demo_link %}
        <a href="{{ project.demo_link }}" class="button">View Demo</a>
      {% endif %}
      {% if project.github_link %}
        <a href="{{ project.github_link }}" class="button">View Code</a>
      {% endif %}
    </div>
  </div>
{% endfor %}

---

# Resume Page (resume.md)
---
layout: page
title: Resume
permalink: /resume/
---

# My Resume

<div class="resume-container">
    <embed src="/assets/resume.pdf" type="application/pdf" width="100%" height="800px" />
</div>

[Download Resume (PDF)](/assets/resume.pdf)

---

# Sample Blog Post (_posts/2024-01-26-welcome-post.md)
---
layout: post
title: "Welcome to My Blog"
date: 2024-01-26
categories: general
---

This is my first blog post! Here I'll share my thoughts on [your topics].

[Your content here]

---

# Updated _config.yml
title: Max Mendoza
author:
  name: Max Mendoza
  email: your.email@example.com
description: >
  Personal website and blog of Max Mendoza, featuring projects,
  blog posts, and professional experience.

baseurl: ""
url: "https://maximusmendoza.github.io"

# Build settings
theme: minima
plugins:
  - jekyll-feed
  - jekyll-seo-tag

# Navigation
header_pages:
  - blog.md
  - projects.md
  - resume.md

# Collections
collections:
  projects:
    output: true

# Defaults
defaults:
  - scope:
      path: ""
      type: "posts"
    values:
      layout: "post"
  - scope:
      path: ""
      type: "projects"
    values:
      layout: "project"

# Custom CSS
sass:
  style: compressed

---

# Custom CSS (assets/css/style.scss)
---
---

@import "minima";

// Custom styles for the resume page
.resume-container {
    background: white;
    padding: 20px;
    border-radius: 5px;
    box-shadow: 0 2px 5px rgba(0,0,0,0.1);
}

// Project card styling
.project-card {
    border: 1px solid #eee;
    padding: 20px;
    margin-bottom: 20px;
    border-radius: 5px;
    
    img {
        max-width: 100%;
        height: auto;
        margin: 10px 0;
    }
    
    .project-links {
        margin-top: 15px;
        
        .button {
            display: inline-block;
            padding: 8px 16px;
            background: #0366d6;
            color: white;
            text-decoration: none;
            border-radius: 3px;
            margin-right: 10px;
            
            &:hover {
                background: #0255b3;
            }
        }
    }
}

// Blog post preview styling
.post-preview {
    margin-bottom: 30px;
    padding-bottom: 20px;
    border-bottom: 1px solid #eee;
    
    .post-meta {
        color: #666;
        font-size: 0.9em;
    }
    
    .read-more {
        color: #0366d6;
        text-decoration: none;
        
        &:hover {
            text-decoration: underline;
        }
    }
}
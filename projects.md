---
layout: page
title: Projects
permalink: /projects/
---

I'm a busy college student, I promise to get to putting my projects up eventually:

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
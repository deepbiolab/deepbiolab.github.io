---
layout: page
title: Laboratory
permalink: /projects/
description: >
  Explorations and learning experiences in AI and bioengineering.
nav: true
nav_order: 3
display_categories: [Models, Prototypes, Experiments, Tools]
display_description: [Implementing and testing various AI and biological models for research and development, 
                      Exploring open-source or innovative projects, 
                      Conducting experiments to test hypotheses or new methodologies in AI and biological processes, 
                      Developing and refining utility tools for productivity enhancement]
background_image: projects_background_image.jpg
horizontal: false
---

<!-- Add jump links -->
<div class="jump-links-container">
  <div class="jump-links">
    <a href="#Models">Models</a>
    <a href="#Prototypes">Prototypes</a>
    <a href="#Experiments">Experiments</a>
    <a href="#Tools">Tools</a>
  </div>
</div>

<!-- pages/projects.md -->
<div class="projects">
{% if site.enable_project_categories and page.display_categories %}
  <!-- Display categorized projects -->
  {% for category in page.display_categories %}
  <a id="{{ category }}" href=".#{{ category }}">
    <h2 class="category">{{ category }}</h2>
  </a>

  <!-- Display corresponding description for the category -->
  <p class="category-description">{{ page.display_description[forloop.index0] }}</p>

  {% assign categorized_projects = site.projects | where: "category", category %}
  {% assign sorted_projects = categorized_projects | sort: "importance" %}
  <!-- Generate cards for each project -->
  {% if page.horizontal %}
  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_projects %}
      {% include projects_horizontal.liquid %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
  {% endif %}
  {% endfor %}

{% else %}

<!-- Display projects without categories -->

{% assign sorted_projects = site.projects | sort: "importance" %}

  <!-- Generate cards for each project -->

{% if page.horizontal %}

  <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
    {% for project in sorted_projects %}
      {% include projects_horizontal.liquid %}
    {% endfor %}
    </div>
  </div>
  {% else %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_projects %}
      {% include projects.liquid %}
    {% endfor %}
  </div>
  {% endif %}
{% endif %}
</div>

{% if site.newsletter.enabled and site.footer_fixed %}
  {% include scripts/newsletter.liquid center=true %}
{% endif %}

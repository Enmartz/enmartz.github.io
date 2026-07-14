---
layout: page
title: projects
permalink: /projects/
description: Research code, computational imaging methods, and selected technical work.
nav: true
nav_order: 3
display_categories: [research, earlier-work]
horizontal: false
---

<div class="projects">
{% for category in page.display_categories %}
  <a id="{{ category }}" href=".#{{ category }}">
    <h2 class="category">{{ category | replace: "-", " " }}</h2>
  </a>
  {% assign categorized_projects = site.projects | where: "category", category %}
  {% assign sorted_projects = categorized_projects | sort: "importance" %}
  <div class="row row-cols-1 row-cols-md-2">
  {% for project in sorted_projects %}
    {% include projects.liquid %}
  {% endfor %}
  </div>
{% endfor %}
</div>

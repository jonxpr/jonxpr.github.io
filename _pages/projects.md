---
layout: page
title: projects
permalink: /projects/
description: A growing collection of your cool projects.
nav: true
nav_order: 3
horizontal: false
paginate: true # Add this line to enable pagination
---

<!-- pages/projects.md -->
<div class="projects">
  {% if paginate %}
    {% assign projects = paginator.posts %}
  {% else %}
    {% assign projects = site.projects %}
  {% endif %}

  {%- if site.enable_project_categories and page.display_categories %}
    <!-- Display categorized projects -->
    {%- for category in page.display_categories %}
    <h2 class="category">{{ category }}</h2>
    {%- assign categorized_projects = projects | where: "category", category -%}
    {%- assign sorted_projects = categorized_projects | sort: "importance" %}
    <!-- Generate cards for each project -->
    {% if page.horizontal -%}
    <div class="container">
      <div class="row row-cols-2">
      {%- for project in sorted_projects -%}
        {% include projects_horizontal.html %}
      {%- endfor %}
      </div>
    </div>
    {%- else -%}
    <div class="grid">
      {%- for project in sorted_projects -%}
        {% include projects.html %}
      {%- endfor %}
    </div>
    {%- endif -%}
    {% endfor %}

  {%- else -%}
  <!-- Display projects without categories -->
    {%- assign sorted_projects = projects | sort: "importance" -%}
    <!-- Generate cards for each project -->
    {% if page.horizontal -%}
    <div class="container">
      <div class="row row-cols-2">
      {%- for project in sorted_projects -%}
        {% include projects_horizontal.html %}
      {%- endfor %}
      </div>
    </div>
    {%- else -%}
    <div class="grid">
      {%- for project in sorted_projects -%}
        {% include projects.html %}
      {%- endfor %}
    </div>
    {%- endif -%}
  {%- endif -%}

  {% if paginate %}
    <div class="pagination">
      {% if paginator.previous_page %}
        <a href="{{ paginator.previous_page_path }}" class="previous">&laquo; Previous</a>
      {% endif %}
      {% if paginator.next_page %}
        <a href="{{ paginator.next_page_path }}" class="next">Next &raquo;</a>
      {% endif %}
    </div>
  {% endif %}
</div>
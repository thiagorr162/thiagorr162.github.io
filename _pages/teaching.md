---
layout: page
title: teaching
permalink: /teaching/
description:
nav: true
nav_order: 2
horizontal: false
year_range: "2020-2022"
display_categories: true
---
{% assign start_year = page.year_range | split: "-" | first | plus: 0 %}
{% assign end_year = page.year_range | split: "-" | last | plus: 0 %}
{% assign all_categories = (start_year..end_year) | reverse %}



<!-- pages/teaching.md -->
<div class="teaching">
{%- if site.enable_teaching_categories and page.display_categories %}
  <!-- Display categorized teaching -->
  {%- for category in all_categories %}
  <h2 class="category">{{ category }}</h2>
  {%- assign categorized_teaching = site.teaching | where: "category", category -%}
  {%- assign sorted_teaching = categorized_teaching | sort: "importance" %}
  <!-- Generate cards for each teaching -->
  {% if page.horizontal -%}
  <div class="container">
    <div class="row row-cols-2">
    {%- for teaching in sorted_teaching -%}
      {% include teaching_horizontal.html %}
    {%- endfor %}
    </div>
  </div>
  {%- else -%}
  <div class="grid">
    {%- for teaching in sorted_teaching -%}
      {% include teaching.html %}
    {%- endfor %}
  </div>
  {%- endif -%}
  {% endfor %}

{%- else -%}
<!-- Display teaching without categories -->
  {%- assign sorted_teaching = site.teaching | sort: "importance" -%}
  <!-- Generate cards for each teaching -->
  {% if page.horizontal -%}
  <div class="container">
    <div class="row row-cols-2">
    {%- for teaching in sorted_teaching -%}
      {% include teaching_horizontal.html %}
    {%- endfor %}
    </div>
  </div>
  {%- else -%}
  <div class="grid">
    {%- for teaching in sorted_teaching -%}
      {% include teaching.html %}
    {%- endfor %}
  </div>
  {%- endif -%}
{%- endif -%}
</div>

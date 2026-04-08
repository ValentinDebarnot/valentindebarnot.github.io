---
layout: page
permalink: pages/Publications
title: Publications
description: 
nav_order: 2
years: [2026, 2025, 2024, 2023, 2022, 2021, 2020, 2019, 2018, 2017]
nav: true
---

{%- for y in page.years %}
  <!-- <h2 class="year">{{y}}</h2> -->
  {% bibliography -f Mybiblio -q @*[year={{y}}]* %}
{% endfor %}


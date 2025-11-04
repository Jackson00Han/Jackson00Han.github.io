---
permalink: /
title: "Current focus"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

<!-- Current focus -->
- <i class="fas fa-wave-square"></i> **Time-series forecasting**
- <i class="fas fa-balance-scale"></i> **Causal inference for decisions**
- <i class="fas fa-stream"></i> **Recommenders**
- <i class="fas fa-cubes"></i> **AI Applications**


## Featured projects
{% assign featured = site.portfolio | where_exp: "item", "item.featured == true" | sort: "date" | reverse %}

{% if featured and featured.size > 0 %}
  <div class="archive">
    {% for post in featured limit: 1 %}
      {% include archive-single.html type="grid" %}
    {% endfor %}
  </div>
  <p><a class="btn" href="{{ '/portfolio/' | relative_url }}">See all projects →</a></p>
{% else %}
  <p class="notice--info">Add <code>featured: true</code> to items in <code>_portfolio/</code> to show them here.</p>
{% endif %}

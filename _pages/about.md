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
{% assign featured = site.portfolio | where_exp: "p", "p.featured == true" | sort: "date" | reverse %}
{% if featured and featured.size > 0 %}
<ul>
{% for p in featured limit:3 %}
  <li>
    <a href="{{ p.url | relative_url }}"><strong>{{ p.title }}</strong></a>
    <span class="page__meta">— {{ p.date | date: "%Y-%m-%d" }}</span><br>
    {{ p.excerpt | markdownify }}
  </li>
{% endfor %}
</ul>
<p><a class="btn" href="/portfolio/">See all projects →</a></p>
{% else %}
<p class="notice--info">Add <code>featured: true</code> to items in <code>_portfolio/</code> to show them here.</p>
{% endif %}
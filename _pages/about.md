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
{% include archive.html
   collection=site.portfolio
   sort_by="date" sort_order="reverse"
   limit=6
   type="grid"
   entries_layout="grid"
   show_excerpts=true          # 卡片里显示简短描述
%}

<p style="margin-top: .5rem;">
  <a class="btn" href="{{ '/portfolio/' | relative_url }}">See all projects →</a>
</p>

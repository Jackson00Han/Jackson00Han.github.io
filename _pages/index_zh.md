---
permalink: /zh/
title: "当前关注"
author_profile: true
lang: zh
ref: home
---


<!-- 当前关注 -->
- <i class="fas fa-wave-square"></i> **时间序列预测**
- <i class="fas fa-balance-scale"></i> **面向决策的因果推断**
- <i class="fas fa-stream"></i> **推荐系统**
- <i class="fas fa-cubes"></i> **AI 应用**


## 精选项目
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
<p><a class="btn" href="/portfolio/">查看全部项目 →</a></p>
{% else %}
<p class="notice--info">
  在 <code>_portfolio/</code> 中给条目添加 <code>featured: true</code>，即可在这里显示。
</p>
{% endif %}
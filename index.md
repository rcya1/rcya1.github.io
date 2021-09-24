---
layout: splash
permalink: /
header:
  overlay_color: "#5e616c"
  overlay_image: "/assets/img/banner.jpeg"
  actions:
    - label: "<i class='fab fa-github' title='GitHub'></i>"
      url: "https://www.github.com/Ryan10145"
    - label: "<i class='fab fa-linkedin-in' title='Linkedin'></i>"
      url: "https://www.linkedin.com/in/ryan-chang-105495215/"
    - label: "<i class='fas fa-envelope' title='Email'></i>"
      url: "mailto:rychang@mit.edu"
    - label: "Resume"
      url: "https://docs.google.com/document/d/16DsdvK2kBI4PQ98Oe6ALp_GboH2S2mnwVawCef40sw8/edit?usp=sharing"
  caption:
excerpt: 'Student at the Massachusetts Institute of Technology (Class of 2025) studying Computer Science and Engineering'
---

<h2 class="archive__subtitle">{{ site.data.ui-text[site.locale].recent_posts | default: "Recent Blog Posts" }}</h2>

{% if paginator %}
  {% assign posts = paginator.posts %}
{% else %}
  {% assign posts = site.posts %}
{% endif %}

{% assign entries_layout = page.entries_layout | default: 'list' %}
<div class="entries-{{ entries_layout }}">
  {% for post in posts %}
    {% include archive-single.html type=entries_layout %}
  {% endfor %}
</div>

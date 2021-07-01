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
      url: "mailto:chang.ryan10145@gmail.com"
    - label: "Resume"
      url: "https://docs.google.com/document/d/1lBLfUP8cBXVQ28--0WeDb10NiBx46YvfKk3CK8KEeVc/edit?usp=sharing"
  caption:
excerpt: 'Incoming freshman at the Massachusetts Institute of Technology studying Computer Science and Engineering'
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

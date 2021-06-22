---
layout: splash
permalink: /
header:
  overlay_color: "#5e616c"
  overlay_image: 
  cta_label: "<i class='fab fa-github'></i> GitHub Profile"
  cta_url: "https://www.github.com/Ryan10145"
  caption:
excerpt: 'Incoming freshman at the Massachusetts Institute of Technology studying Computer Science and Engineering'
---

<h3 class="archive__subtitle">{{ site.data.ui-text[site.locale].recent_posts | default: "Recent Posts" }}</h3>

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

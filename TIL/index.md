---
layout: default
title: "TIL"
main: true
header: true
---

<ul class="catalogue">
{% assign sorted = site.pages | sort: 'order' | reverse %}
{% for page in sorted %}
{% if page.TIL == true %}
{% include post-list.html %}
{% endif %}
{% endfor %}
</ul>

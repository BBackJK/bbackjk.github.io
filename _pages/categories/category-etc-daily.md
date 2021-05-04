---
title: "일상"
layout: archive
permalink: categories/daily
author_profile: true
---

{% assign posts = site.categories.daily %}

{% for post in posts %} 
  {% include archive-single2.html type=page.entries_layout %} 
{% endfor %}
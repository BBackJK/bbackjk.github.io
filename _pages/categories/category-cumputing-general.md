---
title: "컴퓨터 일반"
layout: archive
permalink: categories/computing/general
author_profile: true
---

{% assign posts = site.categories.computing %}

{% for post in posts %} 
  {% include archive-single2.html type=page.entries_layout %} 
{% endfor %}
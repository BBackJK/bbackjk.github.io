---
title: "자바 기초"
layout: archive
permalink: categories/java/basic
author_profile: true
---

{% assign posts = site.categories.java %}

{% for post in posts %} 
  {% include archive-single2.html type=page.entries_layout %} 
{% endfor %}
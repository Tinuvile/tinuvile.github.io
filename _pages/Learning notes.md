---
title: "Learning notes"
layout: archive
permalink: /Learning notes/
author_profile: true
---

<ul>  
  {% for post in site.categories.learning %}  
    <li>  
      <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>  
    </li>  
  {% endfor %}  
</ul>

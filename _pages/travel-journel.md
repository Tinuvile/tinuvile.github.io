---
title: "Travel journals"
layout: archive
permalink: /travel-journal/
author_profile: true
---

<ul>  
  {% for post in site.categories.travel %}  
    <li>  
      <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>  
    </li>  
  {% endfor %}  
</ul>

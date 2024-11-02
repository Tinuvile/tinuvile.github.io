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
  <li>  
    <a href="{{ site.baseurl }}/CS70/">CS70 合集</a>  
  </li>  
  <li>  
    <a href="{{ site.baseurl }}/nand2tetris/">nand2tetris 合集</a>  
  </li>  
  <li>  
    <a href="{{ site.baseurl }}/CS61B/">CS61B 合集</a>  
  </li>  
</ul>

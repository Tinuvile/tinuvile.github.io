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
    <a href="{{ site.baseurl }}/CS70/">CS70 Notes</a>  
  </li>  
  <li>  
    <a href="{{ site.baseurl }}/nand2tetris/">nand2tetris</a>  
  </li>  
</ul>

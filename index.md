---
layout: default
title: Home
---

<ul>
  {% for post in site.posts %}
    <li><time>{{ post.date | date: "%m/%d/%Y" }}</time>
      <span>|</span>
      <a href="{{ post.url }}">{{ post.title }}</a>
      <!-- <div class="post-description">{{ post.description }}</div> -->
    </li>
  {% endfor %}
</ul>

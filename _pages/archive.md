---
layout: default
title: Lưu trữ
---

<ul class="posts">
  {% for post in site.posts %}
  <li>
    <span>
      <a href="{{ site.baseurl }}{{ post.url }}">
        {{ post.title }}
      </a>
    </span>
  </li>
  {% endfor %}
</ul>

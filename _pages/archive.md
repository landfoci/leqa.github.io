---
layout: default
title: Lưu trữ
---

<ul class="posts">
  {% for post in site.posts %}
  <li>
    <div>
      <time class="date" datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%d-%m-%y" }}</time>
    </div>
    <span>
      <a href="{{ site.baseurl }}{{ post.url }}">
        {{ post.title }}
      </a>
    </span>
  </li>
  {% endfor %}
</ul>

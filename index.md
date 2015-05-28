---
layout: page
title: shailendra's blog
tagline: data science, statistics and other stuff
---
{% include JB/setup %}

<ul class="posts">
    {% for post in site.posts limit 1000 %}
      <li>
        <span>{{ post.date | date_to_string }}</span> &raquo; 
        <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a>
      </li>
    {% endfor %}
</ul>

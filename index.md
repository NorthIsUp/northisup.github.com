---
layout: page
title: North Is ⇡
---
{% include JB/setup %}

{% for post in site.posts limit:3 %}
## <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a>

{{ post.excerpt }}
<hr />
<hr />

{% endfor %}


<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

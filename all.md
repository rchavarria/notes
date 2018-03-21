---
layout: default
title: "Artículos por categoría"
---

{% for category in site.categories %}
## {{ category | first }}
  {% for posts in category %}
    {% for post in posts %}
- [{{ post.title }}]({{ site.baseurl }}/{{ post.url }})
    {% endfor %}
  {% endfor %}
{% endfor %}


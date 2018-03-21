---
layout: default
title: "Artículos por categoría"
---

{% for category in site.categories %}
## {{ category | first }}
  {% for posts in category %}
    {% for post in posts %}
      - [post.title]({{ site.baseurl }}/{{ post.url }})
    {% endfor %}
  {% endfor %}
{% endfor %}

# Lo de antes

{% for posts in category %}
  <li><a name="{{ category | first }}">{{ category | first }}</a>
    <ul>
    {% for posts in category %}
      {% for post in posts %}
        <li><a href="{{ post.url }}">{{ post.title }}</a></li>
      {% endfor %}
    {% endfor %}
    </ul>
  </li>
{% endfor %}

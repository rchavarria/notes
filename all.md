---
layout: default
---

{% for post in site.posts %}
- [{{ post.title }}]({{ site.baseurl }}/{{ post.url }})

{% endfor %}

All by category

{% for category in site.categories %}
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

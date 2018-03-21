---
layout: default
---

{% for post in site.posts.take(5) %}
# [{{ post.title }}]({{ site.baseurl }}/{{ post.url }})

{{ post.excerpt }}

{% endfor %}

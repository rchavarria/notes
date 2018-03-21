---
layout: default
---

{% for post in site.posts[0..10] %}
# [{{ post.title }}]({{ site.baseurl }}/{{ post.url }})

{{ post.excerpt }}

{% endfor %}

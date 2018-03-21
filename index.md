---
layout: default
---

{% for post in site.posts[0..5] %}
# [{{ post.title }}]({{ site.baseurl }}/{{ post.url }})

{{ post.excerpt }}

{% endfor %}

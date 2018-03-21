---
layout: default
---

{% for post in site.posts limit:20 offset:0 %}
### {{ forloop.index }}. [{{ post.title }}]({{ site.baseurl | append:post.url }})

{{ post.excerpt }}

{% endfor %}

<hr>

Ver [todos los posts port categoría]({{ site.baseurl | append:"/all" }})

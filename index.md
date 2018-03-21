---
layout: default
---

{% for post in site.posts limit:5 offset:0 %}
### [{{ post.title }}]({{ site.baseurl | append:"/" | append:post.url }})

{{ post.excerpt }}

{% endfor %}

<hr>

Ver [todos los posts port categoría]({{ site.baseurl | append:"/all" }})

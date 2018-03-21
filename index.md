---
layout: default
---

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>

# MORE

<div class="blog-index">
  {% assign index = true %}
  {% for post in paginator.posts %}
  {% assign content = post.content %}
    <article>
      {% include article.html %}
    </article>
  {% endfor %}
  <div class="pagination">
    {% if paginator.next_page %}
      <a class="prev" href="{{paginator.next_page}}">&larr; Older</a>
    {% endif %}
    <a href="/blog/archives">Archivo</a>
    {% if paginator.previous_page %}
    <a class="next" href="{{paginator.previous_page}}">Newer &rarr;</a>
    {% endif %}
  </div>
</div>

---
layout: default
---

{% assign title = page.name | split: "." | first %}

# Article list : {{ title }}

<ul class="list-style-file">
{% for post in site.posts %}
    {% if post.categories contains title %}
        <li><a href="{{ post.url }}"><span class="date">[{{ post.date | date : "%Y-%m-%d" }}]</span>{{ post.title }}</a></li>
    {% endif %}
{% endfor %}
</ul>
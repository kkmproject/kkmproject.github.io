---
layout: default
---

**default**
<ul class="list-style-file">
        <li><a href="/home/about">about</a></li>
</ul>

**List of article categories**
<ul class="list-style-directory">
    {% for ca in site.data.categories_for_articles %}
        <li><a href="{{ ca.link }}">{{ ca.name }}</a></li>
    {% endfor %}
</ul>
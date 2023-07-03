---
layout: default
---

**default**
<ul class="list-style-file">
    <li><a href="/home/about">about</a></li>
</ul>

**List of categories**
<ul class="list-style-directory">
    {% for main_category in site.data.main_categories %}
        <li><a href="{{ main_category.link }}">{{ main_category.name }}</a></li>
    {% endfor %}
</ul>

**The last 5 articles**
<ul class="list-style-file">
    {% for post in site.posts limit:5 %}
        <li><a href="{{ post.url }}"><span class="date">[{{ post.date | date : "%Y-%m-%d" }}]</span><span>[{{ post.categories[-1] }}]</span>{{ post.title }}</a></li>
    {% endfor %}
</ul>
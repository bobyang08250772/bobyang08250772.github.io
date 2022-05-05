---
layout: page
title: Blog Archive
---

<ul>
        {% for cat in site.categories %}
        <li>
                {% assign cat_name = cat[0] %}
                <div class="Projects">
                        <h1>{{ cat_name }}</h1>
                        <ul>
                                {% for post in site.categories[cat_name] %}
                                <li>
                                        <span class="date">{{ post.date | date: '%Y %b %d' }}</span> - <a href="{{ post.url }}">{{ post.title }}</a>
                                </li>
                                {% endfor %}
                        </ul>
                </div>
        </li>
        {% endfor %}
</ul>

---
layout: default
---

{% for post in site.posts reversed %}
<!--span class="post-meta">{{ post.date | date: "%b %-d, %Y" }}</span-->

{% if post.abstract %} <!-- Always both abstract + title -->

* [{{ post.title }}]({{ post.url | remove: '/' | prepend: site.baseurl }}) {{ post.abstract }}

{% else %}
{{ post.content }}
{% endif %}
{% endfor %}

<!--p class="rss-subscribe">subscribe <a href="{{ "/feed.xml" | prepend: site.baseurl }}">via RSS</a></p-->


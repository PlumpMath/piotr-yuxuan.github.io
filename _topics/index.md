---
layout: page
title: piotr-yuxuan.github.io
changefreq: daily
abstract_html: "<p>Well, this points to the page you're currently reading at. This site is to make my mind clearer: it's also a topic we can talk about. See the <a href='/'>homepage</a> for further explanations. This is meta ha ha!</p>"
---

## Topics

Topics order is not relevant but merely lexicographic. Here are just shown topics with an abstract. Give a look to the menu sublevels for a more comprehensive list.

{% for topic in site.topics | sort: 'title' %}
{% if topic.abstract_html %}
<div class="whole single-post-excerpt">
<h3><a href="{{ topic.url }}">{{ topic.title }}</a></h3>
<div class="description">{{ topic.abstract_html }}</div>
</div>
{% endif %}
{% endfor %}

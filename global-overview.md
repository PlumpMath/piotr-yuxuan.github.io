---
layout: page
title: Global overview
---

## Topics

Global introduction to topics. I can write here.

{% for post in site.collections.topics %}
<div class="unit whole single-post-excerpt">
<h3><a href="{{ post.url }}">{{ topic.title }}This {{ topic.name }} is a big title in sentence case</a></h3>
<p class="description">{{ topic.excerpt | strip_html}}I'm hereby willing to introduce to some interests I have. It's not about revealing to the world my splendid masterwork lol -- I just do this as a hobby. It's more about the exercice to express and explain an idea. I believe this can be very helpful for me to make my mind clearer.</p>
</div>
{% endfor %}

I still can write here but it's likely to be skipped.

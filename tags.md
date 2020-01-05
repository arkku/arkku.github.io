---
layout: default
title: Tag
---

# Tags
{:.no_toc}

* Table of Contents
{:toc}

{% assign rawtags = "" %}
{% for post in site.posts %}
    {% assign ttags = post.tags | join:'|' | append:'|' %}
    {% assign rawtags = rawtags | append:ttags %}
{% endfor %}
{% assign rawtags = rawtags | split:'|' | sort %}

{% assign tags = "" %}
{% for tag in rawtags %}
    {% if tag != "" %}
        {% if tags == "" %}
            {% assign tags = tag | split:'|' %}
        {% endif %}
        {% unless tags contains tag %}
            {% assign tags = tags | join:'|' | append:'|' | append:tag | split:'|' %}
        {% endunless %}
    {% endif %}
{% endfor %}

{% for tag_name in tags %}
{% capture tag %}{{ tag_name | slugify }}{% endcapture %}
{% assign tag_posts = site.posts | where_exp: "post", "post.tags contains tag_name" %}
{% unless tag_posts.size == 0 %}
## {{ tag }}

<dl class="tag-posts">
{% for post in tag_posts %}
    {% include post_item.html %}
{% endfor %}
</dl>
{% endunless %}
{% endfor %}

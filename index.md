---
title: home
privacylink: true
---

<!-- markdownlint-disable MD022 -->

## Introduction
{:.no_toc}

<div style="float: right; margin-left: 2em; margin-bottom: 2em">
{% avatar {{ site.author.github }} %}
</div>

I, [Arkku](https://github.com/arkku/), program software for computers, microcontrollers, and mobile devices. Occassionally I tinker with electronics and retrocomputing. This site is for posting about those topics.

(I have [other interests](https://www.flickr.com/photos/arkku/) and [other sites](https://arkku.com/), but I seldom get around to posting on those. This site is more automated.)

## Topics
{:.no_toc}

* Table of Contents
{:toc}

{% assign categories_count = 0 %}
{% assign post_limit = 10 %}
{% for category in site.categories %}
    {% capture category_name %}{{ category | first }}{% endcapture %}
    {% capture category_link %}/{{ category_name | slugify }}{% endcapture %}
    {% assign category_posts = site.categories[category_name] | where_exp: "post", "post.categories[0] == category_name" %}
{% unless category_posts.size == 0 %}
{% assign categories_count = categories_count | plus: 1 %}

## [{{ category_name }}]({{ category_link | relative_url }})

<dl>
{% assign post_count = site.categories[category_name].size %}
{% for post in category_posts limit:post_limit %}
{% include post_item.html %}
{% endfor %}
{% if post_count > post_limit %}
    {% assign more_count = post_count | minus:post_limit %}
    {% assign next_post_link = site.categories[category_name][post_limit].title | slugify %}
    <dt><a class="post-title" href="{{ category_link | relative_url }}#{{ next_post_link }}">{{ more_posts }} more post{% if more_posts != 1 %}s{% endif %}</a></dt>
{% endif %}
</dl>
{% endunless %}
{% endfor %}
{% if categories_count == 0 %}
<p style="float: left">Under construction.</p>

<img src="{{ "/assets/img/under-construction.gif" | relative_url }}" width="133" height="133" alt="[Under construction]" style="width: 133px; height: 133px; float: right;" />
{% endif %}

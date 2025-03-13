---
layout: page
title: Table of Contents
permalink: /table-of-contents/
---

## Computer Science (CS)
{% for post in site.categories.cs %}
- {{ post.date | date: "%Y-%m-%d" }} - [{{ post.title }}]({{ site.baseurl }}{{ post.url }})
{% endfor %}

## Reading
{% for post in site.categories.reading %}
- {{ post.date | date: "%Y-%m-%d" }} - [{{ post.title }}]({{ site.baseurl }}{{ post.url }})
{% endfor %}

## Projects
{% for post in site.categories.project %}
- {{ post.date | date: "%Y-%m-%d" }} - [{{ post.title }}]({{ site.baseurl }}{{ post.url }})
{% endfor %}

## Markets & Trading
{% for post in site.categories.markets %}
- {{ post.date | date: "%Y-%m-%d" }} - [{{ post.title }}]({{ site.baseurl }}{{ post.url }})
{% endfor %}


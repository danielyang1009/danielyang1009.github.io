---
layout: post
date: 2017-04-18T00:00:00Z
title: Jekyll Pagination
description: Modified bootstrap pagination style to work with jekyll
categories: jekyll
tags: jekyll
---

## Setup

Another goal in building my personal website/blog is to have pagination. Bootstrap is already provide us with functional layout. We just need to modified it to work with jekyll. First, we need to set it up in our `_config.yml` file to include `jekyll-paginate`. `paginate` is set to 5, to only show 5 posts per page. And `paginate_path` is the path to show, in my case will be shown as `dyang.io/page2`.

```html
gems: [jekyll-paginate]
paginate: 5
paginate_path: "/page:num/"
```

## Bootstrap pagination

Basic bootstrap pagination copied from bootstrap website.

```html
<nav aria-label="Page navigation">
  <ul class="pagination">
    <li>
      <a href="#" aria-label="Previous">
        <span aria-hidden="true">&laquo;</span>
      </a>
    </li>
    <li><a href="#">1</a></li>
    <li><a href="#">2</a></li>
    <li><a href="#">3</a></li>
    <li><a href="#">4</a></li>
    <li><a href="#">5</a></li>
    <li>
      <a href="#" aria-label="Next">
        <span aria-hidden="true">&raquo;</span>
      </a>
    </li>
  </ul>
</nav>
```

## Modified to work with jekyll

One thing to notice is that `jekyll-paginate` is that pagination  page number starting with 2. Therefore, we need to pay attention to `page1` case. Please see reference: [Jekyll Pagination](https://jekyllrb.com/docs/pagination/)

```html
{% raw %}
{% if paginator.total_pages > 1 %}
<div>
  <ul class="pagination">
    <!-- previous page -->
    <li>
      {% if paginator.previous_page %}
        <a href="{{ paginator.previous_page_path | prepend: site.baseurl | replace: '//', '/' }}">&laquo; Prev</a>
      {% else %}
        <span>&laquo; Prev</span>
      {% endif %}
    </li>
    <!-- list of pages -->
    {% for page in (1..paginator.total_pages) %}
    <li>
      {% if page == paginator.page %}
      <span><strong>{{ page }}</strong></span>
      {% elsif page == 1 %}
        <a href="{{ paginator.previous_page_path | prepend: site.baseurl | replace: '//', '/' }}">{{ page }}</a>
      {% else %}
        <a href="{{ site.paginate_path | prepend: site.baseurl | replace: '//', '/' | replace: ':num', page }}">{{ page }}</a>
      {% endif %}
    </li>
    {% endfor %}
    <!-- next page -->
    <li>
      {% if paginator.next_page %}
        <a href="{{ paginator.next_page_path | prepend: site.baseurl | replace: '//', '/' }}">Next &raquo;</a>
      {% else %}
        <span>Next &raquo;</span>
      {% endif %}
    <li>
  </ul>
</div>
{% endif %}
{% endraw %}
```

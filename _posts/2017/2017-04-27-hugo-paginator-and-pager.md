---
layout: post
date: 2017-04-27
title: Hugo Paginator and Pager
description: Create hugo paginator and pager
categories: hugo
tags: hugo
---

## Pagination

Hugo has a nice support for pagination as well as pager. To check if previous and next pages exists. We can use `.Paginator.HasPrev` and `.Paginator.HasNext`. And use `.Paginator.Prev.URL` and `.Paginator.Next.URL` to go between previous and next pagination page.

{% raw %}
```html
<div class="container">
  <ul class="pager align-center">
    {{ if .Paginator.HasPrev }}
      <li class="previous"><a href="{{ .Paginator.Prev.URL }}">Prev</a></li>
    {{ else }}
      <li class="previous disabled"><a href="">Prev</a></li>
    {{ end }}
    <li>
      <a href="" class="button round small outline">Page {{ .Paginator.PageNumber }} of {{ .Paginator.TotalPages }}</a>
    </li>
    {{ if .Paginator.HasNext }}</a>
      <li class="next"><a href="{{ .Paginator.Next.URL }}">Next</a></li>
    {{ else }}
      <li class="next disabled"><a href="">Next</a></li>
    {{ end }}
  </ul>
</div>
```
{% endraw %}

## Pager

To check if previous or next blog post exists, use `.Prev` and `.Next`. To go between blog posts use `.Prev.Permalink` and `.Next.Permalink`.

{% raw %}
```html
<div class="container">
  <hr>
  <ul class="pager align-center">
    {{ if .Prev }}
      <li class="previous"><a href="{{ .Prev.Permalink }}"><i class="fa fa-angle-left"></i> {{ .Prev.Title }}</a></li>
    {{ end }}
    {{ if .Next }}</a>
      <li class="next"><a href="{{ .Next.Permalink }}">{{ .Next.Title }} <i class="fa fa-angle-right"></i></a></li>
    {{ end }}
  </ul>
</div>
```
{% endraw %}

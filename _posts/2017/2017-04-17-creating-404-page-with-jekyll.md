---
layout: post
date: 2017-04-17
title: Creating 404 Page with Jekyll
description: 404 page for Github page with jekyll
categories: jekyll
tags: jekyll
---

## Create a 404 page

It's really easy to create a custom 404 page with jekyll. First, create `404.html` in your root folder. Then in `YAML front matter`, setup `permallink: /404.html`. And that's it.

For more detailed gitHub pages official documentation, please see [Github Help](https://help.github.com/articles/creating-a-custom-404-page-for-your-github-pages-site/). And to know more, see [Jekyll Permalink](https://jekyllrb.com/docs/permalinks/).

## Code
Here's the code of my `404.html` page for this website.
```html
---
layout: default
permalink: /404.html
---

<h1>404. That’s an error.</h1>
<p>The requested URL was not found on this server. </p>
```

---
layout: post
date: 2017-04-16
title: Jekyll Archive By Tag
description: Using jekyll to create tag archive page
categories: jekyll
tags: jekyll
---

## Problems

This is one of the challenge I faced, when I building this blog with Jekyll. It's to create beautiful tag archive page.

## Implement

First, by creating a `/_layouts/tagpage.html` layout file will save us a lot of effort.

```html
---
layout: default
---

<h1>Articles in tag "{{ page.tag }}"</h1>
<br/>

<ul>
  {% for post in site.tags[page.tag] %}
  <li>{{ post.date | date: "%m/%d/%Y" }}:
    <a href="{{ post.url }}">{{ post.title }}</a>
    <p><em>{{ post.meta }}</em></p>
  </li>
  {% endfor %}
</ul>
```

This will collect all articles from same tag. It will also generate `url` and `title` for us, as well as including `meta` data. Then we just need to create our tag in tag folder like `/tag/python/`. And it also serve as the link address we will visit. And let Jekyll know what exactly is the tag we want to filter. In this case, it's `python`. And keep adding folders in our tag folder to expand future tags.

```html
---
layout: tagpage
title: Articles in tag "python"
tag: python
---
```

```html
project-dyang/
├── .../
└── tag/
    ├── python/
    │   └── index.html
    ├── ruby/
    │   └── index.html
    └── .../
        └── index.html
```

## Improvement

In the above solution, even we achieve our goal, we still have too many folder/index.html in tag folder. And it looks pretty messy in our tag folder.

We can flattening these folders and pages by using `permalink`, like in example below. Then we can still visit our tag archive page by `/tag/python/`. Even we didn't create `/tag/python/` folder, which makes our tag folder a lot cleaner. To know more, please see [Jekyll Permalink](https://jekyllrb.com/docs/permalinks/).

```html
---
layout: tagpage
title: Articles in tag "python"
tag: python
permalink: /tag/python/
---
```

```html
project-dyang/
├── .../
└── tag/
    ├── python.html
    ├── ruby.html
    └── ...
```

---
layout: post
date: 2017-04-16
title: Jekyll Archive By Tag
description: Using jekyll to create tag archive page
categories: jekyll
tags: jekyll
---

## Problems

This is one of the challenge I faced. When I building this blog with Jekyll, it's how to create beautiful tag archive page. I also find out that it's the exact same way you can make category page, which I will explain more details.

## Implement

First, creating a `/_layouts/tagpage.html` layout file will save us a lot of effort. This basically create a template which shows posts in same tag. The reason why I choose to use {{ page.tag }} is I will create a bunch of 'dummy' tag pages which we can link to. And in these 'dummy' tag pages, we can specific which tag we want, like 'python', 'jekyll' and so on.

###### tapage layout

{% raw %}
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
{% endraw %}

This will collect all articles from same tag. It will also generate `url` and `title` for us, as well as including `meta` data. Then we just need to create our pages in tag folder like `/tag/python/`. And it also serve as the link address we will visit. And let Jekyll know what exactly is the tag we want to filter. In this case, it's `python`. And keep adding folders in our tag folder to expand future tags. As I mentioned you can use exact same method to make a category page. Simply change all `tags` in above code to `categories` keyword. I believe in `Jekyll`, `tags` and `categories` are interchangeable, meaning they just the same thing.

###### Front matter
{% raw %}
```html
---
layout: tagpage
title: Articles in tag "python"
tag: python
permalink: /tag/python/
---
```
{% endraw %}

We also flatten these pages by using `permalink`. We can visit our tag archive page by `/tag/python/`. Even we didn't create `/tag/python/` folder, which makes our tag folder a lot cleaner. To know more, please see [Jekyll Permalink](https://jekyllrb.com/docs/permalinks/).

###### File structure
```html
website/
├── .../
└── tag/
    ├── python.html
    ├── ruby.html
    └── ...
```

Now we have created all pages we need. We can now organized everything back in single `tag.html` or `category.html` page. If you want to create a category page, then just change `site.tags` to `site.categories`. In the following example. `tag[0]` is the name of tag. And `tag[1]` is the list of posts in this tag. Therefore we can use `tag[1] | size` to count how many posts in a tag.

###### Liquid code

{% raw %}
```html
{% for tag in site.tags %}
<li>
  <div class="tag-title">
    <a href="/tag/{{ tag[0] }}">
      {{ tag[0] | capitalize }}: {{ tag[1] | size }}
    </a>
  </div>
</li>
{% endfor %}
```
{% endraw %}

We can flattening these folders and pages by using `permalink`, like in example below. Then we can still visit our tag archive page by `/tag/python/`. Even we didn't create `/tag/python/` folder, which makes our tag folder a lot cleaner. To know more, please see [Jekyll Permalink](https://jekyllrb.com/docs/permalinks/).

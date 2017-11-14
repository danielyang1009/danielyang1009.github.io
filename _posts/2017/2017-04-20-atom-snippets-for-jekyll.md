---
layout: post
date: 2017-04-20
title: Atom Snippets for Jekyll
description: Create atom snippets to speed up writing
categories: atom
tags: atom jekyll
---

## Snippets

When I create this technical blog, I'm having a lot of code in every post. often I have to write a lot of `liquid` code. And it's getting really annoying. It's much needed to create snippets to speed up writing. For mode detail information, see [Atom Snippets](https://github.com/atom/snippets).

## Example

The leftmost key is selector for different language. One language can have one selector. Different snippet just follows under some selector. Second key is for the name of snippet, `prefix` is the trigger of the snippet. And `body` is actual code of the snippet. In this example, I can type `%ht` and hit <kbd>tab</kbd> to generate the body of snippet. `$1` is a place holder. It's where we want to insert. And we can have multiple stops to insert.

{% raw %}
```html
'.source.gfm':
  'highlight+html':
    'prefix': '%ht'
    'body': """
    {% highlight html %}
    $1
    {% endhighlight %}
    """
```
{% endraw %}

Here is a list of selectors for different language.

- Markdown: `.source.gfm`
- HTML: `.text.html`
- CSS: `.source.css`
- SASS: `.source.sass`
- JavaScript: `.source.js`
- JSON: `.source.json`
- PHP: `.text.html.php`
- Java: `.source.java`
- Ruby: `.text.html.erb`
- Python: `.source.python`
- plain text: `.text.plain`

## Problem

In `markdown` file, the snippets are working perfectly. However, in `html` file, because I have also install `emmet`, they conflict when I'm using <kbd>tab</kbd>. emmet will automatically generate `html` tag for that. One better solution is for atom `emmet` to have a filter, which don't expand non-keyword word. Faster way is just disable keyboard shortcut <kbd>tab</kbd> for `emmet`. And use <kbd>ctrl+e</kbd> instead.

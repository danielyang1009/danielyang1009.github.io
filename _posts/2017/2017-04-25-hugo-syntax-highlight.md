---
layout: post
date: 2017-04-25
title: Hugo Syntax Highlight
description: Easy way to get syntax highlight with hugo
categories: hugo
tags: hugo
---

## Syntax highlight

Since this is a blog will mainly focus on technical side, I will be posting a lot of code in this blog. Therefore, it's important to configure syntax highlight correctly. There are two important variable to set in `config.toml`.

- `pygmentsuseclasses`

- `PygmentsCodeFences`

In default, `pygmentsuseclasses` is set to `fales`, which means your html code will be generated with embedded color, which will make it impossible to change from your stylesheet. Good thing is it's really simple. You can look up the theme you want from [pygments-css](http://richleland.github.io/pygments-css/), and set `pygmentsstyle` to whatever the theme you like in `config.toml`

The second way which I preferred, is to set `pygmentsuseclasses = true`. This way the color for syntax highlight will not embedded with html code. And you can adjust it by adding css file. Or you can download the style from `pygments-css`.

When putting a code block, you need to use `liquid template` in jekyll or `go template` in Hugo. If you use github a lot, you will certainly miss github style code fences. In hugo, you can turn that on by using `PygmentsCodeFences = true`.

Reference: [Syntax highlighting](https://gohugo.io/extras/highlighting/)

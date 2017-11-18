---
layout: post
date: 2017-04-22
title: Blog with Hugo
description: Switch to hugo, and thoughts on hugo vs jekyll
categories: hugo
tags: hugo
---

## Switch from jekyll

When I first want to build a blog and counter jekyll, I'm really happy about the result for only working for days. It's easy, fast and GitHub Pages supported. I found this great tutorial on YouTube by [Thomas Bradley](https://www.youtube.com/playlist?list=PLWjCJDeWfDdfVEcLGAfdJn_HXyM4Y7_k-). It really makes everything clear and simple to build basic framework of the website. With a little help from `Bootstrap`, I, even never build a website myself, finished first version of my blog within a week. Then I found `Hugo`, same static website generator by `golang`. It's really fast compare to `jekyll`, [Hugo benchmark](https://www.youtube.com/watch?v=CdiDYZ51a2o). It completed 5,000 posts in 7 second. It could be a main advantage of hugo inherit by `golang`.

###### Pros

- Super fast
- More flexible syntax than liquid template
- Since uploading content not source code, no wait until GitHub Pages render your pages
- Theme feature, easily switch and package theme

###### Cons

- Not GitHub Page supported
- No default theme to show content
- Docs is not as clear and easy to follow as jekyll

## Quick start

1. Download and install hugo from [Hugo](https://gohugo.io/).
2. Create a new folder for your website and `hugo new site .` or `hugo new site sitename`, hugo will create for you.
3. Create a sample post by `hugo new post/postname.md`, hugo will create `front matter` for you.
4. Download theme from [Hugo Themes](https://themes.gohugo.io/), unzip and put it in `sitename/themes`
5. Let hugo know which theme you're using, by adding `theme = "themename"` to `config.toml`
6. Fire up hugo by `hugo` or `hugo serve`, using `hugo` will build your website under `public` folder, `hugo serve -w` wont' create anything, just visit site at
`localhost:1313`. `-w` to watch the website change and reflect immediately.

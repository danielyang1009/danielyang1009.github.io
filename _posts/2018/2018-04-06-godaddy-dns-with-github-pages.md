---
layout: post
date: 2018-04-06
title: GoDaddy DNS with Github Pages
description: Setting up GoDaddy domain with Github Pages
categories: github
tags: github godaddy
---

## Steps

1. In your repository, go to Settings, under Github Pages section, fill in your custom domain. This will create a CNAME file in your repository.

2. Add an `A` (host) record with `host = @` and `Points to = 192.30.252.153`.

3. You can also set up an alias record. Add a `CNAME` (alias) record with `host = www` and `Points to = yourname.github.io`.

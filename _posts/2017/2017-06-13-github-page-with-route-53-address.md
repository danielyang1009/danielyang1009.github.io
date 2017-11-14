---
layout: post
date: 2017-06-14
title: Github Page with Route 53 Address
description: Hosting github page with amazon route 53
categories: aws
tags: aws github
---

## Intro

I quite often started a new project and wanted a custom domain rather than a domain start with `github.com`. I've been using Amazon Web Services (AWS) for a while. I used to host my blog using Amazon S3. And now since everything is free with Github Page, I move the whole blog to Github Page immediately. And route 53 still provide a pretty cheap domain name with $12/year. It seems logical to combine these two together. Hosting pages on Github pages and using AWS route 53 name services.

## Steps

First, register a domain name with route 53. Or If you don't have a AWS account just get one. And it offers wonderful free tier services.

Second, in your route 53 dashboard, click hosted zones. It will provide you with a list of domain names you have with route 53. And then click the domain names you just created. Create an `A` type of record set. This will be your `yourdomain.com` rule. Keep everything the same. And add `192.30.252.153` and `192.30.252.154` in IPv4 address box. And save the record set.

Third, create another `A` type of record set. And this will be your `www.yourdomian.com` rule. And it will be an alias for `yourdomian.com`. Choose `alias` on the dashboard, from dropdown menu, choose `yourdomain.com`. Save the record set.

Last, go back to Github repository and create a file name `CNAME` and put in `yourdomian.com` in that file and save.

And that's it. You can visit your Github page from the domain name you get from AWS route 53 services.

[GitHub: Setting up an apex domain](https://help.github.com/articles/setting-up-an-apex-domain/)

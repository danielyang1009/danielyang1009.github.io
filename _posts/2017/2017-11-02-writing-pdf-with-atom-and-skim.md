---
layout: post
date: 2017-11-03
title: Writing PDF With Atom and Skim
description: Setting up an environment writing PDF with Atom and Skim
categories: atom
tags: atom skim
---

## Intro

When huge amount of books and articles I read, I believe the best way to remember them is by note-taking. It's for summarizing things I learn, and for future reference. It's also the reason I created this blog. As a mathematics major, I dealt with math equations a lot. After dealt with org-mode and markdown. I feel like I shall give Latex a go. Here's how I configure Latex note-taking environment with my MacBook.

## MacTex

Since I use MacBook as my primary computer. [MacTex](http://www.tug.org/mactex/) is everything I need to compile a tex file. And it's pretty large, 3.0G. You can also download the basic version which is only around 72M. But I don't suggest you do that. Since the full version include some necessary software like `Tex Live Utility` which help you manage and update plugins. And you can also use included `TexShop` for writing latex files. For windows users, you can download [MiKTex](https://miktex.org/).

## Atom  

There's are two plugins you need for Atom. First one is [latex](https://atom.io/packages/latex). The second one is [language-latex](https://atom.io/packages/language-latex). The first one provide us the way to compile latex files. The second one provide the syntax highlight.

## Skim

Install [Skim](http://skim-app.sourceforge.net/). It's one of the best pdf reader on Mac OS. After you installed skim, go to Preference and then Sync tab. Choose Atom in PDF-Tex Sync support then you are all set. You can set up skim with other text editor from [TeX_and_PDF_Synchronization](https://sourceforge.net/p/skim-app/wiki/TeX_and_PDF_Synchronization/).

By setting up this `pdfsync`, you can jump back and forth between pdf file you created and the latex file you are writing. After you built/compile your latex file by <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>B</kbd>. Or you can use <kbd>Command</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd> to open command palette. From there you can just type in `build` to build the latex file. And the pdf file it generates, will be opened in Skim after the build is finished. From pdf file you created, you can press <kbd>Command</kbd>+<kbd>Shift</kbd> and click anywhere you want to edit. It will take you back to the exact line of the source code in latex.

## Github

When dealing with `.tex` files, it generates a lot of files that we do not want to upload to Github. So this is the `.gitignore` file, I'm been using. Or you can simply excluding `.aux`, `.log` files (there are tons of them) one by one.

```
# Ignore everything
*

# Except tex files
!.gitignore
!*.tex
!*.bib
!*.pdf

# Ignore subdirectories
!*/
```

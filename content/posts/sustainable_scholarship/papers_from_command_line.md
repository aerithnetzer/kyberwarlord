---
title: How to Write a Paper in Neovim 
date: 2024-06-30
draft: false
---

## Introduction

One of my formative experiences as an early-career librarian is when my coworker, a librarian, historian, and humanist, sent me [this article by The Programming Historian](https://programminghistorian.org/en/lessons/sustainable-authorship-in-plain-text-using-pandoc-and-markdown). The article spoke to my love of the command line and my hatred of word processors. This article is surely a great introduction to the philosophy and technology that powers sustainable scholarship for the humanities, and it is an invaluable first look for (post-)humanists at what technology outside the Microsoft behemoth is like. The Programming Historian's article makes use of mostly out-of-the-box features of text editors, which is of course great for certain people who are just getting started with these paradigms of computing. I hope that my contribution in this article is more of an appeal to the "hacker" ethic, where people bodge tools and programs together to create something that works really well for them, but where the content that they create with these tools can of course be easily shared with someone else.

## My Journey With Neovim

Neovim is at the core of everything that I create and interact with as a librarian. I use it to write articles, to write code, to jot down meeting notes or ideas, or to connect to remote HPC resources. Neovim is *highly* extensible, but also predictable in the way its' plugins are presented to the user. I have been using vim *motions* since I began writing shitty python code in high school all the way up to writing shitty python code for one of the largest tech consultancies and a top 10 research institution. The vast majority of text editors worth their salt have some kind of vim motion emulation. That is, you can use vim motions in a program that is outside vim. When I was in high school, we had IntelliJ licenses for our Computer Science class, and that was my first interaction with vim motions after the guy who I sat next to mentioned it to me. After flipping back and forth between commitment and non-commitment to vim motions across a variety of editors, I decided maybe a year ago that I was going vim full-time. I now use Neovim, where I can customize pretty much everything about my text editing experience. After being introduced to citeproc and pandoc a long time ago by my parter, a PhD student herself, I have found that Neovim is by far the best text editing experience I have had for academic writing.

## Citations and Research

Citations in Microsoft Word and Google Docs are in the 1980s compared to the open source community's approach to citations. In Microsoft Word, you cannot use bib files, can't automatically import metadata from a DOI, and the insert citations functions are useless with people who have no idea that these functions exist in Word. Have you ever tried getting anyone to use advanced features of word? It is a nightmare. Let us look at the simple elegance of Markdown and citeproc.

`paper.md`

```md
...According to Ma, et al., there exist concerns about equality for researchers who may be independent, unemployed, or retired @OpenAccessAtMaLa ...
```

One will notice that there is an unusual string of characters in at the end of the code block. `@OpenAccessAtMaLa` is a citeproc citation. It uses what are called citekeys to reference a citation in a `.bib` file. If you need more of an introduction to `.bib` files, [check out this section of The Programming Historian's article](https://programminghistorian.org/en/lessons/sustainable-authorship-in-plain-text-using-pandoc-and-markdown#working-with-bibliographies). Now this is where I diverge from The Programming Historian's article, as I have been using a citation manager from the command line called [papis](https://github.com/papis/papis). Papis is really great at staying out of my way. Although I appreciate Zotero for it's many features, I tend to prefer to read documents in something outside of Zotero, and make notes about it in Neovim. I particularly like the transparent file organization structure of papis, as I can easily access my documents programmatically without the use of a SQL API. Papis integrates very well with neovim by [papis.nvim](https://github.com/jghauser/papis.nvim). Where I can easily use the default keystrokes to cite an article.

Here is a gif of me typing this up!

This is a citation

@AnthropoceneCHarawa2015

This is how I can quickly open a file from neovim too!

---
title: "Migrating the site to Hugo"
date: 2023-02-03T14:21:20-05:00
tags: [lektor, hugo, site]
---

I've decided to migrate my site from [Lektor][lektor] to [Hugo][hugo]. This is solely because Hugo seems to have far more community surrounding it. I don't think I'm ever going to dig far enough into my site to muck with or redesign the core generator, so having a Python-based SSG doesn't make sense as a decision point. I think the way Hugo handles content and files makes more sense in my brain. Plus, the fact that it's `brew install`able is a big plus… having to remember to install Lektor on each machine and remember how and where it's installed was one bit of friction too many. Hopefully I'll be better about whipping out quick posts this way. 

The migration has been pretty simple, once I went through the [quickstart guide for Hugo][hugo-qs]. I'm using the [Blowfish][blowfish-theme] theme for the moment. I like that it supports KaTeX for math input, has syntax highlighting support, and the example site caught my eye. Another big plus to Hugo is that the page files are standard Markdown (Commonmark, but essentially the same thing). This means that metadata makes more sense, and my text editor recognizes the `.md` extension.   

[lektor]: https://www.getlektor.com
[hugo]: https://gohugo.io/
[hugo-qs]: https://gohugo.io/getting-started/quick-start/
[blowfish-theme]: https://github.com/nunocoracao/blowfish
---
title: TIL – Linking (and attaching) a local image in Lektor
date: 2022-11-15T14:21:20-05:00
author: Dustin Wheeler
tags: [TIL,lektor]
---

While trying to post the [previous item]({{< ref "blog/f360-sketch-pattern" >}}), I couldn't get the local image to display. I tried placing the PNG file in the post folder with the `contents.lr` file, then linking with `![alt-text](image.png)`, but couldn't get the page to render with the image. 

I found an old [StackExchange response][se-lektor-image] that suggested placing the image in the `assets/static` folder, then setting the path to `/static/assets/image.png`, but that didn't net me any results. 

Oddly enough, when I view the web editor, the image is listed as an attachment to the page… 

As a next step, I started investigating how [Lektor handles paths][lektor-paths]. From a brief read on that page, it seems like the image should be able to reside in the same folder as the post `contents.lr` file, and the path just needs to be `image.png`, but this definitely doesn't work. What am I doing wrong?

### --EDIT-- ###

I'm so dumb… Because of the text cropping, I couldn't tell that the name of my image was misspelled… instead of `screenshot_pattern_edit.png`, it was named `screenshot_patter_edit.png`, and that missing "n" made all the difference in the world. Now that I spelled it correctly, the image is attaching correctly. I think I'll stick with Lektor now, since it was _entirely_ my fault. 

![Misspelled filename isn't shown because the window edge clips the end of the filename.](./screenshot_clipped.png)

[se-lektor-image]: https://stackoverflow.com/questions/40263599/how-can-i-insert-images-in-lektor-markdown-sections
[lektor-paths]: https://www.getlektor.com/docs/content/paths/
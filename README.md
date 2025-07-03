# JSesh documentation web site

The old JSesh documentation site used dokuwiki, which is a very nice piece of software, but is not very easy to maintain.

I have decided to move most of my code to [grav](https://getgrav.org/), which I feel will be easier for me to work with (it has fewer security issues as I won't have editing features).

I will first "translate" all the existing JSesh documentation pages to markdown, and put the source for this documentation on github.

## Helping with the documentation

The JSesh documentation uses relatively simple files, in the [`markdown`](https://learn.getgrav.org/17/content/markdown) format.

To write a translation of the documentation, you need to create `.md` files, as is done for instance in the folder  `www/user/pages/040.editing/010.mouse`, which is the part of the documentation related to the mouse use:

| file name       | use                           |
| --------------- | ----------------------------- |
| docs.es.md      | spanish version of the page   |
| docs.fr.md      | french version                |
| docs.md         | default (english) version     |
| groupEditor.png | a picture used by those pages |
| Hm_kA.png       | a picture used by those pages |
| mr_xAswt.png    | a picture used by those pages |
| palette_en.png  | a picture used by those pages |
| stp_n_ra1.png   | a picture used by those pages |
| stp_n_ra2.png   | a picture used by those pages |
| w_and_t.png     | a picture used by those pages |

If we look at `docs.md`, we see 

~~~markdown
---
title: Mouse Editing // the title of the page, which should be translated
taxonomy:
    category: docs
---

...

Editing with the mouse is a simple but slow process. Typically, it is combined with other editing methods.

## Setting the Cursor Position (a second level title (say, section instead of chapter))

...

a picture :

![Sign Palette](palette_en.png)


~~~


## Running a local copy of the documentation

If you want to provide a translation for your own language, the pages are in `user/pages`. Look for the files ending in `.md`. To translate a file, simply create, at the same place, a file with the same name, but with ending `.LANG.md`, where LANG is the code for your language. You can ask me if you want.


~~~bash
cd www
./bin/grav serve
~~~
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


`.es` and `.fr` are codes for the language used. You can find them in the [description of ISO 639](https://en.wikipedia.org/wiki/List_of_ISO_639_language_codes).


If we look at `docs.md`, we see 

~~~markdown
---
title: Mouse Editing // the title of the page, which should be translated
author:... if you translate, you can put your name here...
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

Markdown is fairly straightforward. You can use the existing documentation as a guideline. In general, if you are translating the documentation, you will use the same structure as the existing documentation, so you can:

- copy the file you want to translate, adding the correct language code to it :
  ~~~
    cp docs.md docs.fr.md
  ~~~

- edit your new file, replacing the original text with its translation.

You might want to translate some of the pictures. It's quite easy. Simple create a new picture with the translated content.

Then in the markdown file, replace the name of the original picture with the translated one.


## Markdown enhancement for this site

This site allows you to :

- add captions to pictures like this:
  ~~~markdown
  ![](./tagEditor.png?classes=caption "The Tag Creation Window")
  ~~~

  You need to add `?classes=caption` after the picture name, then the caption itself, between quotes.

- use inline pictures. Normally, pictures will occur on a line of their own. If you want them to be part of the text, use `classes=inline` : 

  ~~~markdown
  ![](./importSigns3.png?classes=inline)
  ~~~

- use a simplified version of the *Manuel de Codage* to quote hieroglyphic texts. You need to write a `<span>` with class `mdc`:

  ~~~markdown
  It can be understood as a ligature between the sign <span class="mdc">F20</span> and the group <span class="mdc">xAst:xAst:xAst</span>.
  ~~~

Note that `*` has a special meaning for markdown, and that you might need to put a `\` in front of them:

~~~markdown
 <span class='mdc'>p\*t:pt</span>
~~~


## Where are the files ?

All the files you might need to edit or copy are in `www/user/pages`.

Some of them are called `chapter.md`, and others `docs.md`.

## Running a local copy of the documentation

If you want to provide a translation for your own language, the pages are in `user/pages`. Look for the files ending in `.md`. To translate a file, simply create, at the same place, a file with the same name, but with ending `.LANG.md`, where LANG is the code for your language. You can ask me if you want.


~~~bash
cd www
./bin/grav serve
~~~

## How to send me your modifications?

There are two approaches. One is relatively *low-tech*, the other requires some knowledge of `git`.

### Low-tech approach

The low-tech approach is the following:

- you download a copy of the JSesh documentation sources. The easiest way is to click on the green button labelled `code`, and select *Download zip*
- you create/edit/... the files you want to change;
- you create a **zip** archive of your text and you send it to me. It's important to keep the initial file layout. You can either zip the whole folder for the documentation, or only the folder called `pages` in `www/user/`.

### High-tech approach

You need to create a **github** account.

- log on your github account;
- visit https://github.com/rosmord/jsesh-documentation
- click on the **fork** button
- you now have your own copy of the documentation, which you can save to github with **git push** (or event edit online).
- when you look at your personnal github archive - in your web browser, you will see something like:

  ~~~
  This branch is 1 commit ahead of rosmord/jsesh-documentation:master. .... Contribute
  ~~~

  Click on the **Contribute** button to send your modifications for proofreading to my archive.

  
# JSesh documentation web site

The old JSesh documentation site used dokuwiki, which is a very nice piece of software, but is not very easy to maintain.

I have decided to move most of my code to [grav](https://getgrav.org/), which I feel will be easier for me to work with.

I will first "translate" all the existing JSesh documentation pages to markdown, and put the source for this documentation on github.

If you want to provide a translation for your own language, the pages are in `user/pages`. Look for the files ending in `.md`. To translate a file, simply create, at the same place, a file with the same name, but with ending `.LANG.md`, where LANG is the code for your language. You can ask me if you want.

If you want to run this website locally, you need to download a version of grav and copy the content of the grav bin folder in the www folder of this project. Then :

~~~bash
cd www
./bin/grav serve
~~~
---
title: Using Unicode Fonts
taxonomy:
    category: docs
    tag: []
---

To use a unicode font, you need to have a font with the correct signs. You will find [a page about transliteration](https://jsesh.qenherkhopeshef.org/fr/varia/transliteration) on the JSesh web site; [Daniel Werning](https://aaew.bbaw.de/egyptological-unicode-fonts) maintains a similar list which might be more up to date.


![](fontsprefsunicodetranslit.png)

- You should open the “Preferences” menu (on the Mac, it's in the “JSesh” menu; elsewhere, it's under the “Edit Menu”). 
- Go to the “Font Preferences” Tab.
- Select a font for transliteration
- Open the "show options" panel, and check "Unicode Transliteration font"

## Current problems with unicode fonts

The current support in operating system and softwares for the transliteration fonts is not good. Even Java on the Mac - and hence, JSesh - has problems.

The real problems are H̱ and yod

### Capital H̱

On some systems, H̱ (as in the ram-god *H̱nmw*) displays poorly. It depends on the font **and** on the software **and** on the system. In most cases, it's ok. One annoying exception is that it doesn't give a good result with JSesh **on Mac OS X**. Apparently, the rendering system gives better results on Windows. Note that if you paste your text in a word processor, you will probably get a good result anyway.

### Yod

**outdated - add A7BC code**. 

Unicode gives you a number of choices. I selected the two best solutions (the third one, using a kind of half circle of the yod accent, is simply reproducing a trick used when people had typewriters, and hand-made their yods with "c" letters). The problem is that, technically, the support for those solution is lacking.

The yod is supposed to be coded with a "i" (a //dotted// i, not a dotless one) and an accent. The font should contain enough information to display those signs correctly. The problem is that lots of softwares don't look at the font content, and work on their own. The result is that the dot is not removed on many system (including JSesh on the Mac). The positionning of the accent in front of the capital "I" is another problem.

With a correct configuration, it's possible to get good results with OpenOffice and Word.


The two possibilities for yod are

- U+0313 As i + "comma above" is already used in other languages, its chances to be correctly supported are better. The only problem is that in the normal display of this combination for capital "I", the accent is supposed to be above the I. As you know, the correct display for capital yod has the accent in front of the "I". If you can live with that, this solution is the safest one. It gives good results in most cases (but not with Java and Mac OS X, so JSesh display on the Mac is not correct).

- U+0486 this accent has the interesting feature of not being used for anything else on latin letters. So a font is free to place it in front of capital "I". In theory, this is the good solution. In practice, it works with some, but not all, softwares. OpenOffice gives good results, and the plain TextEdit software on the Mac too. I could succeed with Word on the Mac by enabling all ligatures.

JSesh doesn't support the current IFAO/Unicode system. This standard was a temporary "patch" using available unicode signs, done when no encoding was available for Egyptian transliteration.
Now that "Aleph" and "Ayin" have code, I want to encourage (well, enforce) their use.

### References

* [Wikipedia article on transliteration and unicode](http://en.wikipedia.org/wiki/Transliteration_of_Ancient_Egyptian)


---
title: Fonts modifications
date: 2025/10/17
author: Serge Rosmorduc
taxonomy:
    category: docs
    tag: []
---

## The Problem of Font Modifications

Almost each version of JSesh brings changes in the fonts. In many cases, I add new signs, which will probably not bother most users. I try to document those signs, so look, in the sign palette, to the `Sign Description` part.

However, I will also modify some existing signs. It might be for scientific reasons, if the sign was plainly wrong, or if I wanted to be closer to the *Hieroglyphica* and fix a detail or two. You will find many examples in the release of [JSesh 7.9](https://jsesh.qenherkhopeshef.org/signdiffs/release-7.9) which followed [remarks](https://jsesh.qenherkhopeshef.org/news/news20250609a) sent to me by Dr. Peter Dils. It contains minor changes, such as a slight modification in the writing implement displayed by sign B8G <span class='mdc'>B8G</span>, and more serious changes such as the crown of sign A302A <span class='mdc'>A302A</span>.

I may also modify a sign for purely aesthetic reasons. For instance, I have reduced the width of the lines of the H8 <span class='mdc'>H8</span> sign, which stood out way too much. I also **intend** to change the sign <span class='mdc'>G37</span> one day. The current version is perfectly valid and sourced; I drew it from a glyph in Karnak hypostyle hall; but it doesn't fit with the more detailled style of the signs drawn by Monsieur Serge THOMAS.

The problem is that most users copy/paste JSesh graphics in their documents. If you are in the middle of the redaction of an article, a book, or a Phd, and you change your JSesh version, you might end up with parts of your document using the old version of the font, and other parts using the new font, which might be disturbing. The reader might even wonder if the differences have been encoded on purpose. What can you do?

## The solution(s)

### Do (almost) nothing 

The first solutions are very simple:

- the first possibility is **not to update JSesh**. It's simple, and follows the rule, *if it ain't broken, don't fix it.*
- the second solution is to keep both versions of JSesh. I have decided to use a different folder for each installation of JSesh. That way, you can have a full collection of JSesh versions if you will.

### Manage it at the font level

As you know, you can have a [custom folder for your own hieroglyphs](/extending_sign_list/importingglyphs). You can simply get the signs from JSesh version A, and copy them in a folder to use them in JSesh version B.

There are two ways to do this. 

#### Catalogue approach

The web site of JSesh now provides a section listing [sign differences across JSesh versions](https://jsesh.qenherkhopeshef.org/signdiffs).

Each page in this section is dedicated to an update of JSesh from version *n-1* to version *n* (well, the version numbers are not that simple, but it's from one release to the next).

On the top of the page, you get two links:

- All relevant signs in release-*(n-1)*
- All relevant signs in release-*n*

Each link will allow you to retrieve a ZIP file containing the signs specific to the corresponding release. You can unzip it, and copy its content to your glyph folder. 

It's usable to go from version *n* to version *n-1* (or vice versa).

There is also a list of the modifications at the *glyph* level, with possibly an explanation, and the possibility to retrieve the glyph. Each drawing is a link which leads to the SVG file of the glyph.

#### Technical approach

You need to install both version of JSesh first. Then, in the “old” version, you look for a file called `jseshGlyphs-(VERSION NUMBER).jar`. It contains the glyphs of this version of JSesh. Copy it, rename it to `jseshGlyphs-(VERSION NUMBER).zip`, and **unzip** it. You will find the glyphs there as SVG files in a folder. Simply  select this folder as your personnal glyph folder, and, *voilà*, you are back to this version of JSesh as far as fonts are concerned.


## Are new Signs a Problem?

At first sight, a font with a new sign is not a problem... however, it's not that simple, in particular if you deal with **text databases**.

For instance, looking at palaeographies, I saw that in most cases, the E1 sign, when it means *cattle* *ꞽḥ.w, mnmn.t...* has lyra-shaped horns. It's rather well documented. Gardiner choosed to have a more generic E1 sign, which can also be used for bull, *kꜣ*.

In a modification of JSesh 7.9, I intend to propose:

- ![](./E1.png?classes=inline) the “old” version of the sign, which corresponds to the Gardiner shape (perhaps with slighly shorter horns);
- ![](./E1x.png?classes=inline) the version with lyra-shaped horns, more usual in offering lists.


The problem of adding a new variant of a sign is the following: texts which have been already encoded, and whose original **might** feature the new variant, use the old code. It doesn't make them unreadable, or incorrect in isolation, but it you want to compute statistics, for instance, you won't find all `*real*` occurrences of your sign.

This being said, I'm afraid that creating a large database of texts, accurate at the **sign** level, is almost impossible, because of the human factor. It will require an very strict encoding and proofreading discipline.

At the same time, I would like to be wrong there, and I dream of a system which could tell you when a particular variant of a sign is attested.



---
title: Tips and tricks on hieroglyphic text encoding
taxonomy:
    category: docs
---


Before describing the manuel de codage itself, I'd like to make a point or two about how one should encode a hieroglyphic text.

Typically, you have a source, which might be a) a printed source, with typeset hieroglyphs, b) a photograph or an acurate facsimile of the original text, or c) handwritten hieroglyph from an egyptological publication (for instance, the Urkunden).

You must decide how faithfull to the original you must be, and it's not a simple question. The first point is that you can be sure that **your Manuel de Codage text can't be a facsimile,** so, one way or another, it will betray the original. If the text is ultimately a hieratic text, you are already creating something completely different anyway.

Now, when you have a sign, should you look for the most precise variant for it, or use a somehow standardised one? To answer this, you should wonder if this variant is relevant, in the text, and in the use you intend to make of it. For instance, in the Kanaïs texts by Sethi the Ist, the first person pronoun uses many variants of A40 <span class='mdc'>A40</span>. If you intend the text to be for grammatical study, it's not very relevant. If you wonder whether it's a free play to add diversity to the text, then you may take the time to encode the variants.

As a rule, **if you are a beginner in Egyptian,** I'd advise you to encode the "standard" sign, as it will force you to **read the text, not to copy signs**. The problem you have when you want to be very accurate is that you will find many cases of variants which have no encoding anyway, and you take the chances to mislead your readers by giving a false impression of accuracy... and often, to chose an irrelevant sign which simply happens to look like the one you want.

When your source is an handwritten version of a text, like in the Urkunden, beware of one point: unless a sign is very particular, an egyptologist will usually draw his glyphs in the easiest way. That means, for instance, he will use V23A (<span class='mdc'>V23A</span>) instead of  V22 (<span class='mdc'>V22</span>) which is the normal hieroglyphic sign. You must understand that, and when a sign selection is simply caused by the individual hand of the author, render it with the "standard" sign. On the other hand, when the author has drawn a very specific sign form, it might be worthwhile to give it more consideration.

## Encoding hieratic texts


The above rule is even stronger for hieratic texts. There is no point in making a distinction between <span class='mdc'>V23A</span> and  <span class='mdc'>V22</span>, as both are rendered the same in hieratic!

Now, there are a number of peculiarities of hieratic which deserve more care. Those have been pinpointed by sir Alan Gardiner in his article [“The Transcription of New Kingdom Hieratic”, *JEA* 15 (1929), p. 48-55](https://www.jstor.org/stable/3854012). The rendering of hieratic texts should hint at the way the original signs are placed, in order to allow the reader to understand the reason for the rendering, and to go back to the original when necessary.

JSesh includes a number of signs which are usefull for rendering hieratic texts:

| Sign                           | Code  | Use                                                                                                                                                                                                             |
| ------------------------------ | ----- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <span class='mdc'>Ff1</span>   | Ff1   | a sign particular to Ramesside texts, which serves as a kind of "wildcard". this is different from sign Z5 (<span class='mdc'>Z5</span>). You can get it in JSesh by typing "," (comma) and then the space key. |
| <span class='mdc'>Ff100</span> | Ff100 | a non-standard sign, **dot space filler**. Use it to render the various dots a scribe may use, when they are not a ponctuation.                                                                                 |
| <span class='mdc'>Ff101</span> | Ff101 | a non standard sign, **horizontal space filler**. Use it to render various meaningless horizontal sign the scribe may use to fill voids.                                                                        |

JSesh includes also specific signs for numbers in hieratic texts. In those texts, the "determinative" Z1 is often smaller than the "digit" Z1. Careless rendering might cause <span class='mdc'>h:r-W:ra-Z1-Z1-Z1</span> to be read hrw 3 whereas the original has <span class='mdc'>h:r-W:ra-Z1-Ff302</span>, which is clearly hrw 2.

## Sign layout

Use the various "ligature" capabilities of JSesh, and **if everything else fails,** go for the "group editor". Also, don't lose your time trying to get the exact same sign sizes and proportions as the original, unless you intend to discuss them.

A few interesting points:

In the group "M17-M17", the signs should often be closer than the standard spacing of JSesh allows (actually, this is already stated by sir A. Gardiner in the catalogue of his fonts). If one writes `i*i:k` (that is, two yod grouped horizontally, and a "k" below them), the group JSesh creates is ![](pAyk2.png?classes=inline). To obtain the better layout: ![](pAyk1.png?classes=inline) is simple: you only need to ligature the two yods (type "i" "&" "i", for instance).
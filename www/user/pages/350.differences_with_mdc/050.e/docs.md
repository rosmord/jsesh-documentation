---
title: E: Mammals
taxonomy:
    category: docs
    tag: []
---

- <span class='mdc'>E31</span> JSesh uses the original Gardiner shape and description. The goat is wearing a seal, not an *ꜥnḫ* sign (which is the shape chosen in the Hieroglyphica).
- <span class='mdc'>E31B</span> is the original Hieroglyphica font shape, with an *ꜥnḫ* sign instead of a sceal.
- <span class='mdc'>E187</span> is kept for Hieroglyphica compatibility, but is in fact a “phantom” for E31.
- JSesh has a code US1E31VARA <span class='mdc'>US1E31VARA</span> which was added quite early, but which corresponds to Hieroglyphica E186 <span class='mdc'>E186</span>. I'd suggest using E186 instead.


About fonts evolutions: the current fonts don't clearly differentiate between the actual shapes of glyphs and more general versions (termed *classes* and *signs) in the [Thot Sign List](https://thotsignlist.org/About). I suppose that the history of <span class='mdc'>E31</span> in the Hieroglyphica is the following: 

- first, the original Winglyph, which was mostly limited to the Gardiner font, used the shape  <span class='mdc'>E31B</span> for E31. It wasn't a problem. The sign was the only one available for E31 and variants, which means that using it did not suppose this particular variant of the sign was meant to be in the original text. 
- when extending the library, the need arose to differentiate  <span class='mdc'>E31B</span> and <span class='mdc'>E31</span>, leading to the addition of E187
- the problem is that everyone encoding texts before that, or limiting himself to the Gardiner set, was using the code E31.

This situation can be a bit problematic with text databases. It's also struturally anavoidable if we don't have the distinction between various level of encoding.


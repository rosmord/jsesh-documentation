---
title: Keyboard Editing
taxonomy:
    category: docs
---

## Typing Hieroglyphs

To input hieroglyphic signs using the keyboard, click within the main window (the one displaying the actual hieroglyphic text, not the "Manuel de Codage" field).

When you type a letter or number in the main window, it appears in the small panel located in the bottom left corner of JSesh. This panel allows you to enter “Manuel de Codage”  codes efficiently.


* Lots of signs have phonetic codes, which correspond to their translitteration;
* all signs are accessible through their code in Gardiner's grammar. To find the code, you can push at the "Basic Hieroglyphs" button or look at the hieroglyphic palette.

Once the code is typed, you must validate it. To validate, type one of `space`, '`:`', '`*`', '`-`', `enter`.

The sign will be added to the hieroglyphic text.

Phonetic codes can correspond to more than one sign. For instance, iw corresponds to one of <span class="mdc">N18</span>,  <span class="mdc">D54</span>, <span class="mdc">E9</span>,  <span class="mdc">E14</span> and <span class="mdc">F51</span>.The “official”  sign for iw is <span class="mdc">iw</span>, according to the *manuel* (a relatively weird choice, as <span class="mdc">D54</span> seems more frequent). However, you might want another sign. In this case, it's quite simple : press the **space bar**, and the system will circle through the possibilities, one at a time.

Your last choice will be retained the next time you type the code in this session.

### Phonetic codes

The uniliteral signs have the following codes, which are also used when typing transliteration:

| Code | Letter    |
| ---- | --------- |
| A    | ꜣ (aleph) |
| i    | ꞽ (yod)   |
| y    | y         |
| a    | ꜥ (ayin)  |
| w    | w         |
| b    | b         |
| p    | p         |
| f    | f         |
| m    | m         |
| n    | n         |
| r    | r         |
| l    | l         |
| h    | h         |
| H    | ḥ         |
| x    | ḫ         |
| X    | ẖ         |
| z    | z         |
| s    | s         |
| S    | s         |
| q    | ḳ         |
| k    | k         |
| g    | g         |
| t    | t         |
| T    | ṯ         |
| d    | d         |
| D    | ḏ         |

W is also used for Z7, M for Aa15, and N for S3.

## Grouping signs


The sign you type when validating can be used to group the hieroglyphs. Both 'space' and '`-`'' have the simple effect that the next sign will be added in a new cadrat.

* '`:`' and '`*`' will add the next sign respectively below and besides the last sign entered.
* 'enter' has two consequences : it validates a sign (if there is one), and it adds a new line.

If no code has been entered (that is, if the code window is entered), the previous grouping sign type will group the last two cadrats. It looks a bit strange, but you will see that it's quite natural. you can use it to group signs as an afterthough. Actually, it was a behaviour I unexpectly got when writing TkSesh, and that I have kept, as I found it useful.

### *Exempli gratia*


If you want to type the word <span class="mdc">p*t:pt</span>, you can :

* type 'p', then '`*`', 't', '`:`', 'pt'
* type 'p', 't', then '`*`', `space` (which kind of validates the '`*`'), pt, '`:`', and `space`.

---
title: Advanced Informations in Inkscape
taxonomy:
    category: docs
    tag: []
---

## Introduction
 
JSesh has now a relatively advanced ligature mechanism, which is not as good as the one in RES, but give reasonnable results in most cases. In many cases, JSesh is able to "guess" where ligatured groups should fit, but it can also do with some extra help. This help can be provided in the sign's SVG file itself, and we decided to use the mechanisms of inkscape for that.

## Ligature zones

For each sign, JSesh will try to compute two ligature zones, one for ligatures of groups before the sign, the other for ligatures of groups after the sign. **Those zones can be computed automatically,** but the sign author can also provide them.

![The A17 sign with its two ligature zones](zones1.png?classes=caption "The A17 sign with its two ligature zones")


to create one of the two ligature zones in inkscape, do the following:

- create a rectangle where the group should fit. Note that the whole group will be scaled to fit there, so draw it large enough. I usually draw these rectangles in red, but it's only a convention.
- open the contextual menu for the rectangle (right-click over the rectangle), and select object properties . You will get the object properties window ( Figure “Zone Properties” below.) Define the Id as either "zone1" or "zone2". Don't forget to click on the Define button to validate your modification. Also clear the label (more on this in the section called “Ligature zones gravity” ).

Admitedly, we are using the id and label information in a way they are not supposed to be used. The reason for this is purely pragmatic. It's far easier to do things that way, as the sign creator has no need to know about the inner organization of the XML format.

![](./zoneProperties.png?classes=caption "Zone Properties")

## Ligature zones gravity

The ligatured group will go somewhere in the ligature zone. But where exactly ? It can stand in the middle of the area, or stick to one of its sides. In fact, the behaviour of the layout algorithm is not always the same. In ![𓅱 and 𓏏 ligatured](./w_and_t.png?classes=inline), the "t" tends to fit on the bottom left of the rectangular area. In ![](./Hm_kA.png?classes=inline), the U36 <span class="mdc">U36</span> sign is more or less centered, both horizontally and vertically. JSesh allows signs authors to design the behaviour of "ligature zones", in the following way. Remember the label of the previous paragraph? You can set it to 

~~~
gravity:gravity specifications.
~~~

where gravity specifications can contain

* `s` or `e` to ask the group to stick to the **start** side or to the **end** side of the zone[^1]. If neither `s` nor `e` is specified, the group will be horizontally centered.
* `t` or `b` to ask the group to stick to the top or bottom of the zone. If neither "t" nor "b" is specified, the group will be vertically centered.

“Zone Properties”, ''gravity:te'' means that the group which would be ligatured in zone1 (in front of the "child" sign) would stick to the top of the red rectangle, and stay near the sign, for instance ![](./W_Xrd.png?classes=inline).

[^1]: `start` and `end` are taken from M.-J. Nederhof's RES, and avoid the use of “left” and “right” , which are not really usable for hieroglyphs.

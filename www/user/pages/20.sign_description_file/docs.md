---
title: Appendix B: the sign description file
taxonomy:
    category: docs
    tag: []
---
====== Appendix B: Technical information on the sign description file ======

Beware: technically explicit content. Pure souls, avert your eyes. A more user friendly system has been created.

Alternatively, you may directly edit your file description file. You need some kind of simple editor to do this : The notepad might do on windows, and softwares like TextWrangler can be used on Mac OS X. XML files are made of plain text.

JSesh won't accept badly formed files, so you may find yourself unable to launch JSesh. If this is the case, either correct signs_definition.xml, or rename it to something else, so that it will be ignored. In the future, I will add a user friendly editor, but I won't do it until the format is completely defined.
The file must have the following form:
<code>
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE signs PUBLIC "-//ORG/QENHERKHOPESHEF//DTD SIGNDESCRIPTION 1.0" "sign_description.dtd">
<signs>

<!-- here your signs definitions -->

</signs>
</code>

It is important to have exactly this content, specially the DOCTYPE line.

Here is a small example (actually, a part of JSesh standard sign description file). This file describes signs C1 and C1A. You see that they are classified in a number of categories. They are both human-headed deities and seated characters. The translitteration of C1 is given. We have provided one for C1A as well. The code ''"relevance='1'"'' means that this translitteration is here only for informationnal purposes. Actually, the XML format has been prepared to accomodate a lot of different data, which is not really used yet by JSesh, and I am very interested in getting suggestions about it. The definition for the format (its "dtd") is given just after this appendix.
<code>
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE signs PUBLIC "-//ORG/QENHERKHOPESHEF//DTD SIGNDESCRIPTION 1.0" "sign_description.dtd">
<signs>

<!-- As C is the most complete part of JSesh fonts now, we try to cover it fully. -->

<tagCategory tag="human-headed deity" label="human-headed deity"/>
<tagCategory tag="hawk-headed deity" label="hawk-headed deity"/>
<tagCategory tag="ibis-headed deity" label="ibis-headed deity"/>
<tagCategory tag="ram-headed deity" label="ram-headed deity"/>

<sign sign="C1">
 <hasTranslitteration sign="C1" translitteration="ra"/>
 <hasTag tag="human-headed deity"/>
 <hasTag tag="seated"/>
 <contains partCode="N6"/>
</sign>

<sign sign="C1A">
 <similarTo baseSign="C1"/>
 <hasTranslitteration translitteration="ra" relevance="1"/>
 <hasTag tag="human-headed deity"/>
 <hasTag tag="seated"/>
 <contains partCode="N6"/>
 <contains partCode="S40"/>
</sign>
</signs>
</code>
Note that tags must be defined before they are used (as tagCategory). A tag has a name and a label ; it is indeed possible to define labels in multiple languages, although this is not really used by JSesh now.

===== Sign description DTD =====

For the more technically-oriented, here is the current DTD used for sign descriptions. It is still experimental, and has already changed since version 2.4.13.

<code>
<!-- DTD used to describe signs characteristics. -->
<!-- CATALOG NAME : "-//ORG/QENHERKHOPESHEF//DTD SIGNDESCRIPTION 1.0" --> 

<!ENTITY % signInfo "variantOf|hasTransliteration|partOf|contains|signDescription|isDeterminative|hasTag|phantom"
>

<!ELEMENT signs (sign|determinativeCategory|tagCategory|tagLabel|%signInfo;)*>

<!-- The sign element is optional, but allows to have a better structured file. -->

<!ELEMENT sign (%signInfo;)* >

<!ATTLIST sign
    sign CDATA #REQUIRED
 alwaysDisplay (y|n) 'n'
>

<!--
 The notion of variant used here is somehow ad-hoc.
 The problem of variants is that there are two different notions behind it, both useful in our software.
 The first notion is LINGUISTIC variant. A sign is a linguistic variant of another one if it has the same uses.
 For instance, Y2 is a linguistic variant of Y1. Now, Y2 also "looks like" Y1. We will call it a "graphical variation".
 Both notions are independant, though statistically linked. For instance, Z7 is a linguistic variant of G43, but not a 
 graphical variation thereof.

 the notion of "looking like" another sign is covered by the "isSimilar" attribute.

 In lots of cases, especially for determinatives, the signs are not always fully substitutable one for another.
 To allow the use of 'variant' information in searches, we introduce the "linguistic" attribute.

 let B be a variant of A.
 "full" means that all uses of B are also possible uses of A, and all uses of A are uses of B.
 "other" means that B is more specific than A, or that the degree is unknown
 "partial" means that the uses of A and B intersect, but they have also both significantly different uses.
  For instance, the D36 sign (ayin) is a partial variant of D37 (di), as D36 can write "di". However,
  in this case, I would not consider D37 as a variant of D36, because it would cause more harm than good.
 "no" is used when the sign is not at all a linguistic variant. In this case, isSimilar is normally "y".

-->

<!ELEMENT variantOf EMPTY>
<!ATTLIST variantOf
 sign CDATA #IMPLIED
 baseSign CDATA #REQUIRED
 isSimilar (y|n) 'y'
 linguistic (full|partial|other|no|unspecified)  'unspecified'
>



<!ELEMENT hasTransliteration EMPTY>
<!-- the main purporse of transliteration is helping someone to find a sign. -->
<!-- a few more information help here -->
<!--
    the "use" attribute explain where the transliteration will be visible in JSesh.
 'keyboard' means the sign is typical of this transliteration, i.e. it should be used 
 in the main software when using "space" to circle among possible signs.
 'palette' means the sign is a not-too-unusual value for a given transliteration.
 it should be accessible through the palette.
 'informative' means the value is here for informative purposes only.

 type allows one to specify whence the value comes. It might be that a sign is a real
 phonogram (e.g. G1 for aleph), or an ideogram, or abbreviation, or simply be typical of certain words (e.g. "bin" is not 
 really a value for G37 ; but it's typical. G37 however is a known abbreviation for Sri.
-->

<!ATTLIST hasTransliteration
 sign CDATA #IMPLIED
 transliteration CDATA #REQUIRED
 use (keyboard|palette|informative) 'keyboard'
 type (phonogram|ideogram|abbreviation|typical) 'phonogram'
>

<!ELEMENT hasShape EMPTY>
<!ATTLIST hasShape
 sign CDATA #IMPLIED
 shape (tallNarrow|lowBroad|lowNarrow) #REQUIRED
 order CDATA #IMPLIED
>

<!ELEMENT partOf EMPTY>
<!ATTLIST partOf
 sign CDATA #IMPLIED
 baseSign CDATA #REQUIRED
>

<!-- Easier to use (and to declare) than isPartOf -->

<!ELEMENT contains EMPTY>
<!ATTLIST contains
 sign CDATA #IMPLIED
 partCode CDATA #REQUIRED
>


<!ELEMENT determinativeCategory EMPTY>
<!ATTLIST determinativeCategory
 category CDATA #REQUIRED
 lang NMTOKEN 'en'
 label CDATA #REQUIRED
>

<!ELEMENT isDeterminative EMPTY>
<!ATTLIST isDeterminative
 sign CDATA #IMPLIED
 category CDATA #REQUIRED
>

<!ELEMENT hasTag EMPTY>
<!ATTLIST hasTag
 sign CDATA #IMPLIED
 tag CDATA #REQUIRED
>

<!-- Declares a tag (without any label) -->
<!ELEMENT tagCategory (tagLabel)*>
<!ATTLIST tagCategory
 tag CDATA #REQUIRED
>

<!-- Declares a label for a tag. -->
<!ELEMENT tagLabel EMPTY>
<!ATTLIST tagLabel
 tag CDATA #IMPLIED
 lang NMTOKEN 'en'
 label CDATA #REQUIRED
>

<!-- sign description, in manuel de codage format. 
  - lang can be used to describe the language. User "fr" for french, "de" for german...
-->
<!ELEMENT signDescription (#PCDATA)>
<!ATTLIST signDescription
 sign CDATA #IMPLIED
 lang CDATA 'en'
>

<!-- A phantom is a redundant code. It states that a given code is the exact equivalent of another one.
     This can be used for normalization purposes. For instance, There are a few signs which have different encodings 
     in winglyph, JSesh, and Inscribe. The use of phantom a) avoids having multiple signs
     and b) allows to create a normalized text.
-->

<!ELEMENT phantom EMPTY>
<!ATTLIST phantom
 baseSign CDATA #REQUIRED
 existsIn CDATA 'jsesh'
>
</code>
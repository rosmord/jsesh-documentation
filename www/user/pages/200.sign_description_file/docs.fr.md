---
title: "Annexe B : le fichier de description des signes"
taxonomy:
    category: docs
    tag: []
---

Attention : contenu techniquement explicite. Âmes pures, détournez les yeux. Un système plus convivial a été créé.

Alternativement, vous pouvez éditer directement votre fichier de description des signes. Vous n'avez besoin que d'un éditeur simple pour cela : le Bloc-notes peut faire l'affaire sous Windows, et des logiciels comme TextWrangler peuvent être utilisés sous Mac OS X. Les fichiers XML sont constitués de texte brut.

JSesh n'acceptera pas les fichiers mal formés, vous risquez donc de ne pas pouvoir lancer JSesh. Si c'est le cas, corrigez le fichier `signs_definition.xml` ou renommez-le en quelque chose d'autre, afin qu'il soit ignoré. À l'avenir, j'ajouterai un éditeur convivial, mais je ne le ferai pas tant que le format ne sera pas complètement défini.
Le fichier doit avoir la forme suivante :

~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE signs PUBLIC "-//ORG/QENHERKHOPESHEF//DTD SIGNDESCRIPTION 1.0" "sign_description.dtd">
<signs>

<!-- here your signs definitions -->

</signs>
~~~

Il est important d'avoir exactement ce contenu, en particulier la ligne DOCTYPE.

Voici un petit exemple (en fait, une partie du fichier de description des signes standard de JSesh). Ce fichier décrit les signes C1 et C1A. Vous voyez qu'ils sont classés dans un certain nombre de catégories : ce sont à la fois des personnages à tête humaine et des personnages assis. La translittération de C1 est donnée ; l'attribut `use="keyboard"` signifie que cette translittération peut servir à saisir le signe (les attributs `use` et `type` sont décrits dans l'annexe précédente). C1A est déclaré comme une variante graphique de C1, dont il partage les tags et les parties. En fait, le format XML a été préparé pour accueillir beaucoup de données différentes, qui ne sont pas encore vraiment utilisées par JSesh, et je suis très intéressé de recevoir des suggestions à ce sujet. La définition du format (sa « DTD ») est donnée juste après cette annexe.

~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE signs PUBLIC "-//ORG/QENHERKHOPESHEF//DTD SIGNDESCRIPTION 1.0" "sign_description.dtd">
<signs>

<!-- As C is the most complete part of JSesh fonts now, we try to cover it fully. -->

<tagCategory tag="human-headed"/>
<tagCategory tag="seated"/>

<sign sign="C1">
 <hasTransliteration transliteration="ra" type="phonogram" use="keyboard"/>
 <hasTag tag="human-headed"/>
 <hasTag tag="seated"/>
 <contains partCode="N6"/>
 <contains partCode="A40"/>
</sign>

<sign sign="C1A">
 <variantOf baseSign="C1" isSimilar="y" linguistic="unspecified"/>
 <hasTag tag="human-headed"/>
 <hasTag tag="seated"/>
 <contains partCode="N6"/>
 <contains partCode="S40"/>
</sign>
</signs>
~~~

Notez que les balises doivent être définies avant d'être utilisées (comme `tagCategory`). Un tag a un nom et une étiquette ; il est en effet possible de définir des étiquettes dans plusieurs langues, bien que cela ne soit pas vraiment utilisé par JSesh à l'heure actuelle.

## DTD des descriptions de signes

Pour les plus techniciens, voici la DTD actuellement utilisée pour les descriptions de signes. Elle est encore expérimentale, et a déjà changé depuis la version 2.4.13.

~~~xml
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
        "unspecified" is used when the sign creator hasn't made a choice for yet.

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
~~~

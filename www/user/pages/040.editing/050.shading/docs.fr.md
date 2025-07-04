---
title: Ombrer/Hachurer un texte
author: Bertrand Gajeot, Didier Morandi
taxonomy:
    category: docs
    tag: []
---


Ombrer ou hachurer est actuellement un peu complexe. La mauvaise nouvelle, c'est ce que cela va empirer.

En tant qu'option (Fichier/Propriétés du document), l'ombrage peut être rendu soit par les classiques lignes entrecroisées que l'on peut voir dans les anciennes publications, soit par un fond gris clair. Bien que de nombreux utilisateurs préfèrent la première solution, plus traditionnelle, la seconde est meilleure sur un plan typographique.  Les lignes entrecroisées rendent difficile la lecture des signes, ce qui n'est pas le cas d'un fond gris clair.

L'ombrage se présente de nombreuses façons. Cela est dû à l'histoire du Manuel de Codage.

Un bon résumé est disponible dans le document de démonstration de JSesh (celu qui apparaît lorsque l'on lance JSesh, et qui est désormais inclus dans la bibliothèque de textes de JSesh).

Néanmoins, pour dire toute l'histoire :

* Originellement, il existait deux systèmes d'ombrage. Le premier ombrait une partie entière du texte : c'est celui que vous obtenez quand vous utilisez "Ombrer une zone". Dans JSesh, il fonctionne sur le **texte sélectionné**.
* Le second système d'ombrage utilisait des symboles d'ombrage, utilisés de la même façon que des hiéroglyphes. Dans le manuel originel, les cadrats étaient ombrés en les recouvrant avec les symboles d'ombrages correspondants. Vous pouvez les obtenir depuis le menu "Symboles d'ombrage". Ainsi, ![A hare above a shaded zone](./basic.png?classes=inline) peut être obtenu en saisissant "wn", puis en ajoutant un symbole d'ombrage, et en empilant les deux verticalement. JSesh comprend ce genre d'ombrage depuis le début, mais le menu pour l'utiliser n'est disponible que depuis la version 2.10.
* ensuite, aux alentours de 1994, un nouveau système d'ombrage fut proposé, qui couvrait des cas plus simples. C'st celui que l'on obtient avec le menu "Ombrage". Il s'applique au groupe en cours (celui devant le curseur), et peut être utilisé pour ombrer n'importe quel quartier d'un groupe.
* MacScribe est capable d'ombrer les quartiers de signes individuel. Sur MacScribe, `p##13*p:pt` montrerait le signe "p" à moitié ombré. Une variante de ce système est comprise par JSesh. Le logiciel externe [MacScribe converter](https://jsesh.qenherkhopeshef.org/software/MacScribeImporter.zip) comprend cela.
* Un système d'ombrage « libre »  serait agréable également. Dans ce cas, les limites de la zone d'ombrage serait librement tracée. Je prévois également de l'ajouter (en prenant appui sur l'éditeur de groupe). Mais pour le moment, si vous avez un tel besoin de précision, la seule option que JSesh vous donne est d'exporter votre fichier dans un format pratique (par exemple SVG) et de le modifier sous cette forme.

## Ombrer une partie de cadrat

Le menu Manipulation de texte/Ombrage peut s'appliquer à une sélection. En fait, vous pouvez ombrer la partie supérieure de tous les groupes d'une sélection (auparavant, il fallait ombrer chaque groupe un par un).

En outre, pour ceux qui saisissent des textes comportant de nombreuses lacunes, j'ai ajouté un menu popup, qui apparaît en appuyant sur la touche `#` du clavier. Vous pouvez y naviguer à l'aide cu clavier ou sélectionner des entrées par lettres spécifiques.

Voici un exemple : j'ai sélectionné une partie du texte et tapé `#`. Le menu contextuel apparaît.

![Partial shading popup](./popup.png?classes=caption "menu d'ombrage partiel")

Maintenant je peux sélectionner l'ombrage dont j'ai besoin de différentes façons (cela dépend de votre système d'exploitation). Par exemple, je peux taper "3", me déplacer dans le menu à l'aide des touches fléchées du clavier ou sélectionner l'option de menu avec la souris. Ensuite, le texte ainsi sélectionné est entièrement ombré :


![Partial shading applied](./shading2.png?classes=caption "Ombrage partiel appliqué")

## Options courantes pour réaliser des ombrages difficiles

Si vous souhaitez, par exemple, ajouter une zone d'ombrage au-dessus du milieu d'un signe, vous pouvez désormais le faire. En fait, c'est la raison pour laquelle j'ai ajouté un menu pour retrouver les "anciens" symboles d'ombrages.
Admettons que vous vouliez créer ![](./shading3.png?classes=inline). Vous devez d'abord saisir ces deux signes. L'ombrage est ajouté à travers les menus :

![Adding a shading symbol](./addSymbol.png?classes=caption "Ajout d'un symbole d'ombrage")


Ensuite, vous n'avez plus qu'à utiliser l'éditeur de groupe :

![Moving shading symbols with the group editor](./group.png?classes=caption "Déplacement des symboles d'ombrage avec l'éditeur de groupe")
}

Autant que possible, il faudrait saisir le symbole d'ombrage en premier, et ensuite le hiéroglyphe. Ainsi, si votre format de rendu final ne comprend pas la transparence, vous aurez quand même un rendu correct.

(Au passage, les marques ecdotiques comme `[ ... ]` sont considérées comme des hiéroglyphes. À ce titre, elles peuvent être déplacées à l'aide de l'éditeur de groupe).
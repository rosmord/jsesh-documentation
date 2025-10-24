---
title: Copy/Paste
taxonomy:
    category: docs
---

À partir de la version 5 et ultérieures, le copier-coller peut être utilisé pour transférer des données entre Jsesh et d'autres applications. On peut :

- Copier/coller entre différentes fenêtres dans JSesh lui-même.

- Copier du texte et des signes dans un traitement de texte (fonctionne avec OpenOffice et MS Word)

## Copier et coller : Configuration

Souvent, on a besoin de deux tailles de signes dans une application : une pour le texte principal et une plus petite pour les notes de bas de page. JSesh permet de conserver deux configurations pour le copier-coller. La taille actuelle peut être sélectionnée dans le menu Édition : choisissez simplement "copier : petite taille", "copier : grande taille" ou "copier : tel qu'à l'écran" (cette dernière doit être utilisée si vous voulez que le glyphe copié garde la même disposition que ceux d'origine).

### Choix du format

Un copier-coller fait intervenir deux logiciels : JSesh et votre traitement de texte (Word, OpenOffice, etc.)
Désormais, JSesh proposera un certain nombre de *formats* différents à votre traitement de texte, lui permettant de choisir celui qu'il préfère. Pour contrôler ce qui sera proposé par JSesh, vous pouvez utiliser la boîte de dialogue Choix du format (dans les préférences).

Je fais la plupart de mes tests avec **OpenOffice** et **LibreOffice**. Ils ne sont pas parfaits, mais ils ont tendance à traiter correctement les images et l'unicode, c'est pourquoi j'encourage fortement leur utilisation. Leurs fichiers ont tendance à être très portables d'un ordinateur à l'autre. Pas de problème de différentes versions du traitement de texte détectés.

![Boîte de dialogue Choix de format](formatChoice.img_assist_custom.png?classes=caption "Boîte de dialogue Choix de format")



RTF
: probablement le choix le plus polyvalent pour l'instant. Fonctionne (presque) partout et donne des résultats raisonnables, en particulier pour les hiéroglyphes mélangés avec du texte alphabétique. Autrefois problématique avec certaines versions de Word sur Mac, mais s'est récemment (en 2016) améliorée.

PDF
: actuellement le choix donnant le meilleur rendu. Pour autant que je sache, seul Mac OS X prend en charge le copier-coller de PDF, et peu de logiciels le comprennent. Par exemple, Word 2004 ne le fait pas. Word 2008 le fait, cependant. Textedit a la mauvaise idée d'accepter le copier-coller du PDF, mais de transformer le résultat en un bitmap.

bitmap
: donne un bitmap (actuellement) basse résolution, adapté aux pages web par exemple.

texte brut
: copiera l'encodage selon le *Manuel de Codage* dans le presse-papiers.

Pour des informations spécifiques à **votre** traitement de texte, consultez le chapitre  
[sur JSesh et les traitements de textes](https://jseshdoc.qenherkhopeshef.org/en/graphical_exports/word_processors)

### Réglages fins


Les paramètres pour "grande taille/petite taille/tel qu’à l’écran" peuvent être modifiés dans les préférences.

![](./cut_and_paste_preferences.png?classes=caption "Préférences pour le Couper/coller")


Les « Préférences d'exportation » vous permettent de choisir comment le texte hiéroglyphique sera collé dans les exportations RTF. Il y a trois options :

  - **comme une grande image** : L'ensemble du texte sélectionné sera collé dans votre traitement de texte comme une seule image. C'est parfait pour le texte en colonnes, par exemple, ou si vous souhaitez conserver la disposition graphique. Il semble également que la plupart des logiciels de traitement de texte préfèrent gérer de grandes images plutôt que de nombreuses petites.
  
  - **cadrats groupés** : Les cadrats hiéroglyphiques adjacents seront regroupés dans une seule image. Le texte résultant alternera texte normal et grandes images.
  
  - **une image par cadrat** : Le texte collé contiendra du texte normal et des images pour le texte hiéroglyphique. Mais alors, chaque cadrat sera rendu comme une seule image. C'est très bien pour la coupe de ligne et peut être intéressant si vous mélangez du texte et des hiéroglyphes.
  

Hauteur du cadrat
: modifie la taille du texte hiéroglyphique collé.
 
Format graphique
: permet de sélectionner le type de format pour l'exportation du graphique.

### Limitations du copier-coller


En raison de problèmes techniques, nous avons limité le copier-coller. Il n'est pas possible de coller des textes très longs dans un traitement de texte (vous pouvez plutôt "exporter au format RTF"). Nous allons essayer de l'améliorer, mais nous pensons que c'est une nuisance mineure, car on colle généralement de petites parties de textes hiéroglyphiques plutôt que l'ensemble d'un grand document (la limite est actuellement de 1000 cadrats).

N'hésitez pas à écrire à l'auteur à ce sujet (ou sur d'autres problèmes avec JSesh).

## Menu "Copier" avancé


Normalement, dans JSesh, vous choisissez le format que vous souhaitez copier/coller dans le menu des préférences. Mais dans certains cas, vous souhaiterez peut-être copier votre texte dans un format spécifique qui n'est pas celui que vous avez choisi. Au lieu de revenir aux préférences, vous pouvez utiliser le menu "Copier sous". Il vous permet de copier le texte sélectionné au format PDF, RTF ou Bitmap.

## Copier des hiéroglyphes *depuis* un traitement de texte


### Principes et problèmes

*Je suis désolé, cette partie est un peu technique. Si quelqu'un est capable d'écrire les mêmes explications de manière plus claire, ce serait une contribution bienvenue pour le site de JSesh.*

Sur Windows (et sur Mac OS antérieur à Mac OS X), il existe une fonctionnalité appelée "Object linking and embedding", qui est plus ou moins un copier-coller intelligent. Vous copiez/collez un document de votre éditeur hiéroglyphique dans Word, puis si vous double-cliquez sur l'image collée, cela ouvrira l'éditeur hiéroglyphique, afin que vous puissiez modifier le texte.

Ce n'est pas possible avec JSesh, car ce type d'action est très spécifique au système (si vous en avez vraiment besoin, je crois savoir qu'il est assez bien pris en charge par Inscribe). Cependant, à partir de la version 2.11, JSesh fournit une version simplifiée. Fondamentalement, l'astuce (également utilisée dans d'autres éditeurs de hiéroglyphes, comme MacScribe) est d'utiliser le champ de commentaire disponible dans certains formats d'image (comme PDF ou EMF), et de mettre le texte du manuel de codage dans ce champ de commentaire. Lorsque l'image est collée dans JSesh, on peut simplement extraire le code.

Bien sûr, c'est plus ou moins automatique. Mais j'avais besoin de l'expliquer, car cela dépend d'un certain nombre de facteurs :

  * le format de l'image doit prendre en charge les commentaires, et je dois écrire le code correspondant. Ceci est actuellement fait uniquement pour EMF et PDF.
  * le traitement de texte doit accepter l'image collée « telle quelle » , et ne pas la modifier. Les modifications suppriment généralement le commentaire. Par exemple, sur un Mac, vous pouvez coller une image PDF dans MS Word 2008. Mais Word transformera (je suppose) l'image dans son propre format et perdra le commentaire au cours du processus.

Toutes ces explications pour vous dire que ce système ne fonctionnera pas avec tous les traitements de texte... et surtout pas avec MS Word (en tout cas pas avec Word 2008 sur Mac). Désolé.

Maintenant, voyons les solutions possibles

### Les éditeurs Mellel, Nissus et le PDF

Si vous utilisez Mellel ou Nissus Writer (et si vous configurez votre option Copier-coller pour utiliser le format PDF), vous pourrez coller vos hiéroglyphes dans JSesh.

Sélectionnez simplement les hiéroglyphes dans votre traitement de texte (par exemple Mellel) et copiez-les...

![Copie depuis Melel](mellel_copy.png?classes=caption "Copie depuis Melel")



Ensuite, allez dans JSesh et sélectionnez Fichier/Importer/Importer à partir d'un PDF (copier/coller).


![Importation PDF](jsesh_pdf_import.png?classes=caption "Importation PDF")


Le résultat remplacera votre document JSesh actuel :
![Résultat de l'import PDF](jsesh_pdf_import_result.png?classes=caption "Résultat de l'import PDF")


### NeoOffice/OpenOffice/LibreOffice et texte RTF


Ce chapitre décrit les manipulations effectuées sur un Macintosh en utilisant NeoOffice comme traitement de texte. Il fonctionne également avec OpenOffice sur Windows et Linux (mais il semble échouer avec OpenOffice 3.1.1 sur Mac).

Si vous configurez votre option couper-coller pour utiliser le format RTF **et** si vous avez choisi **EMF** comme format d'image (voir ci-dessus), vous pourrez recoller vos hiéroglyphes dans JSesh.

Tout d'abord, vous devez sélectionner "EMF" comme format de copie à utiliser.

![Préférences de copie](cut_and_paste_preferences.png?classes=caption "Préférences de copie")


Le texte collé dans EMF dans NeoOffice peut ensuite être recollé dans JSesh :

![Copier du RTF](copy_rtf.png?classes=caption "Copier du RTF")

![Importation RTF](import_rtf.png?classes=caption "Importation RTF")

![Texte RTF importé](import_rtf_result.png?classes=caption "Texte RTF importé")


Cependant il y a un petit problème. Nous voulons que NeoOffice envoie du texte RTF (avec l'image intégrée). Cela ne se produira pas si vous sélectionnez directement l'image :

![Mauvaise sélection dans NeoOffice](bad_copy_attempt.png?classes=caption "Mauvaise sélection dans NeoOffice")


Notez que dans la "bonne" sélection, l'image est encadrée en noir.

La sélection directe d'une image entraînera un message d'erreur (inoffensif) :


![Message d'erreur de mauvaise sélection](bad_copy_attempt_result.png?classes=caption "Message d'erreur de mauvaise sélection")

Maintenant, la bonne façon de sélectionner l'image est de cliquer devant elle dans le texte et de la faire glisser avec la souris.

Alternativement (et de manière moins acrobatique), vous pouvez sélectionner l'image en déplaçant le curseur de texte devant elle, puis en appuyant sur "shift" et l'une des flèches du clavier (c'est beaucoup plus simple de le faire que de le décrire).

Notez que vous pouvez sélectionner plusieurs images :

![Copies multiples](multi_copy.png?classes=caption "Copies multiples")


Et vous obtiendrez une ligne par image dans JSesh :

![Importations multiples](multi_copy_result.png?classes=caption "Importations multiples")


Veuillez ** noter que cela ne fonctionne que si vos images ont été collées à partir de la version 2.11 ou plus de JSesh, et dans le bon format**.

### Autres

Je suis très intéressé de savoir si d'autres configurations fonctionnent.
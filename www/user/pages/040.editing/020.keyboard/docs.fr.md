---
title: Édition à l'aide du clavier
author: Bertrand Gajeot, Didier Morandi
taxonomy:
    category: docs
    tag: []
---


## Saisie des hiéroglyphes

Pour saisie des signes à l'aide du clavier, cliquer sur la fenêtre principale (celle qui affiche le texte hiéroglyphique en cours, et non celle avec le *Manuel de codage*).
Lorsque vous saisissez une lettre ou un nombre dans la fenêtre principale, cette lettre ou ce nombre apparaît dans le petit panneau en bas à gauche de l'écran de Jsesh. Ceci vous permet de saisie des codes *Manuel de codage*.

* De nombreux signes ont un code phonétique, qui correspond à leur translitération ;
* Tous les signes sont accessibles par leur code dans la fonte Gardiner. Pour connaître ce code, vous pouvez vous reporter au menu "Hiéroglyphes".

Une fois le code saisi, vous devez le valider. Pour ce faire, appuyez au choix sur la touche **Espace, ':', '*', '-' ou Entrée**.

Le signe sera ajouté au texte hiéroglyphique.

Les codes phonétiques peutvent correspondre à plus d'un signe. Par exemple, iw correspond à <span class="mdc">N18</span>,  <span class="mdc">D54</span>, <span class="mdc">E9</span>,  <span class="mdc">E14</span> et <span class="mdc">F51</span>. Le signe "officiel" pour iw est  <span class="mdc">iw</span> selon le manuel. Toutefois, vous pouvez désirez que ce soit un autre signe. Dans ce cas, c'est très simple : appuyez sur **Espace**, et le système fera défiler toutes les possibilités, une par une.

Votre dernier choix sera enregistré pour la prochaine fois que vous saisirez **le même code au cours de la même session.**

### Codes phonétiques

Les signes unilitères possèdent les codes suivants, qui sont également utilisés lorsque l'on saisit leur translitération :

| Code | Lettre    |
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

W est également utilisé pour Z7 <span class='mdc'>Z7</span>, M pour Aa15 <span class='mdc'>Aa15</span>, et N pour S3 <span class='mdc'>S3</span>.

## Signes groupés


Le signe que vous saisissez au mmoment d'une validation peut être utilisé pour grouper des hiéroglyphes. 'Espace' et '-' ont pour effet d'ajouter le signe suivant dans un nouveau cadrat.

* ':' et '*' ajouteront respectivement le signe suivant en dessous et à côté du dernier signe saisi.
* 'Entrée' a deux conséquences : cela valide un signe (s'il y en a un), et cela ajoute une nouvelle ligne.

Si aucun code n'a été entré (c'est-à-dire, si la fenêtre de code est utilisée), la saisie de groupement de signes précédentes groupera les deux derniers cadrats. Cela paraît un peu étrange, mais vous verrez que c'est assez naturel. Vous pouvez vous en servir pour grouper des signes après coup

### Exemple

Si vous voulez saisir le mot <span class="mdc">p*t:pt</span>, vous pouvez :
* saisir 'p', puis '*', 't', ':', 'pt'
* saisir 'p', 't', puis '*', ''Espace'' (ce qui, en quelque sorte, valide le '*'), pt, ':', et ''Espace''.

* saisir 'p', puis '`*`', 't', '`:`', 'pt'
* saisir 'p', 't', puis '`*`', `espace` (ce qui valide en quelque sorte le '`*`'), pt, '`:`', et `espace`.

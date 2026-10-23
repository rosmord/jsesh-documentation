---
title: 'Concepts de base'
taxonomy:
    category: docs
    tag: []
---

## Concepts de base

Le **Manuel de Codage (MdC)** est l'encodage textuel des hiéroglyphes égyptiens (par exemple `i-w-r:a-ra-m-p*t:pt`). JSesh lit, édite, affiche et écrit du MdC.

### Représenter un texte

Trois types représentent les textes hiéroglyphiques, par richesse croissante :

| Type | Ce que c'est | Paquetage |
|---|---|---|
| `HieroglyphicText` (anciennement `TopItemList`) | Le **texte hiéroglyphique** lui-même : un arbre de hiéroglyphes, cadrats, cartouches, sauts de ligne... C'est la représentation en mémoire d'un texte. | `jsesh.model` |
| `MDCDocument` | Un `HieroglyphicText` **plus** les métadonnées du fichier (chemin, encodage, dialecte, préférences). C'est ce que l'on charge et sauvegarde. | `jsesh.document` |
| `HieroglyphicTextModel` | Une enveloppe **vivante, observable et annulable** autour d'un `HieroglyphicText`, utilisée par l'éditeur. | `jsesh.document` |

Règle pratique :

- code par lots ou serveur qui ne fait que transformer du texte : `HieroglyphicText` ;
- chargement et sauvegarde de fichiers : `MDCDocument` ;
- tout ce qui est interactif (éditeur, annuler/refaire, notification des changements) : `HieroglyphicTextModel`.

### Rendu

Le rendu a besoin de deux contextes :

- un `JSeshRenderContext` : *avec quoi* dessiner (un style et un répertoire de polices/formes) ;
- un `JSeshTechRenderContext` : *où* dessiner (le `Graphics2D`, l'échelle du périphérique).

La classe `MDCDrawingFacade` cache les deux dans les cas courants. Voir [Rendu](/developpers_guide/jsesh_8/rendering).

### Ressources

Polices, base de signes et données de complétion sont regroupées dans un objet `HieroglyphResources`, que l'on construit avec `HieroglyphResourcesBuilder`. Voir [Ressources et polices](/developpers_guide/jsesh_8/resources_and_fonts).

## Objets immuables et « construction builders »

Dans les versions précédentes, certains objets (en particulier `DrawingSpecification`) étaient *modifiables*, ce qui posait problème quand ils étaient **partagés** entre composants (par exemple entre l'éditeur et l'éditeur de groupes). Il était difficile de savoir qui avait modifié quoi.

JSesh 8 favorise les **objets immuables**, comme il est de plus en plus courant en programmation objet. `JSeshStyle`, par exemple, est un record immuable. Quand vous avez besoin d'une version modifiée d'un objet immuable, vous en créez un nouveau. C'est ce qui se passe avec les chaînes Java :

~~~java
String example = "Hello";
String upper = example.toUpperCase(); // creates a new string, example is unchanged
~~~

Bien sûr, une *variable* peut toujours être modifiée pour désigner un autre objet :

~~~java
String example = "Hello";
example = example.toUpperCase();
~~~

Ici, `example`, qui désignait la chaîne `"Hello"`, désigne maintenant `"HELLO"` ; l'ancienne chaîne est inchangée.

![example désigne maintenant la nouvelle chaîne "HELLO" ; "hello" est inchangée](immutability.svg)

Pour les objets composites comme `JSeshStyle`, la façon de base d'obtenir une version modifiée est de créer une nouvelle instance :

~~~java
JSeshStyle style = JSeshStyle.DEFAULT;
// New painting specifications
PaintingSpecifications newPainting = ...;
// create a new style with a modified value
JSeshStyle newStyle = new JSeshStyle(
    style.geometry(),
    newPainting,
    style.fonts(),
    style.options());
~~~

Ce n'est pas très pratique, d'où l'utilisation de ce que Martin Fowler appelle un **construction builder**. `copy()` fournit un constructeur initialisé avec les valeurs actuelles ; vous modifiez ce qu'il faut, puis appelez `build()` :

~~~java
JSeshStyle style = JSeshStyle.DEFAULT.copy()
    .options(o -> o.textDirection(TextDirection.RIGHT_TO_LEFT)
                   .smallSignCentered(true))
    .geometry(g -> g.leftMargin(10)
                    .topMargin(10))
    .build();
~~~

Le partage est désormais explicite plutôt qu'implicite. Un `JSeshStyle` peut être utilisé sans risque à plusieurs endroits : remplacer une valeur dans l'un laisse les autres inchangés.

Si vous *voulez* que plusieurs composants partagent le même style et suivent ses changements (par exemple pour utiliser le même style dans tous vos éditeurs), utilisez une `JSeshStyleReference`.

---
title: 'Guide du développeur : JSesh 8'
taxonomy:
    category: docs
    tag: []
---

# Guide du développeur : JSesh 8

Si vous savez programmer en **Java,** vous pouvez utiliser **JSesh** comme *bibliothèque* dans vos propres programmes. JSesh 8 est une réécriture majeure des bibliothèques, et son API est beaucoup plus propre que celle de JSesh 7.

> **Attention :** JSesh 8 est encore jeune. L'API a beaucoup changé, et peut encore changer avant d'être figée. N'hésitez pas à l'essayer et à signaler problèmes et suggestions, mais attendez-vous à devoir mettre à jour le code que vous écrivez maintenant.

JSesh 8 nécessite **Java 25**, et se compile avec **Gradle**.

Ce guide est organisé autour de cas d'usage concrets ; la partie [How to](/developpers_guide/jsesh_8/howto) sera probablement la plus utile :

- [Obtenir le code](/developpers_guide/jsesh_8/getting_the_code) : récupérer et compiler les sources ;
- [Utiliser JSesh dans votre projet](/developpers_guide/jsesh_8/using_jsesh_in_your_project) : les dépendances Gradle (ou Maven) ;
- [Concepts de base](/developpers_guide/jsesh_8/core_concepts) : les classes principales et la manière dont JSesh 8 construit des objets immuables ;
- [Rendu](/developpers_guide/jsesh_8/rendering) : produire des bitmaps, du SVG, ou dessiner sur un `Graphics2D` ;
- [Analyse et documents](/developpers_guide/jsesh_8/parsing_and_documents) : lire, écrire et convertir des textes en Manuel de Codage ;
- [Composants Swing](/developpers_guide/jsesh_8/swing_components) : intégrer l'éditeur dans une interface Swing ;
- [Ressources et polices](/developpers_guide/jsesh_8/resources_and_fonts) : polices, base de signes et glossaire ;
- [Exports](/developpers_guide/jsesh_8/exporting) : PDF, SVG, RTF et autres formats ;
- [Référence rapide](/developpers_guide/jsesh_8/quick_reference) ;
- [How to](/developpers_guide/jsesh_8/howto) : petits exemples.

Si vous avez du code écrit pour JSesh 7, voyez [Passer de JSesh 7 à JSesh 8](/developpers_guide/jsesh_7_to_jsesh_8).

## Les démonstrations

Le projet [jsesh-demos](https://github.com/rosmord/jsesh-demos) contient de petits projets Gradle indépendants, prêts à l'emploi, qui montrent comment utiliser la bibliothèque. Je vous conseille vivement de les récupérer : la plupart du code de ce guide en provient.

| Démo | Montre comment |
|---|---|
| `bitmapDemo` | produire des images PNG |
| `svgExportDemo` | produire des fichiers SVG |
| `lowleveldrawing` | passer d'une chaîne Manuel de Codage à une image étape par étape |
| `gui` | construire des champs hiéroglyphiques Swing |
| `multipleSignSources` | utiliser des signes provenant de plusieurs dossiers |

Le [dépôt JSesh](https://github.com/rosmord/jsesh) contient aussi un dossier `00_Documents/documentation` avec la documentation du programmeur qui a servi à écrire ce guide ; elle peut être un peu en avance sur celui-ci.

---
title: 'Passer de JSesh 7 à JSesh 8'
taxonomy:
    category: docs
    tag: []
---

## Passer de JSesh 7 à JSesh 8

JSesh 8 est une réécriture majeure. La compatibilité de l'API avec le code ancien n'était pas un objectif : vous devrez donc mettre à jour le code qui utilise JSesh comme bibliothèque. Cette page liste les principaux changements. Le [guide JSesh 8](/developpers_guide/jsesh_8) décrit en détail la nouvelle API.

### Système de construction et prérequis

- JSesh se compile maintenant avec **Gradle** (`./gradlew build`) au lieu de Maven.
- JSesh 8 nécessite **Java 25**.
- Le groupId est `org.qenherkhopeshef.jsesh`. Les anciennes versions utilisaient `org.qenherkhopeshef` (voir le [guide JSesh 7](/developpers_guide/jsesh_7)).
- Les bibliothèques JSesh 8 s'installent dans votre dépôt Maven local avec `./gradlew publishToMavenLocal`. Les projets Gradle comme Maven peuvent les utiliser.

### Paquetages

Le code est maintenant organisé par domaine. Les classes utilisées dans les exemples de JSesh 7 ont bougé ainsi :

| JSesh 7 | JSesh 8 |
|---|---|
| `jsesh.mdcDisplayer.swing.editor` (`JMDCEditor`, `JMDCField`) | `jsesh.ui.editor` |
| `jsesh.mdcDisplayer.draw` (`MDCDrawingFacade`) | `jsesh.render.draw` |
| `jsesh.mdc` (`MDCSyntaxError`) | `jsesh.parser` |
| `TopItemList` (le modèle de texte) | `HieroglyphicText` (`jsesh.model`) |

Si un import ne compile pas, la [référence rapide](/developpers_guide/jsesh_8/quick_reference) donne l'emplacement actuel des principaux points d'entrée.

### Styles immuables

Les `DrawingSpecification` et `PageLayout`, modifiables, sont remplacés par le `JSeshStyle` immuable, que l'on modifie par un constructeur :

JSesh 7 :

~~~java
MDCDrawingFacade drawing = new MDCDrawingFacade();
drawing.setCadratHeight(60);
DrawingSpecification drawingSpecifications = new DrawingSpecificationsImplementation();
PageLayout pageLayout = new PageLayout();
pageLayout.setLeftMargin(5);
pageLayout.setTopMargin(5);
drawingSpecifications.setPageLayout(pageLayout);
drawing.setDrawingSpecifications(drawingSpecifications);
BufferedImage result = drawing.createImage(mdcText);
~~~

JSesh 8 :

~~~java
MDCDrawingFacade facade = MDCDrawingFacade.buildDefault();
facade.setCadratHeight(60);
JSeshStyle style = JSeshStyle.DEFAULT.copy()
    .geometry(g -> g.leftMargin(5).topMargin(5))
    .build();
facade.setStyle(style);
BufferedImage result = facade.createImage(mdcText);
~~~

Voir [Concepts de base](/developpers_guide/jsesh_8/core_concepts).

### Polices et ressources

Polices, base de signes et glossaire sont maintenant réunis dans un objet `HieroglyphResources`, construit avec `HieroglyphResourcesBuilder`. Des composants comme `JMDCEditor` et `JMDCField` les acceptent dans leurs constructeurs, ce qui permet de partager les polices. Voir [Ressources et polices](/developpers_guide/jsesh_8/resources_and_fonts).

### SVG et autres formats vectoriels

La sortie SVG nécessite la bibliothèque séparée `org.qenherkhopeshef:jvectclipboard` ; voir le `svgExportDemo`.

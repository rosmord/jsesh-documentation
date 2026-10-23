---
title: Moving from JSesh 7 to JSesh 8
taxonomy:
    category: docs
    tag: []
---

## Moving from JSesh 7 to JSesh 8

JSesh 8 is a major rewrite. API compatibility with older code was not a goal, so you will have to update the code which uses JSesh as a library. This page lists the main changes. The [JSesh 8 guide](/developpers_guide/jsesh_8) describes the new API in detail.

### Build system and requirements

- JSesh is now built with **Gradle** (`./gradlew build`) instead of Maven.
- JSesh 8 requires **Java 25**.
- The group id is `org.qenherkhopeshef.jsesh`. Older versions used `org.qenherkhopeshef` (see the [JSesh 7 guide](/developpers_guide/jsesh_7)).
- JSesh 8 libraries are installed in your local Maven repository with `./gradlew publishToMavenLocal`. Both Gradle and Maven projects can use them.

### Packages

The code is now organised by domain. The classes used in the JSesh 7 examples moved as follows:

| JSesh 7 | JSesh 8 |
|---|---|
| `jsesh.mdcDisplayer.swing.editor` (`JMDCEditor`, `JMDCField`) | `jsesh.ui.editor` |
| `jsesh.mdcDisplayer.draw` (`MDCDrawingFacade`) | `jsesh.render.draw` |
| `jsesh.mdc` (`MDCSyntaxError`) | `jsesh.parser` |
| `TopItemList` (the text model) | `HieroglyphicText` (`jsesh.model`) |

If an import doesn't compile, the [quick reference](/developpers_guide/jsesh_8/quick_reference) gives the current location of the main entry points.

### Immutable styles

The mutable `DrawingSpecification` and `PageLayout` are replaced by the immutable `JSeshStyle`, which you modify through a builder:

JSesh 7:

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

JSesh 8:

~~~java
MDCDrawingFacade facade = MDCDrawingFacade.buildDefault();
facade.setCadratHeight(60);
JSeshStyle style = JSeshStyle.DEFAULT.copy()
    .geometry(g -> g.leftMargin(5).topMargin(5))
    .build();
facade.setStyle(style);
BufferedImage result = facade.createImage(mdcText);
~~~

See [Core concepts](/developpers_guide/jsesh_8/core_concepts).

### Fonts and resources

Fonts, sign database and glossary are now gathered in a `HieroglyphResources` object, built with `HieroglyphResourcesBuilder`. Components such as `JMDCEditor` and `JMDCField` accept them in their constructors, so that fonts can be shared. See [Resources and fonts](/developpers_guide/jsesh_8/resources_and_fonts).

### SVG and other vector formats

SVG output needs the separate library `org.qenherkhopeshef:jvectclipboard`; see the `svgExportDemo`.

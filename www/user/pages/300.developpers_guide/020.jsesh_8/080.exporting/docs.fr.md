---
title: 'Exports'
taxonomy:
    category: docs
    tag: []
---

## Exporter en PDF, SVG, RTF, EMF...

Les exporteurs de formats se trouvent dans `jsesh.ui.export.*`. Chaque format a son paquetage ; ils partagent la mécanique de `jsesh.ui.export.generic` (`GraphicalExporter`, `AbstractGraphicalExporter`, `SelectionExporter`, `ExportData`).

| Format | Paquetage ou classe |
|---|---|
| PDF (iText) | `jsesh.ui.export.pdfExport.PDFExporter` |
| SVG | `jsesh.ui.export.svg.SVGExporter` |
| RTF (avec images intégrées) | `jsesh.ui.export.rtf` |
| EMF / WMF (métafichiers Windows) | `jsesh.ui.export.emf`, `jsesh.ui.export.wmf` |
| EPS | `jsesh.ui.export.eps` |
| PICT Mac | `jsesh.ui.export.macpict` |
| Bitmaps (PNG, JPEG) | `jsesh.ui.export.bitmaps` |
| HTML | `jsesh.ui.export.html` |

Ces classes mêlent le rendu et un peu d'interface utilisateur (panneaux d'options), et sont donc moins « pures » que la façade de dessin. Pour un **bitmap sans interface**, ou un SVG simple, vous voudrez presque toujours `MDCDrawingFacade` (voir [Rendu](/developpers_guide/jsesh_8/rendering)). Utilisez ces exporteurs quand vous avez besoin d'un format vectoriel ou de presse-papiers précis. Ils suivent la même chaîne `MDCView`/`ViewDrawer` que l'écran, et la sortie correspond donc à ce que montre l'éditeur.

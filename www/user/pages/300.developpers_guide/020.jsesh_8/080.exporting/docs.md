---
title: Exporting
taxonomy:
    category: docs
    tag: []
---

## Exporting to PDF, SVG, RTF, EMF...

Format exporters live in `jsesh.ui.export.*`. Each format has its own package; they share the machinery of `jsesh.ui.export.generic` (`GraphicalExporter`, `AbstractGraphicalExporter`, `SelectionExporter`, `ExportData`).

| Format | Package or class |
|---|---|
| PDF (iText) | `jsesh.ui.export.pdfExport.PDFExporter` |
| SVG | `jsesh.ui.export.svg.SVGExporter` |
| RTF (with embedded pictures) | `jsesh.ui.export.rtf` |
| EMF / WMF (Windows metafiles) | `jsesh.ui.export.emf`, `jsesh.ui.export.wmf` |
| EPS | `jsesh.ui.export.eps` |
| Mac PICT | `jsesh.ui.export.macpict` |
| Bitmaps (PNG, JPEG) | `jsesh.ui.export.bitmaps` |
| HTML | `jsesh.ui.export.html` |

These classes mix rendering with some user interface (option panels), so they are less "pure" than the drawing facade. For a **headless bitmap**, or a simple SVG, you almost always want `MDCDrawingFacade` instead (see [Rendering](/developpers_guide/jsesh_8/rendering)). Use these exporters when you need a specific vector or clipboard format. They walk the same `MDCView`/`ViewDrawer` pipeline as the screen, so the output matches what the editor shows.

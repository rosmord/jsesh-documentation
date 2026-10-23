---
title: Quick reference
taxonomy:
    category: docs
    tag: []
---

## Quick reference: key entry points

| I want to... | Use | Package |
|---|---|---|
| Parse MdC into a model | `MDCParserModelGenerator.parse` | `jsesh.mdcreader` |
| Parse MdC into a literal syntax tree | `MDCParser.parse` | `jsesh.parser` |
| Turn a model into MdC text | `MdCModelWriter.write` | `jsesh.io.mdc` |
| Draw hieroglyphs (image or `Graphics2D`) | `MDCDrawingFacade` | `jsesh.render.draw` |
| Load a `.gly` file | `MDCDocumentReader.loadFile` | `jsesh.io.document` |
| Save a document | `MDCDocumentWriter.write` | `jsesh.io.document` |
| Keep a text with its metadata | `MDCDocument` | `jsesh.document` |
| Have an editable, observable, undoable model | `HieroglyphicTextModel` | `jsesh.document` |
| Embed an interactive editor | `JMDCEditor`, `JMDCField` | `jsesh.ui.editor` |
| Query signs, variants, completion | `HieroglyphDatabase` | `jsesh.glyphs.signdata` |
| Convert hieroglyphs to Unicode | `MdCToUnicodeConverter` | `jsesh.model.unicode` |
| Build fonts, database and completion | `HieroglyphResourcesBuilder` | `jsesh.defaults` |
| Export to PDF, SVG, RTF, EMF... | `jsesh.ui.export.*` | `jsesh.ui.export` |
| Use the low-level rendering pipeline | `ViewBuilder` and `ViewDrawer` | `jsesh.render.view`, `jsesh.render.draw` |

Runnable examples are available in the [demos](https://github.com/rosmord/jsesh-demos), and in the `jseshTests` module of the JSesh sources.

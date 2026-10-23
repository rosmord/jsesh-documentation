---
title: 'Référence rapide'
taxonomy:
    category: docs
    tag: []
---

## Référence rapide : points d'entrée principaux

| Je veux... | Utiliser | Paquetage |
|---|---|---|
| Analyser du MdC en modèle | `MDCParserModelGenerator.parse` | `jsesh.mdcreader` |
| Analyser du MdC en arbre syntaxique littéral | `MDCParser.parse` | `jsesh.parser` |
| Transformer un modèle en texte MdC | `MdCModelWriter.write` | `jsesh.io.mdc` |
| Dessiner des hiéroglyphes (image ou `Graphics2D`) | `MDCDrawingFacade` | `jsesh.render.draw` |
| Charger un fichier `.gly` | `MDCDocumentReader.loadFile` | `jsesh.io.document` |
| Sauvegarder un document | `MDCDocumentWriter.write` | `jsesh.io.document` |
| Garder un texte avec ses métadonnées | `MDCDocument` | `jsesh.document` |
| Avoir un modèle éditable, observable, annulable | `HieroglyphicTextModel` | `jsesh.document` |
| Intégrer un éditeur interactif | `JMDCEditor`, `JMDCField` | `jsesh.ui.editor` |
| Interroger signes, variantes, complétion | `HieroglyphDatabase` | `jsesh.glyphs.signdata` |
| Convertir des hiéroglyphes en Unicode | `MdCToUnicodeConverter` | `jsesh.model.unicode` |
| Construire polices, base et complétion | `HieroglyphResourcesBuilder` | `jsesh.defaults` |
| Exporter en PDF, SVG, RTF, EMF... | `jsesh.ui.export.*` | `jsesh.ui.export` |
| Utiliser la chaîne de rendu bas niveau | `ViewBuilder` et `ViewDrawer` | `jsesh.render.view`, `jsesh.render.draw` |

Des exemples exécutables sont disponibles dans les [démos](https://github.com/rosmord/jsesh-demos), et dans le module `jseshTests` des sources de JSesh.

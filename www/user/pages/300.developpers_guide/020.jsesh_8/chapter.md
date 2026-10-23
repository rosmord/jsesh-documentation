---
title: 'Developer''s guide: JSesh 8'
taxonomy:
    category: docs
    tag: []
---

# Developer's guide: JSesh 8

If you know how to program in **Java,** you can use **JSesh** as a *library* for your own programs. JSesh 8 is a major rewrite of the libraries, and its API is much cleaner than the one of JSesh 7.

> **Warning:** JSesh 8 is still young. The API has changed a lot, and may change again before it is frozen. Please experiment with it and report problems and suggestions, but expect to update the code you write now.

JSesh 8 requires **Java 25**, and is built with **Gradle**.

This guide is organised around concrete use cases; the [How to](/developpers_guide/jsesh_8/howto) part will probably be the most useful:

- [Getting the code](/developpers_guide/jsesh_8/getting_the_code): getting and building the sources;
- [Using JSesh in your project](/developpers_guide/jsesh_8/using_jsesh_in_your_project): the Gradle (or Maven) dependencies;
- [Core concepts](/developpers_guide/jsesh_8/core_concepts): the main classes, and the way JSesh 8 builds immutable objects;
- [Rendering](/developpers_guide/jsesh_8/rendering): producing bitmaps, SVG, or drawing on a `Graphics2D`;
- [Parsing and documents](/developpers_guide/jsesh_8/parsing_and_documents): reading, writing and converting Manuel de Codage texts;
- [Swing components](/developpers_guide/jsesh_8/swing_components): embedding the editor in a Swing interface;
- [Resources and fonts](/developpers_guide/jsesh_8/resources_and_fonts): fonts, sign database and glossary;
- [Exporting](/developpers_guide/jsesh_8/exporting): PDF, SVG, RTF and other formats;
- [Quick reference](/developpers_guide/jsesh_8/quick_reference);
- [How to](/developpers_guide/jsesh_8/howto): short recipes.

If you already have code written for JSesh 7, see [Moving from JSesh 7 to JSesh 8](/developpers_guide/jsesh_7_to_jsesh_8).

## The demos

The [jsesh-demos](https://github.com/rosmord/jsesh-demos) project contains small, independent, ready-to-run Gradle projects showing how to use the library. I strongly recommend getting them: most of the code in this guide comes from them.

| Demo | Shows how to |
|---|---|
| `bitmapDemo` | produce PNG pictures |
| `svgExportDemo` | produce SVG files |
| `lowleveldrawing` | go from a Manuel de Codage string to a picture step by step |
| `gui` | build Swing hieroglyphic fields |
| `multipleSignSources` | use signs coming from several folders |

The [JSesh repository](https://github.com/rosmord/jsesh) also contains a folder, `00_Documents/documentation`, with the programmer's documentation used to write this guide. It may be a little ahead of this one.

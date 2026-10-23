---
title: Swing components
taxonomy:
    category: docs
    tag: []
---

## Embedding the editor in a Swing application

### The editor

`jsesh.ui.editor.JMDCEditor` is a ready-to-use Swing component. Put it in a `JScrollPane`:

~~~java
import jsesh.ui.editor.JMDCEditor;

JMDCEditor editor = new JMDCEditor();
frame.add(new JScrollPane(editor), BorderLayout.CENTER);

editor.setMDCText("i-mn:n-ra");        // load text (syntax errors are ignored)
String current = editor.getMDCText();  // read it back
~~~

Text direction and orientation are set on the editor:

~~~java
editor.setTextDirection(TextDirection.RIGHT_TO_LEFT);
editor.setTextOrientation(TextOrientation.HORIZONTAL);
~~~

The constructor `JMDCEditor(HieroglyphicTextModel, JSeshStyle, HieroglyphResources)` lets you share a model, apply a custom style, and supply your own fonts and signs (see [Resources and fonts](/developpers_guide/jsesh_8/resources_and_fonts)). There is also a variant taking a `JSeshStyleReference`, for editors which must follow a shared style.

Key collaborators (you rarely need them, but they are there for advanced control):

| Class | Role |
|---|---|
| `JMDCEditorWorkflow` | The editing **state machine**: `getMDCCode()`/`setMDCCode()`, caret, undo/redo, insertion. Get it with `editor.getWorkflow()`. |
| `HieroglyphicTextModel` | The observable and undoable model behind the editor (`editor.getHieroglyphicTextModel()`). Register listeners here to react to edits. |
| `MDCEditorKeyManager` | Keyboard handling. |
| `MDCCaret` | Selection and cursor position, as `MDCPosition`s (`getInsertPosition()`, `getMinPosition()`, `getMaxPosition()`...). |

### A one-line field

`JMDCField` is a hieroglyphic text field, for single-line input. Everything above also applies to it.

~~~java
JMDCField textField = new JMDCField();
~~~

Several constructors are available, from "just give me a field" to "fully configured field". The `gui` demo shows three of them:

~~~java
// 1. The simplest one. Uses the fonts embedded in the libraries only.
JMDCField textField1 = new JMDCField();

// 2. Width, height, style and hand-built resources: full control.
JSeshStyle style = JSeshStyle.DEFAULT;

GlossaryManager glossaryManager = new GlossaryManager();
glossaryManager.read();
Glossary glossary = glossaryManager.getGlossary();

HieroglyphResources resources = new HieroglyphResourcesBuilder()
    .addGnuTraceFont()          // only the GNU trace font
    .useUserDefinitions(true)   // pull in signs defined via SignInfo
    .glossary(glossary)         // enable completion from the user's glossary
    .build();

JMDCField textField2 = new JMDCField(300, 40, style, resources);

// 3. Same constructor, with the "full" resources helper: standard font,
// GNU trace font, the user's sign definitions and glossary.
HieroglyphResources resourcesFull = HieroglyphResourcesBuilder.buildWithUserDefinitions();
JMDCField textField3 = new JMDCField(300, 40, style, resourcesFull);
~~~

A fourth constructor, `JMDCField(int width, JSeshStyleReference styleReference, HieroglyphResources resources)`, takes a *shared* style reference, so that several components react together to style changes. The height is then derived from the style.

**Important:** in most cases, resources (fonts, style) should be *shared* between components. If you create them for each component, you end up with several copies of the hieroglyphic fonts in memory.

You can forbid editing with `setEditable(false)`.

---
title: 'Composants Swing'
taxonomy:
    category: docs
    tag: []
---

## Intégrer l'éditeur dans une application Swing

### L'éditeur

`jsesh.ui.editor.JMDCEditor` est un composant Swing prêt à l'emploi. Placez-le dans un `JScrollPane` :

~~~java
import jsesh.ui.editor.JMDCEditor;

JMDCEditor editor = new JMDCEditor();
frame.add(new JScrollPane(editor), BorderLayout.CENTER);

editor.setMDCText("i-mn:n-ra");        // load text (syntax errors are ignored)
String current = editor.getMDCText();  // read it back
~~~

La direction et l'orientation du texte se règlent sur l'éditeur :

~~~java
editor.setTextDirection(TextDirection.RIGHT_TO_LEFT);
editor.setTextOrientation(TextOrientation.HORIZONTAL);
~~~

Le constructeur `JMDCEditor(HieroglyphicTextModel, JSeshStyle, HieroglyphResources)` permet de partager un modèle, d'appliquer un style personnalisé et de fournir vos propres polices et signes (voir [Ressources et polices](/developpers_guide/jsesh_8/resources_and_fonts)). Une variante prend une `JSeshStyleReference`, pour des éditeurs qui doivent suivre un style partagé.

Principaux collaborateurs (vous en avez rarement besoin, mais ils existent pour un contrôle avancé) :

| Classe | Rôle |
|---|---|
| `JMDCEditorWorkflow` | La **machine à états** d'édition : `getMDCCode()`/`setMDCCode()`, curseur, annuler/refaire, insertion. Obtenue par `editor.getWorkflow()`. |
| `HieroglyphicTextModel` | Le modèle observable et annulable derrière l'éditeur (`editor.getHieroglyphicTextModel()`). Enregistrez-y des écouteurs pour réagir aux modifications. |
| `MDCEditorKeyManager` | Gestion du clavier. |
| `MDCCaret` | Sélection et position du curseur, sous forme de `MDCPosition` (`getInsertPosition()`, `getMinPosition()`, `getMaxPosition()`...). |

### Un champ d'une ligne

`JMDCField` est un champ de texte hiéroglyphique pour une saisie sur une ligne. Tout ce qui précède s'y applique aussi.

~~~java
JMDCField textField = new JMDCField();
~~~

Plusieurs constructeurs existent, de « donnez-moi simplement un champ » à « champ entièrement configuré ». La démo `gui` en montre trois :

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

Un quatrième constructeur, `JMDCField(int width, JSeshStyleReference styleReference, HieroglyphResources resources)`, prend une référence de style *partagée*, de sorte que plusieurs composants réagissent ensemble aux changements de style. La hauteur est alors déduite du style.

**Important :** dans la plupart des cas, les ressources (polices, style) doivent être *partagées* entre les composants. Si vous les créez pour chaque composant, vous aurez plusieurs copies des polices hiéroglyphiques en mémoire.

Vous pouvez interdire l'édition avec `setEditable(false)`.

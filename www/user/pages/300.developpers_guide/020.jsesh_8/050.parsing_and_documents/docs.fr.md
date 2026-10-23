---
title: 'Analyse et documents'
taxonomy:
    category: docs
    tag: []
---

## Analyser, lire et écrire du Manuel de Codage

### D'une chaîne MdC à un modèle

Vous avez une chaîne de code MdC et voulez la manipuler (par exemple pour extraire de façon fiable la liste des hiéroglyphes). La solution est de construire un `HieroglyphicText` avec `jsesh.mdcreader.MDCParserModelGenerator` :

~~~java
import jsesh.mdcreader.MDCParserModelGenerator;
import jsesh.parser.MDCSyntaxError;
import jsesh.model.HieroglyphicText;

MDCParserModelGenerator generator = new MDCParserModelGenerator();
try {
    HieroglyphicText text = generator.parse("i-w-r:a-ra-m-p*t:pt");
    // ... use the model ...
} catch (MDCSyntaxError e) {
    // e.getLine() / e.getColumn() locate the problem in the input
    System.err.println("Bad MdC: " + e.getMessage());
}
~~~

- `parse(String)` et `parse(Reader)` sont disponibles.
- Passez un `Dialect` au constructeur (`new MDCParserModelGenerator(Dialect.TKSESH)`) pour lire d'anciens encodages. Pour du MdC moderne, la valeur par défaut convient.
- `setPhilologyAsSigns(true)` traite `[[`, `]]`, `(`... comme des signes ordinaires plutôt que comme des constructions philologiques. Nécessaire seulement pour de très anciens textes TkSesh.
- **Niveau inférieur :** si vous voulez l'arbre syntaxique littéral plutôt qu'un `HieroglyphicText`, utilisez `jsesh.parser.MDCParser`, qui renvoie un `AstDocument` (voir `jsesh.parser.ast`), enregistrement fidèle et non interprété de ce que l'analyseur a lu, que l'on parcourt avec un `AstVisitor`. `MDCParserModelGenerator` est simplement `MDCParser` suivi d'une étape d'interprétation qui transforme cet arbre en `HieroglyphicText`.

### Charger et sauvegarder des documents

Les fichiers contiennent plus que le texte : un encodage, un dialecte, des préférences de document (orientation, direction...). Utilisez `MDCDocument` avec le lecteur et l'écrivain de `jsesh.io.document`.

~~~java
import jsesh.io.document.MDCDocumentReader;
import jsesh.document.MDCDocument;

MDCDocumentReader reader = new MDCDocumentReader();
MDCDocument doc = reader.loadFile(new File("text.gly"));
HieroglyphicText text = doc.getHieroglyphicText();
~~~

Le lecteur **devine l'encodage et le dialecte** à partir de divers indices (contenu du fichier, extension `.hie`, en-tête `@` de WinGlyph, en-tête MacScribe, en-tête `++JSeshInfo` de JSesh...). Il est *tolérant* : une ligne qu'il ne sait pas analyser est conservée telle quelle en texte rouge au lieu d'interrompre le chargement. Appelez `reader.failFast()` auparavant si vous préférez qu'un fichier mal formé lance `MDCSyntaxError`, par exemple pour valider des données.

`readString(mdc, file)` construit un document directement à partir d'une chaîne MdC, en l'associant à un (futur) fichier.

Pour sauvegarder :

~~~java
import jsesh.io.document.MDCDocumentWriter;

new MDCDocumentWriter().write(doc);   // saves to doc.getFile()
~~~

Attention : `write(...)` appelle `prepareForSaving(doc)`, qui **normalise le document en place** : il impose le dialecte JSesh moderne, l'encodage UTF-8 et l'extension `.gly` (ou `.hie` et iso-8859-1 quand la philologie-comme-signes est activée). Variantes :

- `write(doc, OutputStream)` et `write(doc, Writer)` vident le flux mais ne le ferment pas : il reste à l'appelant ;
- `toMdC(doc)` renvoie le document complet (en-tête compris) sous forme de `String` ;
- `toMdC(HieroglyphicText, DocumentPreferences)` est pratique quand vous avez un texte et des préférences, mais pas de vrai document.

### D'un modèle vers du MdC

Si vous n'avez besoin que de la source MdC d'un `HieroglyphicText` (sans en-tête de fichier), utilisez `jsesh.io.mdc.MdCModelWriter` :

~~~java
import jsesh.io.mdc.MdCModelWriter;
import java.io.StringWriter;

StringWriter out = new StringWriter();
new MdCModelWriter().write(out, text);
String mdc = out.toString();
~~~

Il existe aussi les surcharges `write(File, HieroglyphicText)` et `write(String fileName, HieroglyphicText)`. Pour n'écrire qu'une partie du texte, passez deux positions (`jsesh.model.MDCPosition`, situées *entre* les éléments de premier niveau ; construisez-les avec `text.getPositionAt(int)`) : `toMdC(text, start, end)` ou `write(out, text, start, end)`.

### Conversion en Unicode

`jsesh.model.unicode.MdCToUnicodeConverter` convertit un modèle vers le bloc Unicode des hiéroglyphes, avec en option des caractères de contrôle de format pour le groupement :

~~~java
import jsesh.model.unicode.MdCToUnicodeConverter;

MdCToUnicodeConverter converter = new MdCToUnicodeConverter();
converter.setIncludeFormatControlChars(true);   // emit grouping controls
String unicode = converter.convertToPlainUnicode(text);
~~~

Combinez-le avec l'analyseur pour passer directement d'un texte MdC à de l'Unicode.

### Parcourir ou transformer un modèle

Le modèle est un arbre de `ModelElement`s, avec des motifs **visiteur** et **observateur**. Pour l'inspecter ou le transformer, implémentez un visiteur plutôt que des chaînes de `instanceof`.

- La racine est un `HieroglyphicText`, contenant des `TopItem`s (`Cadrat`, `Cartouche`, `LineBreak`, `ZoneStart`...). Un `Cadrat` contient des `HBox`es de `HorizontalListElement`s (`Hieroglyph`, `InnerGroup`, `ComplexLigature`).
- Les modifications structurelles et opérations de plus haut niveau sont dans `jsesh.model.operations`.
- Pour être prévenu des changements, enregistrez-vous auprès du `HieroglyphicTextModel` ou des observateurs de chaque élément.

`MdCToUnicodeConverter` et `MdCModelWriter` sont de bons exemples lisibles de visiteurs du modèle.

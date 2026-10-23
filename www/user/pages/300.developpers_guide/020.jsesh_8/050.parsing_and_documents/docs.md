---
title: Parsing and documents
taxonomy:
    category: docs
    tag: []
---

## Parsing, reading and writing Manuel de Codage

### From an MdC string to a model

You have a string of MdC code and want to manipulate it (for instance, to extract the list of hieroglyphs in a reliable way). The solution is to build a `HieroglyphicText` with `jsesh.mdcreader.MDCParserModelGenerator`:

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

- `parse(String)` and `parse(Reader)` are both available.
- Pass a `Dialect` to the constructor (`new MDCParserModelGenerator(Dialect.TKSESH)`) to read legacy encodings. For plain modern MdC the default is fine.
- `setPhilologyAsSigns(true)` treats `[[`, `]]`, `(`... as ordinary signs instead of philological constructs. It is only needed for very old TkSesh texts.
- **Lower level:** if you want the literal parse tree rather than a `HieroglyphicText`, use `jsesh.parser.MDCParser`, which returns an `AstDocument` (see `jsesh.parser.ast`), a faithful and uninterpreted record of what the parser read, which you can walk with an `AstVisitor`. `MDCParserModelGenerator` is just `MDCParser` followed by an interpretation step which turns this tree into a `HieroglyphicText`.

### Loading and saving documents

Files carry more than the text: an encoding, a dialect, and document preferences (orientation, direction...). Use `MDCDocument` with the reader and writer in `jsesh.io.document`.

~~~java
import jsesh.io.document.MDCDocumentReader;
import jsesh.document.MDCDocument;

MDCDocumentReader reader = new MDCDocumentReader();
MDCDocument doc = reader.loadFile(new File("text.gly"));
HieroglyphicText text = doc.getHieroglyphicText();
~~~

The reader **guesses the encoding and dialect** from various hints (file content, `.hie` extension, WinGlyph `@` header, MacScribe header, JSesh `++JSeshInfo` header...). It is *forgiving*: a line it can't parse is kept verbatim as red text rather than aborting the load. Call `reader.failFast()` beforehand if you prefer a malformed file to throw `MDCSyntaxError`, for instance to validate input.

`readString(mdc, file)` builds a document directly from an MdC string, associating it with a (future) file.

To save:

~~~java
import jsesh.io.document.MDCDocumentWriter;

new MDCDocumentWriter().write(doc);   // saves to doc.getFile()
~~~

Beware: `write(...)` calls `prepareForSaving(doc)`, which **normalises the document in place**: it forces the modern JSesh dialect, UTF-8 encoding, and a `.gly` extension (or `.hie` and iso-8859-1 when philology-as-signs is on). Variants:

- `write(doc, OutputStream)` and `write(doc, Writer)` flush but do not close the stream, which stays the caller's;
- `toMdC(doc)` returns the full document (header included) as a `String`;
- `toMdC(HieroglyphicText, DocumentPreferences)` is a convenience when you have a bare text and preferences, but no real document.

### From a model back to MdC

If you only need the MdC source of a `HieroglyphicText` (no file header), use `jsesh.io.mdc.MdCModelWriter`:

~~~java
import jsesh.io.mdc.MdCModelWriter;
import java.io.StringWriter;

StringWriter out = new StringWriter();
new MdCModelWriter().write(out, text);
String mdc = out.toString();
~~~

It also has `write(File, HieroglyphicText)` and `write(String fileName, HieroglyphicText)` overloads. To write only part of the text, pass two positions (`jsesh.model.MDCPosition`, which fall *between* top items; build them with `text.getPositionAt(int)`): `toMdC(text, start, end)` or `write(out, text, start, end)`.

### Converting to Unicode

`jsesh.model.unicode.MdCToUnicodeConverter` maps a model to the Unicode hieroglyph block, plus optional format control characters for grouping:

~~~java
import jsesh.model.unicode.MdCToUnicodeConverter;

MdCToUnicodeConverter converter = new MdCToUnicodeConverter();
converter.setIncludeFormatControlChars(true);   // emit grouping controls
String unicode = converter.convertToPlainUnicode(text);
~~~

Combine it with the parser to go straight from MdC text to Unicode.

### Walking or transforming a model

The model is a tree of `ModelElement`s, with **visitor** and **observer** patterns. To inspect or transform it, implement a visitor rather than chains of `instanceof`.

- The root is a `HieroglyphicText`, containing `TopItem`s (`Cadrat`, `Cartouche`, `LineBreak`, `ZoneStart`...). A `Cadrat` holds `HBox`es of `HorizontalListElement`s (`Hieroglyph`, `InnerGroup`, `ComplexLigature`).
- Structural edits and higher-level operations live in `jsesh.model.operations`.
- To be notified of changes, register on the `HieroglyphicTextModel` or on the observers of individual elements.

`MdCToUnicodeConverter` and `MdCModelWriter` are good, readable examples of model visitors.

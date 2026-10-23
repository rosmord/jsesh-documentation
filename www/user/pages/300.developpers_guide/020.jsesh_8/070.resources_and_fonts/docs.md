---
title: Resources and fonts
taxonomy:
    category: docs
    tag: []
---

## Resources, fonts and the sign database

"Resources" bundle what rendering, editing and querying need: the sign **shapes** (fonts), the sign **database** (metadata), and the **possibilities** (completion). You build them with `jsesh.defaults.HieroglyphResourcesBuilder`, which gives you a `HieroglyphResources` record (`shapes()`, `database()`, `possibilities()`).

### Ready-made resources

Factory methods cover the usual needs (you need only **one** of them):

~~~java
import jsesh.defaults.HieroglyphResourcesBuilder;
import jsesh.defaults.HieroglyphResources;

// Only what ships inside the jar: no user signs, no user fonts.
HieroglyphResources embedded = HieroglyphResourcesBuilder.buildEmbedded();

// Embedded fonts + the user's SignInfo definitions (signs_definition.xml).
HieroglyphResources withUser = HieroglyphResourcesBuilder.buildWithUserDefinitions();

// Everything: user font folder + user definitions + a glossary for completion.
// Use this when you keep the DirectoryReference and the glossary yourself
// (for instance because your application edits and saves them).
HieroglyphResources full =
    HieroglyphResourcesBuilder.buildFull(userFontsDirectoryReference, glossary);

// Same, but reads the user's own JSesh preferences for you: the one-liner
// for programs which want to behave like JSesh itself.
HieroglyphResources fromPrefs = HieroglyphResourcesBuilder.buildFullFromUserPreferences();
~~~

### Building resources piece by piece

You can add font sources one at a time. **Order matters: earlier fonts win.**

~~~java
HieroglyphResources res = new HieroglyphResourcesBuilder()
        .addFontDirectory("signs1")       // user signs override...
        .addStandardJSeshFont()
        .addGnuTraceFont()                // ...fallback last
        .useUserDefinitions(true)
        .glossary(myGlossary)
        .build();
~~~

### Using signs from several places

The `multipleSignSources` demo uses two font sources: a plain external folder (`signs1`), and a folder *embedded* in the software as a resource (`signs2`), which is useful when you make a release. Signs of `signs1` take precedence over those of `signs2`, which take precedence over standard JSesh signs, and the user's own folder is ignored:

~~~java
public static HieroglyphResources prepareFonts() {
    return new HieroglyphResourcesBuilder()
            .addFontDirectory("signs1")
            .addFontFromResource("/signs2")
            .addStandardJSeshFont()
            .addGnuTraceFont()
            .build();
}
~~~

(`addFontDirectory` also accepts a `File`, and `addFontDirectoryReference` a `DirectoryReference`.) A lower-level equivalent builds a `CompositeHieroglyphShapeRepository` by hand from `DirectoryHieroglyphShapeRepository`, `ResourcesHieroglyphicShapeRepository` and `PredefinedFonts`.

### The glossary

If your program must manage the glossary (for instance to edit it with the glossary editor), get it from the `GlossaryManager`, and don't forget to pass it to the `HieroglyphResourcesBuilder`:

~~~java
GlossaryManager glossaryManager = new GlossaryManager();
// Read the user glossary of the JSesh application.
glossaryManager.read();
Glossary glossary = glossaryManager.getGlossary();
~~~

### The user font directory

You can use several font folders. To use the one set in the JSesh preferences, ask the `UserFontDirectoryManager`:

~~~java
UserFontDirectoryManager userFontDirectoryManager = UserFontDirectoryManager.buildUserFontManager();
DirectoryReference userFontReference = userFontDirectoryManager.getUserFontReference();
~~~

`UserFontDirectoryManager` is the only class of `jsesh.defaults` which touches `java.util.prefs`. If you don't want JSesh's preference tree to be involved at all, ignore it and call `HieroglyphResourcesBuilder.buildFull(...)` with your own `DirectoryReference` and `Glossary`.

### Fully custom build

If you want the same resources as the JSesh application, with full control:

~~~java
GlossaryManager glossaryManager = new GlossaryManager();
glossaryManager.read();
UserFontDirectoryManager userFM = UserFontDirectoryManager.buildUserFontManager();

HieroglyphResources res = new HieroglyphResourcesBuilder()
        .glossary(glossaryManager.getGlossary())
        .addFontDirectoryReference(userFM.getUserFontReference())
        // other font directories if needed
        .addStandardJSeshFont()
        .addGnuTraceFont()
        .useUserDefinitions(true)
        .build();
~~~

### Querying the sign database

`jsesh.glyphs.signdata.HieroglyphDatabase` answers questions about the signs: transliterations, variants, families, tags, code completion.

~~~java
HieroglyphResources resources = HieroglyphResourcesBuilder.buildWithUserDefinitions();
HieroglyphDatabase db = resources.database();

List<String> values       = db.getValuesFor("G17");           // phonetic values of a sign
String description        = db.getDescriptionFor("A1");
Collection<SignVariant> v = db.getVariants("N35");
PossibilitiesList byValue = db.getPossibilityFor("mn", null);  // signs for a phonetic value
PossibilitiesList byCode  = db.getCodesStartingWith("G1");     // code completion
Collection<String> tagged = db.getSignsWithTagInFamily("tall", "A");
~~~

Also see `getFamilies`, `getTagsForSign`, the variant navigation methods (`getVariants(code, VariantTypeForSearches)`, `getTransitiveVariants(...)`), and the search methods `getSuitableSignsForCode`, `getSignsContaining`, `getSignsIn`.

The Gardiner code system itself (parsing `A1`, `G17`, phantom codes...) is in `GardinerCode` and `ManuelDeCodage`, in the `jsesh.signcodes` package.

For the database alone, `jsesh.defaults.HieroglyphDatabaseFactory` offers `buildPlainDefault(codesSource)` and `buildWithUserDefinitions(codesSource)`.

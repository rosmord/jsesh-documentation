---
title: 'Ressources et polices'
taxonomy:
    category: docs
    tag: []
---

## Ressources, polices et base de signes

Les « ressources » regroupent ce dont le rendu, l'édition et les requêtes ont besoin : les **formes** des signes (polices), la **base de données** des signes (métadonnées), et les **possibilités** (complétion). On les construit avec `jsesh.defaults.HieroglyphResourcesBuilder`, qui fournit un record `HieroglyphResources` (`shapes()`, `database()`, `possibilities()`).

### Ressources prêtes à l'emploi

Des méthodes de fabrique couvrent les besoins courants (une **seule** suffit) :

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

### Construire les ressources morceau par morceau

On peut ajouter les sources de polices une à une. **L'ordre compte : les premières polices l'emportent.**

~~~java
HieroglyphResources res = new HieroglyphResourcesBuilder()
        .addFontDirectory("signs1")       // user signs override...
        .addStandardJSeshFont()
        .addGnuTraceFont()                // ...fallback last
        .useUserDefinitions(true)
        .glossary(myGlossary)
        .build();
~~~

### Utiliser des signes de plusieurs origines

La démo `multipleSignSources` utilise deux sources de polices : un dossier externe ordinaire (`signs1`) et un dossier *embarqué* dans le logiciel comme ressource (`signs2`), utile pour faire une distribution. Les signes de `signs1` l'emportent sur ceux de `signs2`, qui l'emportent sur les signes standard de JSesh, et le dossier personnel de l'utilisateur est ignoré :

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

(`addFontDirectory` accepte aussi un `File`, et `addFontDirectoryReference` un `DirectoryReference`.) Un équivalent de plus bas niveau construit à la main un `CompositeHieroglyphShapeRepository` à partir de `DirectoryHieroglyphShapeRepository`, `ResourcesHieroglyphicShapeRepository` et `PredefinedFonts`.

### Le glossaire

Si votre programme doit gérer le glossaire (par exemple pour l'éditer avec l'éditeur de glossaire), obtenez-le du `GlossaryManager`, et n'oubliez pas de le passer au `HieroglyphResourcesBuilder` :

~~~java
GlossaryManager glossaryManager = new GlossaryManager();
// Read the user glossary of the JSesh application.
glossaryManager.read();
Glossary glossary = glossaryManager.getGlossary();
~~~

### Le dossier de polices de l'utilisateur

Vous pouvez utiliser plusieurs dossiers de polices. Pour utiliser celui défini dans les préférences de JSesh, demandez-le à `UserFontDirectoryManager` :

~~~java
UserFontDirectoryManager userFontDirectoryManager = UserFontDirectoryManager.buildUserFontManager();
DirectoryReference userFontReference = userFontDirectoryManager.getUserFontReference();
~~~

`UserFontDirectoryManager` est la seule classe de `jsesh.defaults` qui touche à `java.util.prefs`. Si vous ne voulez pas du tout impliquer l'arbre de préférences de JSesh, ignorez-la et appelez `HieroglyphResourcesBuilder.buildFull(...)` avec vos propres `DirectoryReference` et `Glossary`.

### Construction entièrement personnalisée

Si vous voulez les mêmes ressources que l'application JSesh, avec un contrôle total :

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

### Interroger la base de signes

`jsesh.glyphs.signdata.HieroglyphDatabase` répond aux questions sur les signes : translittérations, variantes, familles, étiquettes, complétion de codes.

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

Voyez aussi `getFamilies`, `getTagsForSign`, les méthodes de navigation entre variantes (`getVariants(code, VariantTypeForSearches)`, `getTransitiveVariants(...)`), et les méthodes de recherche `getSuitableSignsForCode`, `getSignsContaining`, `getSignsIn`.

Le système de codes de Gardiner lui-même (analyse de `A1`, `G17`, codes fantômes...) se trouve dans `GardinerCode` et `ManuelDeCodage`, dans le paquetage `jsesh.signcodes`.

Pour la seule base de données, `jsesh.defaults.HieroglyphDatabaseFactory` offre `buildPlainDefault(codesSource)` et `buildWithUserDefinitions(codesSource)`.

---
title: 'Recettes'
taxonomy:
    category: docs
    tag: []
---

## Ajouter un champ hiéroglyphique à une interface Swing

Ajoutez `jsesh` et `jseshGlyphs` à vos dépendances (voir [Utiliser JSesh dans votre projet](/developpers_guide/jsesh_8/using_jsesh_in_your_project)), puis :

~~~java
import jsesh.ui.editor.JMDCEditor;
import jsesh.ui.editor.JMDCField;

public class MyClass {
    void buildInterface() {
        // A large editor, better placed in a JScrollPane
        JMDCEditor editor = new JMDCEditor();
        // A text-field-like editor
        JMDCField mdcField = new JMDCField();
    }
}
~~~

Vous pouvez ensuite utiliser `setMDCText(String)` et `getMDCText()` pour définir et récupérer le contenu en Manuel de Codage, ou travailler directement avec le `HieroglyphicTextModel`. `setEditable(false)` interdit l'édition. Voir [Composants Swing](/developpers_guide/jsesh_8/swing_components) et la démo `gui`.

## Produire une image bitmap à partir d'un texte MdC

~~~java
MDCDrawingFacade facade = MDCDrawingFacade.buildDefault();
facade.setCadratHeight(60);
BufferedImage img = facade.createImage("i-w-r:a-ra-m-p*t:pt");
ImageIO.write(img, "png", new File("example.png"));
~~~

Les marges, la direction du texte et les autres réglages sont contrôlés par un `JSeshStyle`. Voir [Rendu](/developpers_guide/jsesh_8/rendering) et le `bitmapDemo`.

## Produire un fichier SVG

Voir [Rendu](/developpers_guide/jsesh_8/rendering) et le `svgExportDemo`.

## Utiliser des signes provenant de vos propres dossiers

Voir [Ressources et polices](/developpers_guide/jsesh_8/resources_and_fonts) et la démo `multipleSignSources`.

## Lancer une démo

Chaque démo est un projet Gradle autonome. Après avoir [installé les bibliothèques JSesh dans votre dépôt Maven local](/developpers_guide/jsesh_8/getting_the_code) :

~~~bash
git clone https://github.com/rosmord/jsesh-demos.git
cd jsesh-demos/bitmapDemo
./gradlew run
~~~

---
title: How to
taxonomy:
    category: docs
    tag: []
---

## Add a hieroglyphic field to a Swing interface

Add `jsesh` and `jseshGlyphs` to your dependencies (see [Using JSesh in your project](/developpers_guide/jsesh_8/using_jsesh_in_your_project)), then:

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

You can then use `setMDCText(String)` and `getMDCText()` to set and retrieve the content as Manuel de Codage, or work directly with the `HieroglyphicTextModel`. `setEditable(false)` forbids editing. See [Swing components](/developpers_guide/jsesh_8/swing_components) and the `gui` demo.

## Produce a bitmap picture from an MdC text

~~~java
MDCDrawingFacade facade = MDCDrawingFacade.buildDefault();
facade.setCadratHeight(60);
BufferedImage img = facade.createImage("i-w-r:a-ra-m-p*t:pt");
ImageIO.write(img, "png", new File("example.png"));
~~~

Margins, text direction and other settings are controlled by a `JSeshStyle`. See [Rendering](/developpers_guide/jsesh_8/rendering) and the `bitmapDemo`.

## Produce an SVG file

See [Rendering](/developpers_guide/jsesh_8/rendering) and the `svgExportDemo`.

## Use signs from your own folders

See [Resources and fonts](/developpers_guide/jsesh_8/resources_and_fonts) and the `multipleSignSources` demo.

## Run a demo

Each demo is a self-contained Gradle project. After [installing the JSesh libraries in your local Maven repository](/developpers_guide/jsesh_8/getting_the_code):

~~~bash
git clone https://github.com/rosmord/jsesh-demos.git
cd jsesh-demos/bitmapDemo
./gradlew run
~~~

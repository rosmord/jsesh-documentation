---
title: How to
taxonomy:
    category: docs
    tag: []
---


## Add a hieroglyphic edition field in a SWING interface

Actually, this is quite easy to do. You need to have jsesh.jar in your classpath, and probably jseshGlyphs.jar too if you want the full fonts. Then, having a hieroglyphic field in your application is as easy as:

~~~java
// The package may change one day in the (far) future.
import package jsesh.mdcDisplayer.swing.editor.*;
public MyClass .... {
   void buildInterface() {
           // A large editor, better placed in a JScrollPane
           JMDCEditor editor= new JMDCEditor();
           // A TextField-like editor
           JMDCField mdcField= new JMDCField();
    }
}
~~~

Now, you can manipulate the text directly through the HieroglyphicTextModel class, which represents the text as a list of objects, or, if you need only simple functionalities, use the methods `setMDCText(String mdc)` and `getMDCText()` to set and retrieve the content of the field as "Manuel de codage".

You can forbid the editing of the text with `setEditable(false)`

One thing which is currently missing from the libraries (but which should be fixed soon) is a way to easily direct the information from the palette to various JSesh widgets (it can be done with the overall structure, but it's not automatic at all).

## Producing a bitmap picture from an MDC text

There are a number of reasons for which you might want to produce a picture from an MDC Text. For instance, you might use JSesh as a library in a web application.

Of course, you need to have both jsesh.jar and jseshGlyphs.jar in your classpath. Currently (JSesh 2.13.7) you also need jvectClipboard-1.0.jar, but this is a dependency I will remove in a short while. You will need jvectClipboard-1.0.jar if you want to produce SVG, WMF or the like. Then the following Java code will do:

~~~java
public static BufferedImage buildImage(String mdcText) throws MDCSyntaxError {
    // Create the drawing system:                
    MDCDrawingFacade drawing = new MDCDrawingFacade();
    // Create the picture 
    BufferedImage result = drawing.createImage(mdcText);
    return result
}
~~~

That's all. Once you have a BufferedImage, it can be displayed on the screen, or written in JPEG or PNG using ImageIO.

Optionnally, it's possible to customize the rendering. Here is a complete ready-to run example:

~~~java
 /**
 * How to use JSesh to create bitmaps in Java.
 * compile: javac -cp .:/FOLDER_CONTAINING/jsesh.jar TestJSeshBitmap.java
 * run: java -cp .:/FOLDER_CONTAINING/jsesh.jar TestJSeshBitmap
 * 
 * jseshGlyphs.jar and jvectClipboard-1.0.jar should be in the same folder as jsesh.jar.
 * (normally, there is no need to add them explicitely to the class path , as jsesh.jar contains the necessary 
 * information in its manifest.
 */

import  javax.imageio.ImageIO;
import java.io.*;
import java.awt.image.* ;
import jsesh.mdcDisplayer.preferences.*;
import jsesh.mdcDisplayer.draw.*;
import jsesh.mdc.*;

public class Test {
    public static BufferedImage buildImage(String mdcText) throws MDCSyntaxError {
        // Create the drawing system:                
        MDCDrawingFacade drawing = new MDCDrawingFacade();
        // Change the scale, choosing the cadrat height in pixels.
        drawing.setCadratHeight(60);
        // Change a number of parameters 
        DrawingSpecification drawingSpecifications = new DrawingSpecificationsImplementation();
        PageLayout pageLayout= new PageLayout();
        pageLayout.setLeftMargin(5);
        pageLayout.setTopMargin(5);
        drawingSpecifications.setPageLayout(pageLayout);
        drawing.setDrawingSpecifications(drawingSpecifications);
        // Create the picture 
       BufferedImage result = drawing.createImage(mdcText);
       return result;
    }

public static void main(String args[]) throws MDCSyntaxError, IOException {
              // Create the picture
              BufferedImage img= buildImage("i-w-r:a-C1-m-p*t:pt");
              File f = new File("example.png");
              // save it in png (better than jpeg in this case)
              ImageIO.write(img, "png", f);
  }
}
~~~

The size of the signs is controlled using `drawing.setCadratHeight()`.

(note to self: it should be easier to change the size of everything using `drawingSpecification` !!!)

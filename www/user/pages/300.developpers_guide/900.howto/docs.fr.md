---
title: Comment faire
taxonomy:
    category: docs
    tag: []
---


## Ajouter un champ d'édition hiéroglyphique dans une interface SWING

En fait, c'est assez facile à faire. Vous devez avoir jsesh.jar dans votre classpath, et probablement aussi jseshGlyphs.jar si vous voulez les polices complètes. Ensuite, avoir un champ hiéroglyphique dans votre application est aussi simple que ceci :

~~~java
// Le package pourra changer un jour dans un (lointain) avenir.
import package jsesh.mdcDisplayer.swing.editor.*;
public MyClass .... {
   void buildInterface() {
           // Un grand éditeur, à placer de préférence dans un JScrollPane
           JMDCEditor editor= new JMDCEditor();
           // Un éditeur de type TextField
           JMDCField mdcField= new JMDCField();
    }
}
~~~

Vous pouvez maintenant manipuler le texte directement via la classe HieroglyphicTextModel, qui représente le texte sous forme de liste d'objets, ou, si vous n'avez besoin que de fonctionnalités simples, utiliser les méthodes `setMDCText(String mdc)` et `getMDCText()` pour définir et récupérer le contenu du champ au format « Manuel de codage ».

Vous pouvez interdire l'édition du texte avec `setEditable(false)`.

Une chose qui manque actuellement dans les bibliothèques (mais qui devrait être corrigée bientôt) est un moyen de diriger facilement les informations de la palette vers divers composants JSesh (cela peut être fait avec la structure globale, mais ce n'est pas du tout automatique).

## Produire une image bitmap à partir d'un texte MDC

Il existe un certain nombre de raisons pour lesquelles vous pouvez souhaiter produire une image à partir d'un texte MDC. Par exemple, vous pouvez utiliser JSesh comme bibliothèque dans une application Web.

Bien sûr, vous devez avoir à la fois jsesh.jar et jseshGlyphs.jar dans votre classpath. Actuellement (JSesh 2.13.7), vous avez également besoin de jvectClipboard-1.0.jar, mais c'est une dépendance que je supprimerai sous peu. Vous aurez besoin de jvectClipboard-1.0.jar si vous souhaitez produire du SVG, du WMF ou similaire. Ensuite, le code Java suivant fera l'affaire :

~~~java
public static BufferedImage buildImage(String mdcText) throws MDCSyntaxError {
    // Création du système de dessin :
    MDCDrawingFacade drawing = new MDCDrawingFacade();
    // Création de l'image
    BufferedImage result = drawing.createImage(mdcText);
    return result
}
~~~

C'est tout. Une fois que vous avez une BufferedImage, elle peut être affichée à l'écran, ou écrite en JPEG ou en PNG à l'aide d'ImageIO.

En option, il est possible de personnaliser le rendu. Voici un exemple complet, prêt à l'emploi :

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

La taille des signes est contrôlée à l'aide de `drawing.setCadratHeight()`.

(note à moi-même : il devrait être plus facile de tout redimensionner en utilisant `drawingSpecification` !)

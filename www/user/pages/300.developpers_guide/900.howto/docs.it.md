---
title: Come fare
taxonomy:
    category: docs
    tag: []
---


## Aggiungere un campo di modifica geroglifico in un'interfaccia SWING

In realtà, è abbastanza semplice. Devi avere jsesh.jar nel tuo classpath e probabilmente anche jseshGlyphs.jar se vuoi i font completi. Quindi, avere un campo geroglifico nella tua applicazione è semplice come:

~~~java
// Il pacchetto potrebbe cambiare in un (lontano) futuro.
import package jsesh.mdcDisplayer.swing.editor.*;
public MyClass .... {
   void buildInterface() {
           // Un editor di grandi dimensioni, meglio posizionato in un JScrollPane
           JMDCEditor editor= new JMDCEditor();
           // Un editor simile a TextField
           JMDCField mdcField= new JMDCField();
    }
}
~~~

Ora è possibile manipolare il testo direttamente tramite la classe HieroglyphicTextModel, che rappresenta il testo come un elenco di oggetti, oppure, se si necessita solo di funzionalità semplici, utilizzare i metodi `setMDCText(String mdc)` e `getMDCText()` per impostare e recuperare il contenuto del campo come "Manuel de codage".

È possibile impedire la modifica del testo con `setEditable(false)`.

Una cosa che attualmente manca nelle librerie (ma che dovrebbe essere risolta a breve) è un modo per indirizzare facilmente le informazioni dalla palette a vari widget JSesh (può essere fatto con la struttura generale, ma non è affatto automatico).

## Generare un'immagine bitmap da un testo MDC

Ci sono diversi motivi per cui si potrebbe voler generare un'immagine da un testo MDC. Ad esempio, si potrebbe utilizzare JSesh come libreria in un'applicazione web.

Naturalmente, è necessario avere sia jsesh.jar che jseshGlyphs.jar nel classpath. Attualmente (JSesh 2.13.7) è necessario anche jvectClipboard-1.0.jar, ma questa è una dipendenza che eliminerò a breve. Se si desidera generare SVG, WMF o simili, sarà necessario jvectClipboard-1.0.jar. A questo punto, il codice Java seguente sarà sufficiente:

~~~java
public static BufferedImage buildImage(String mdcText) throws MDCSyntaxError {
    // Crea il sistema di disegno:                
    MDCDrawingFacade drawing = new MDCDrawingFacade();
    // Crea l'immagine 
    BufferedImage result = drawing.createImage(mdcText);
    return result
}
~~~

Questo è tutto. Una volta ottenuta una BufferedImage, è possibile visualizzarla sullo schermo o scriverla in formato JPEG o PNG utilizzando ImageIO.

Opzionalmente, è possibile personalizzare il rendering. Ecco un esempio completo e pronto all'uso:

~~~java
 /**
 * Come usare JSesh per creare bitmap in Java.
 * compilare: javac -cp .:/FOLDER_CONTAINING/jsesh.jar TestJSeshBitmap.java
 * eseguire: java -cp .:/FOLDER_CONTAINING/jsesh.jar TestJSeshBitmap
 *
 * jseshGlyphs.jar e jvectClipboard-1.0.jar dovrebbero trovarsi nella stessa cartella di jsesh.jar.
 * (normalmente, non è necessario aggiungerli esplicitamente al class path, poiché jsesh.jar contiene le informazioni necessarie
 * nel suo manifest.
 */

import  javax.imageio.ImageIO;
import java.io.*;
import java.awt.image.* ;
import jsesh.mdcDisplayer.preferences.*;
import jsesh.mdcDisplayer.draw.*;
import jsesh.mdc.*;

public class Test {
    public static BufferedImage buildImage(String mdcText) throws MDCSyntaxError {
        // Crea il sistema di disegno:                
        MDCDrawingFacade drawing = new MDCDrawingFacade();
        // Modifica la scala, scegliendo l'altezza del quadrato in pixel.
        drawing.setCadratHeight(60);
        // Modifica una serie di parametri 
        DrawingSpecification drawingSpecifications = new DrawingSpecificationsImplementation();
        PageLayout pageLayout= new PageLayout();
        pageLayout.setLeftMargin(5);
        pageLayout.setTopMargin(5);
        drawingSpecifications.setPageLayout(pageLayout);
        drawing.setDrawingSpecifications(drawingSpecifications);
        // Crea l'immagine
       BufferedImage result = drawing.createImage(mdcText);
       return result;
    }

public static void main(String args[]) throws MDCSyntaxError, IOException {
              // Crea l'immagine
              BufferedImage img= buildImage("i-w-r:a-C1-m-p*t:pt");
              File f = new File("example.png");
              // salvalo in png (meglio di jpeg in questo caso)
              ImageIO.write(img, "png", f);
  }
}
~~~

La dimensione dei segnali è controllata tramite `drawing.setCadratHeight()`.

(nota personale: dovrebbe essere più facile modificare le dimensioni di tutto tramite `drawingSpecification`!!!)

---
title: 'Rendu'
taxonomy:
    category: docs
    tag: []
---

## Afficher des hiéroglyphes

`jsesh.render.draw.MDCDrawingFacade` est la classe des programmeurs qui veulent simplement dessiner des hiéroglyphes. Elle accepte une `String` MdC ou un `HieroglyphicText`.

### Un bitmap à partir d'une chaîne MdC

~~~java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

import jsesh.render.draw.MDCDrawingFacade;

MDCDrawingFacade facade = MDCDrawingFacade.buildDefault();
facade.setCadratHeight(40);   // approximate height of a cadrat, in pixels
BufferedImage img = facade.createImage("i-w-r:a-ra-m-p*t:pt");
ImageIO.write(img, "png", new File("word.png"));
~~~

`buildDefault()` utilise les polices embarquées dans les bibliothèques et le style par défaut. Elle n'inclut **pas** les signes personnels de l'utilisateur : pour cela, voir [Ressources et polices](/developpers_guide/jsesh_8/resources_and_fonts).

`createImage` lance une `jsesh.parser.MDCSyntaxError` si le texte ne peut pas être analysé.

### Choisir le style

Le style est un `JSeshStyle` immuable (voir [Concepts de base](/developpers_guide/jsesh_8/core_concepts)). Voici un exemple complet (c'est le `bitmapDemo`) :

~~~java
public static BufferedImage buildImage(String mdcText) throws MDCSyntaxError {
    MDCDrawingFacade facade = MDCDrawingFacade.buildDefault();
    // Change the global scale, choosing the cadrat height in pixels.
    facade.setCadratHeight(32);
    // Define the drawing style (if you don't, you get the default style).
    JSeshStyle style = JSeshStyle.DEFAULT.copy()
        .options(o -> o.textDirection(TextDirection.RIGHT_TO_LEFT)
                       .smallSignCentered(true))
        .geometry(g -> g.leftMargin(10)
                        .topMargin(10))
        .build();
    facade.setStyle(style);
    return facade.createImage(mdcText);
}
~~~

Autres réglages : `setDeviceScale(double)` (pixels par point typographique : augmentez-le pour la résolution d'impression) et `setMaxSize(w, h)` (limite la taille du bitmap).

### Dessiner sur un Graphics2D

Utile pour inclure des hiéroglyphes dans un dessin plus large (rapport, composant personnalisé, autre exporteur) :

~~~java
// g is a Graphics2D; x, y is the top-left target point.
Rectangle2D bounds = facade.draw("nfr-nfr-nfr", g, x, y);
// bounds is the box which was drawn, useful for layout.
~~~

`getBounds(mdcText, x, y)` calcule la même boîte **sans** dessiner, ce qui permet de dimensionner un composant ou de mettre en page d'abord.

### SVG

La sortie SVG utilise le même mécanisme : on calcule d'abord la taille de l'image, puis on dessine sur un `SVGGraphics2D` (de la bibliothèque `jvectclipboard`, voir [Utiliser JSesh dans votre projet](/developpers_guide/jsesh_8/using_jsesh_in_your_project)). C'est le `svgExportDemo` :

~~~java
import org.qenherkhopeshef.graphics.svg.SVGGraphics2D;
import jsesh.utils.datatypes.DoubleDimensions;

public static void buildImage(String mdcText) throws MDCSyntaxError, IOException {
    MDCDrawingFacade facade = MDCDrawingFacade.buildDefault();
    facade.setCadratHeight(200);
    // Find the picture size
    Rectangle2D dims = facade.getBounds(mdcText, 0, 0);

    try (FileWriter writer = new FileWriter("foo.svg")) {
        SVGGraphics2D g = new SVGGraphics2D(writer,
                new DoubleDimensions(dims.getWidth(), dims.getHeight()));
        facade.draw(mdcText, g, 0, 0);
        g.dispose();
    }
}
~~~

### Construire la façade explicitement

Si vous avez vos propres `HieroglyphResources` (voir [Ressources et polices](/developpers_guide/jsesh_8/resources_and_fonts)), construisez la façade à partir d'un contexte de rendu :

~~~java
import jsesh.render.context.JSeshRenderContext;
import jsesh.render.style.JSeshStyle;
import jsesh.glyphs.fonts.PredefinedFonts;

JSeshRenderContext ctx = new JSeshRenderContext(
        JSeshStyle.DEFAULT, PredefinedFonts.buildAllEmbeddedFonts());
MDCDrawingFacade facade = new MDCDrawingFacade(ctx);
~~~

### Contrôle total

La démo `lowleveldrawing` détaille toutes les étapes pour passer d'une chaîne en Manuel de Codage à une image. Dans la plupart des cas, `MDCDrawingFacade` est une alternative plus simple. La chaîne de rendu, si vous en avez besoin, est `ViewBuilder.buildView(text, renderContext, techContext)`, qui renvoie un `MDCView`, suivi de `new ViewDrawer().draw(graphics, renderContext, techContext, view)` (paquetages `jsesh.render.view` et `jsesh.render.draw`).

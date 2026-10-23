---
title: Rendering
taxonomy:
    category: docs
    tag: []
---

## Rendering hieroglyphs

`jsesh.render.draw.MDCDrawingFacade` is the class for programmers who just want to draw hieroglyphs. It accepts either an MdC `String` or a `HieroglyphicText`.

### A bitmap from an MdC string

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

`buildDefault()` uses the fonts embedded in the libraries and the default style. It does **not** include the user's own signs: for that, see [Resources and fonts](/developpers_guide/jsesh_8/resources_and_fonts).

`createImage` throws a `jsesh.parser.MDCSyntaxError` if the text can't be parsed.

### Choosing the style

The style is an immutable `JSeshStyle` (see [Core concepts](/developpers_guide/jsesh_8/core_concepts)). Here is a complete example (this is the `bitmapDemo`):

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

Other settings: `setDeviceScale(double)` (pixels per typographic point: raise it for print resolution) and `setMaxSize(w, h)` (caps the bitmap size).

### Drawing on a Graphics2D

This is useful to include hieroglyphs in a larger drawing (a report, a custom component, another exporter):

~~~java
// g is a Graphics2D; x, y is the top-left target point.
Rectangle2D bounds = facade.draw("nfr-nfr-nfr", g, x, y);
// bounds is the box which was drawn, useful for layout.
~~~

`getBounds(mdcText, x, y)` computes the same box **without** drawing, so that you can size a component or lay out a page first.

### SVG

SVG output uses the same mechanism: first compute the size of the picture, then draw it on an `SVGGraphics2D` (from the `jvectclipboard` library, see [Using JSesh in your project](/developpers_guide/jsesh_8/using_jsesh_in_your_project)). This is the `svgExportDemo`:

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

### Building the facade explicitly

If you have your own `HieroglyphResources` (see [Resources and fonts](/developpers_guide/jsesh_8/resources_and_fonts)), build the facade from a render context:

~~~java
import jsesh.render.context.JSeshRenderContext;
import jsesh.render.style.JSeshStyle;
import jsesh.glyphs.fonts.PredefinedFonts;

JSeshRenderContext ctx = new JSeshRenderContext(
        JSeshStyle.DEFAULT, PredefinedFonts.buildAllEmbeddedFonts());
MDCDrawingFacade facade = new MDCDrawingFacade(ctx);
~~~

### Total control

The `lowleveldrawing` demo details all the steps needed to go from a Manuel de Codage string to a picture. In most cases, `MDCDrawingFacade` is a simpler alternative. The pipeline, should you need it, is `ViewBuilder.buildView(text, renderContext, techContext)`, which returns an `MDCView`, followed by `new ViewDrawer().draw(graphics, renderContext, techContext, view)` (packages `jsesh.render.view` and `jsesh.render.draw`).

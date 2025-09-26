---
title: Ombreggiatura/Tratteggio
taxonomy:
    category: docs
---


Al momento, l'ombreggiatura/tratteggio è un po' complessa. La cattiva notizia è che peggiorerà.

Come opzione (consultare le proprietà File/Documento), l'ombreggiatura può essere la classica "ombreggiatura a linee incrociate" che si può vedere nelle vecchie pubblicazioni, oppure uno sfondo grigio chiaro. Sebbene molti utenti preferiscano la prima opzione per tradizione, la seconda è effettivamente tipograficamente superiore. L'ombreggiatura a linee incrociate rende i segni difficili da leggere, cosa che non accade con lo sfondo grigio chiaro.

L'ombreggiatura è disponibile in diverse varianti. Questo è dovuto alla storia del Manuel de Codage.

Un buon riassunto è disponibile nel documento di esempio di JSesh (quello che appariva all'avvio di JSesh e che ora è incluso nella libreria di testo di JSesh (nella prossima versione, ovviamente)).

Ma, per dirla tutta:

* In origine, esistevano due sistemi di ombreggiatura. Il primo ombreggiava un'intera parte di testo. È l'ombreggiatura che si ottiene quando si chiede "zona ombreggiata". In JSesh, funziona sul **testo selezionato**.
* Il secondo sistema di ombreggiatura utilizzava simboli di ombreggiatura, usati esattamente come geroglifici. Nel manuale originale, i cadrat venivano ombreggiati sovrascrivendoli con i simboli di ombreggiatura corrispondenti. Si ottengono dalla voce di menu "simbolo di ombreggiatura". Pertanto, ![Una lepre sopra una zona ombreggiata](./basic.png?classes=inline) può essere ottenuta digitando "wn", quindi aggiungendo un simbolo di ombreggiatura e impilando entrambi verticalmente. JSesh supporta questo tipo di ombreggiatura fin dall'inizio, ma un menu per utilizzarlo è stato reso disponibile solo nella versione 2.10.
* Poi, intorno al 1994, fu proposto un nuovo sistema di ombreggiatura, che copriva la maggior parte dei casi semplici. È quello che si ottiene tramite il menu "Ombreggiatura". Si applica al gruppo corrente (il gruppo davanti al cursore) e può essere utilizzato per ombreggiare qualsiasi quarto di un gruppo.
* MacScribe è in grado di ombreggiare un quarto di singoli segni. In MacScribe, "`p##13*p:pt`" avrebbe ombreggiato a metà il segno "p". Una variante di questo sistema è supportata da JSesh. Il software esterno [MacScribe converter](https://jsesh.qenherkhopeshef.org/software/MacScribeImporter.zip) lo supporta.
* Anche un sistema di ombreggiatura "libero" sarebbe utile. In questo caso, il contorno della zona ombreggiata verrebbe disegnato liberamente. Ho intenzione di aggiungerlo (sfruttando l'editor di gruppi). Ma al momento, se hai bisogno di essere così preciso, l'unica opzione che JSesh ti offre è quella di esportare il tuo file in un formato comodo (ad esempio SVG) e modificarlo lì.

## Ombreggiatura di una parte di un quadrante

La voce di menu in Manipolazione/Ombreggiatura del testo può essere applicata a una selezione. In altre parole, è possibile ombreggiare la parte superiore di tutti i gruppi di una selezione in un'unica operazione (in precedenza, era necessario ombreggiare ogni gruppo singolarmente).

Per chi digita testi con molte lacune, ho aggiunto un menu a comparsa. Premendo il tasto "#" sulla tastiera, verrà visualizzato questo menu. È possibile navigare al suo interno con la tastiera o selezionare le voci tramite una lettera specifica.

Ecco un esempio. Ho selezionato una parte del testo e ho premuto "#". Si apre il popup.

![Popup di ombreggiatura parziale](./popup_it.png)

Now I can select the shading I need by various means (it depends on your computer system). For instance, I can type "3", move in the menu with the keyboard arrows or select the menu item with the mouse. Then, the whole selected text is shaded:

![Ombreggiatura parziale applicata](./shading2_it.png)

## Opzioni attuali per realizzare ombreggiature complesse

Se, ad esempio, vuoi aggiungere una zona ombreggiata al centro di un cartello, ora puoi farlo. In effetti, è il motivo per cui ho aggiunto un menu per recuperare i "vecchi" simboli di ombreggiatura.

Supponiamo che tu voglia creare ![](./shading3.png?classes=inline). Devi prima inserire entrambi i cartelli. L'ombreggiatura viene aggiunta tramite i menu:

![Aggiungere un simbolo di ombreggiatura](./addSymbol_it.png)

Quindi, ti basterà utilizzare l'editor di gruppo:

![Spostamento dei simboli di ombreggiatura con l'editor di gruppo](./group_it.png)

Probabilmente dovresti inserire prima il simbolo di ombreggiatura e poi il glifo. In questo modo, se il formato di output finale non supporta la trasparenza, otterrai comunque un rendering corretto.

(A proposito, anche i segni ecdotici come `[ ... ]` sono glifi. Pertanto, possono essere spostati nell'editor di gruppo).

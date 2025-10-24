---
title: Copia/incolla
taxonomy:
    category: docs
---

A partire dalla versione 5, è possibile utilizzare la funzione copia e incolla per trasferire dati tra JSesh e altre applicazioni. È possibile:

* Copiare/incollare tra diverse finestre di JSesh stesso.
* Copiare testo e caratteri in un elaboratore di testi (funziona sia con OpenOffice che con Word).

## Copia e incolla: configurazione

Spesso, in un'applicazione sono necessarie due dimensioni per i caratteri: una per il testo principale e una più piccola per le note a piè di pagina. JSesh consente di mantenere due configurazioni per il copia e incolla. La dimensione corrente può essere selezionata nel menu di modifica: basta scegliere "copia: piccola", "copia: grande" o "copia: wysiwyg" (quest'ultima opzione è consigliata se si desidera che il glifo copiato mantenga la stessa disposizione di quelli originali).

### Scelta del formato

Un copia e incolla coinvolge due software: JSesh e il tuo elaboratore di testi (Word, OpenOffice, ecc.).
Ora, JSesh proporrà diversi *formati* al tuo elaboratore di testi, lasciandogli scegliere quello che preferisce. Per controllare cosa verrà proposto da JSesh, puoi utilizzare la finestra di dialogo Scelta del formato (nelle preferenze).

Eseguo la maggior parte dei miei test con **Open Office** e **Libre Office**. Non sono perfetti, ma tendono a elaborare correttamente immagini e Unicode, quindi ne consiglio vivamente l'uso. I loro file tendono ad essere facilmente trasferibili da un computer all'altro. Nessun problema con le diverse versioni dell'elaboratore di testi.

![Format choice dialog](formatChoice.img_assist_custom.png?classes=caption "Format choice dialog")


RTF
: probabilmente la scelta più versatile per ora. Funziona (quasi) ovunque e offre risultati ragionevoli, soprattutto per geroglifici mischiati a testo alfabetico. In passato creava problemi con alcune versioni di Word su Mac, ma recentemente (2016) è migliorato.

PDF
: attualmente la scelta più accurata. Per quanto ne so, solo Mac OS X supporta il copia e incolla PDF, e pochi software lo supportano. Ad esempio, Word 2004 non lo supporta. Word 2008 sì, invece. Textedit ha la pessima idea di accettare il copia e incolla PDF, ma trasforma il risultato in un'immagine bitmap.

bitmap
: restituisce un'immagine bitmap (attualmente) a bassa risoluzione, adatta ad esempio per le pagine web.

testo normale
: copierà la codifica *Manuel de Codage* negli appunti.

Per informazioni specifiche sul tuo **elaboratore di testi**, consulta il capitolo sui [[word_processor_issues|problemi dell'elaboratore di testi]]

### Impostazioni avanzate


Le impostazioni per "dimensione grande/dimensione piccola/wysiwyg" possono essere modificate nelle preferenze. Ci sono due schede, una per la dimensione "piccola" e l'altra per la dimensione "grande". La modalità "wysiwyg" utilizza le impostazioni per la dimensione grande.

![](./cut_and_paste_preferences_it.png?classes=caption "Preferenze di taglia e incolla")

"Altezza riquadro" modifica la dimensione del testo geroglifico incollato. "Modalità di esportazione" consente di scegliere come incollare il testo geroglifico nelle esportazioni RTF. Sono disponibili tre opzioni:

* **come un'unica immagine grande** L'intero testo selezionato verrà incollato nell'elaboratore di testi come un'unica immagine. Questa opzione è adatta, ad esempio, per il testo in colonne o se si desidera mantenere il layout grafico. Sembra inoltre che la maggior parte degli elaboratori di testi preferisca gestire immagini di grandi dimensioni piuttosto che molte immagini piccole.

* **raggruppamento di riquadri** I riquadri di geroglifici adiacenti verranno raggruppati in un'unica immagine. Il testo risultante alternerà testo normale e immagini di grandi dimensioni.

* **un'immagine per riquadro** Il testo incollato conterrà testo normale e immagini per il testo geroglifico. Tuttavia, ogni riquadro verrà visualizzato come un'unica immagine. Questa opzione è ideale per il taglio delle linee e potrebbe essere interessante se si combinano testo e geroglifici.

### Limitazioni per il taglia e incolla

A causa di problemi tecnici, abbiamo imposto un limite al taglia e incolla. Non è possibile incollare testi molto lunghi in un elaboratore di testi (è possibile "esportare in formato RTF"). Cercheremo di migliorare la funzionalità, ma riteniamo che sia un piccolo inconveniente, poiché in genere si incollano piccole parti di testi geroglifici anziché interi documenti di grandi dimensioni (il limite attuale è di 1000 cadrat).

Don't hesitate to write to the author about this (or other problems with JSesh).

## Menu "copia" avanzato

Normalmente, in JSesh, si sceglie il formato desiderato per il copia/incolla nel menu delle preferenze. Ma in alcuni casi, si potrebbe voler copiare il testo in un formato specifico diverso da quello scelto. Invece di tornare alle preferenze, è possibile utilizzare il menu "Copia come". Questo consente di copiare il testo selezionato in PDF, RTF o Bitmap.

## Possibilità di incollare testo geroglifico in JSesh

### Principi e problemi

Mi dispiace, questa parte è un po' tecnica. Se qualcuno fosse in grado di scrivere le stesse spiegazioni in modo più chiaro, sarebbe un gradito contributo al sito di JSesh.

Su Windows (e sui Mac OS precedenti a Mac OS X), esiste una funzionalità chiamata "Collegamento e incorporamento di oggetti", che è più o meno un taglia e incolla intelligente. Copia/incolla un documento dal tuo editor di geroglifici in Word, quindi fai doppio clic sull'immagine incollata per aprire l'editor di geroglifici, in modo da poter modificare il testo.

Questo non è possibile con JSesh, poiché questo tipo di funzionalità è molto specifico del sistema (se ne avete davvero bisogno, mi risulta che sia ben supportato in Inscribe). Tuttavia, la versione 2.11 di JSesh fornisce una versione "povera". In pratica, il trucco (utilizzato anche in alcuni altri editor di geroglifici, come MacScribe) consiste nell'utilizzare il campo di commento disponibile in alcuni formati immagine (come PDF o EMF) e inserire il testo del manuale di codifica in questo campo. Quando l'immagine viene incollata in JSesh, è possibile semplicemente estrarre il codice.

Naturalmente, questo è più o meno automatico. Ma ho dovuto spiegarlo, perché dipende da diversi fattori:

* il formato dell'immagine deve supportare i commenti e devo scrivere il codice corrispondente. Attualmente questo viene fatto solo per EMF e PDF.
* l'elaboratore di testi deve accettare l'immagine incollata "così com'è" e non modificarla. Le modifiche di solito eliminano il commento. Ad esempio, su un Mac, è possibile incollare un'immagine PDF in MS/Word 2008. Ma Word (credo) trasformerà l'immagine nel suo formato originale, perdendo il commento nel processo.

Tutte queste spiegazioni per dirvi che questo sistema non funziona con tutti gli elaboratori di testi... e soprattutto non con MS/Word (almeno non con Word 2008 su Mac). Mi scuso.

Ora passiamo alle possibili soluzioni

### Mellel/Nissus Writer e PDF

Se utilizzi Mellel o Nissus Writer (e se configuri l'opzione "taglia e incolla" per usare il formato PDF), potrai incollare nuovamente i tuoi geroglifici in JSesh.

Basta selezionare i geroglifici nel vostro elaboratore di testo (ad esempio Mellel) e copiarli...

![Copiare da Mellel](mellel_copy.png?classes=caption "Copiare da Mellel")

Quindi si torna su JSesh e si seleziona File/Importa/Importa da PDF incollato.

![Importare PDF](jsesh_pdf_import.png?classes=caption "Importare PDF")

Il risultato sostituirà il vostro attuale documento JSesh:

![risultato importazione PDF](jsesh_pdf_import_result.png?classes=caption "risultato importazione PDF")

### NeoOffice (Openoffice) e testo RTF

Questo capitolo descrive le manipolazioni effettuate su un Macintosh utilizzando Neooffice come elaboratore di testi. Funziona anche con Openoffice su Windows e Linux (ma sembra non funzionare con Openoffice 3.1.1 su Mac).

Se configuri l'opzione "taglia e incolla" per utilizzare il formato RTF **e** se scegli **EMF** come formato immagine (vedi sopra), potrai incollare nuovamente i tuoi geroglifici in JSesh.

Per prima cosa, devi selezionare "EMF" come formato di copia da utilizzare.

![Preferenze Copia](cut_and_paste_preferences.png?classes=caption "Preferenze Copia")

Il testo incollato in EMF in Neooffice può essere incollato nuovamente in JSesh:

![Copiare RTF](copy_rtf.png?classes=caption "Copiare RTF")

![Importare RTF](import_rtf.png?classes=caption "Importare RTF")

![Testo RTF importato](import_rtf_result.png?classes=caption "Testo RTF importato")

Ora, c'è un piccolo problema. Vogliamo che Neooffice invii testo RTF (con l'immagine incorporata). Questo non accadrà se selezioni direttamente l'immagine:

![Errata selezione in Neooffice](bad_copy_attempt.png?classes=caption "Errata selezione in Neooffice")

Si noti che nella selezione "buona", l'immagine è contornata in nero.

La selezione diretta di un'immagine comporterà un (innocuo) messaggio di errore:

![Messaggio di errore selezione errata](bad_copy_attempt_result.png?classes=caption "Messaggio di errore selezione errata")

Ora, il modo corretto per selezionare l'immagine è cliccare davanti ad essa nel testo e trascinare con il mouse.
In alternativa (e con meno destrezza), puoi selezionare l'immagine spostando il cursore del testo davanti ad essa e poi premendo "Maiusc" e una delle frecce della tastiera (è molto più semplice farlo che descriverla).

Nota che puoi selezionare più di un'immagine:

![Copie multiple](multi_copy.png?classes=caption "Copie multiple")

E otterrai una riga per immagine in JSesh:

![Importazioni multiple](multi_copy_result.png?classes=caption "Importazioni multiple")

Nota che **questo funziona solo se le tue immagini sono state incollate dalla versione 2.11 o successiva di JSesh e nel formato corretto**.

### Altro

Sarei molto interessato a sapere se altre configurazioni funzionano

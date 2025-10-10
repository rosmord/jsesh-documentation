---
title: Importazione di nuovi glifi
taxonomy:
    category: docs
    tag: []
---

## Scelta di una cartella per i tuoi simboli

Per poter aggiungere nuovi simboli, devi prima scegliere dove verranno salvati sul tuo computer. Per farlo, seleziona Strumenti/Modifica Preferenze.
Nella scheda "Selezione font" (attualmente l'unica disponibile), inserisci la cartella che desideri utilizzare nel campo "Directory font geroglifici". Dovresti creare una cartella vuota per questo scopo specifico.

Creazione di una cartella:

![Creazione di una cartella](glyphDir1.png)


Selezione della cartella
![La cartella è selezionata](glyphDir2.png)


Devi farlo solo una volta. Le successive invocazioni di JSesh useranno questa cartella.

## Allegare codici ai disegni e inserirli in JSesh

Una volta disegnato un segno, o dopo averlo ottenuto dalla [libreria di segni JSesh](https://jsesh.qenherkhopeshef.org/glyphs) o da qualche altra fonte, è il momento di dargli un nome.

Tranne quando si creano segni già documentati nel Manuale di Codifica (ad esempio, perché non sono disponibili in JSesh), è necessario prima ottenere un ID utente, che distinguerà i propri segni da quelli creati da altri utenti.

Per ottenere un uid, registrarsi come utente JSesh. Nota per gli utenti tksesh: l'uid è semplicemente il proprio ID tksesh.

Fare attenzione quando si assegna un nome ai segni. Si desidera che i file siano leggibili da chiunque, quindi attenersi scrupolosamente al *Manuale di Codifica*. I nostri suggerimenti attuali sono i seguenti:

* Se crei la tua versione di un simbolo nel Manuale (perché non è ancora disponibile in JSesh o perché non ti piace il simbolo predefinito fornito), usa il Manuale di codifica standard per il simbolo oppure usa la seguente notazione: `US` + **uid** + `codice Gardiner`, dove **uid** è l'ID utente. Ad esempio, se hai l'ID utente 527834, sarebbe `US527834A1VARA` per una variante di `A1`.

* Quando crei un simbolo che consideri una variante di un simbolo standard, dovresti costruirne il nome in questo modo: **USuid+Codice Gardiner+"VAR"+CODICE VARIANTE** dove:
* Il Codice Gardiner è il codice standard del Manuale di codifica per il simbolo base
* Il CODICE VARIANTE è solitamente una lettera maiuscola.

Ad esempio, la forma tipica di <span class="mdc">wn</span> (E34) in epoca ramesside ha la coda dell'animale Seth. Se voglio distinguerlo dal simbolo "normale", posso chiamarlo `US1E34VARA`.

* Quando il simbolo che crei corrisponde a un simbolo completamente nuovo, assegnagli un codice del tipo: **USuid+Categoria Gardiner + NUMERO +"XT"+CODICE VARIANTE OPZIONALE.**

Sei libero di scegliere il numero che preferisci, ma ti consiglio di provare a trovare una disposizione logica. Sarebbe anche meglio se questo numero non corrispondesse a un segno "standard" (per evitare di confondere gli utenti inesperti di altri software). Ad esempio, puoi iniziare la numerazione da 1000. Nota anche che il numero non deve contenere zeri iniziali. La categoria deve essere corretta e, se proprio non ne hai idea, dovresti usare la categoria Aa. "Ff" è riservato ai segni utilizzati specificamente nella trascrizione ieratica.

Esempio: l'Arpa Louvre E 116 A è stata recentemente pubblicata da C. Barbotin (La voce dei geroglifici, pp. 66-67), e nel suo testo compare il segno sconosciuto ![](./aa1000.png?classes=inline). Posso creare questo segno e assegnargli, ad esempio, il codice US1Aa1000XT. D'altra parte, la Stele d'Israele contiene un segno che molto probabilmente è un grifone, ma non corrisponde a nessun segno di grifone registrato nel manuale <span class="mdc">US1E162VARA</span>. Quindi gli ho assegnato il codice US1E162VARA, perché E162 è un segno di grifone.

* Utilizzo di questo sistema durante l'importazione di testi da altri software: è possibile che altri software forniscano i propri codici "non standard". Se vuoi importare testi da questi software in JSesh, potresti dover dare un nome ai nuovi simboli che contengono (nota che i font sono solitamente protetti dalle leggi sul copyright, quindi dovrai ridisegnare i simboli tu stesso, adattando i simboli JSesh esistenti o trovando un'immagine dei simboli nelle fonti geroglifiche originali). Per motivi di compatibilità, i seguenti codici ID utente possono essere utilizzati per altri software:

| software    | user id substitute |
| ----------- | ------------------ |
| winglyph    | 1000               |
| macscribe   | 1001               |
| inscribe    | 1002               |
| got         | 1003               |
| visualglyph | 1004               |

Se vi vengono in mente altri software che dovrei aggiungere, per favore ditemelo.

* codice standard del manuale di codifica. Troverete questi codici, ad esempio, nel WB di Hannig. Sono disponibili anche diversi elenchi sul web. Tenete presente che utilizzare i codici è una cosa, ma che i segni effettivamente disegnati con i font di altri software sono legalmente protetti. Quindi, dovrete procurarvi le vostre versioni dei segni, sia da fonti reali che ricreandole. Troverete maggiori informazioni sul disegno dei segni nella prossima sezione. Nel nostro esempio, la vostra paperella sostituirebbe quella normale, quindi avrebbe il codice "G39".

Suggeriamo che, se create un segno con un codice Gardiner "normale", gli assegniate anche un codice utente. In questo modo, sarete sicuri di mantenerlo anche se in seguito al software verrà aggiunto un segno con questo codice Gardiner.

Si noti che, per compatibilità con tksesh, supportiamo anche "codici glifi utente" arbitrari. Questi codici corrispondono ai codici che tksesh ha assegnato ai nuovi simboli. I codici dei glifi utente hanno la forma **UG id M mid N sid**, dove id, mid e sid sono numeri. Evitate di usare questi codici per ora.

## Inserimento effettivo del simbolo

## Simboli pronti per JSesh

Il modo più semplice per aggiungere simboli alla tua libreria è creare file SVG delle dimensioni corrette. Dovresti usare una dimensione per l'intero quadrate di 1800px x 1800px. Naturalmente, l'immagine potrebbe essere più piccola se il glifo non occupa un intero quadrate.

JSesh può anche usare simboli con una dimensione base del quadrate di 18px, ma ti consiglio di evitarlo.

Il tuo file SVG dovrebbe avere un nome che corrisponda a un codice (ad esempio, `US1A1VARA.svg`).

In questo caso, puoi semplicemente copiare il file nella cartella JSesh Hieroglyphic e il simbolo sarà disponibile.

## Sistema alternativo

Esiste anche un sistema secondario, che può aiutare a ridimensionare i simboli e a scegliere un nome corretto. Ammetto di non averlo usato per anni.

L'interfaccia di importazione dei simboli può essere avviata dal menu Strumenti/Aggiungi nuovi simboli.

L'importazione dei simboli avviene in due fasi:

* si importa un'immagine o un set di immagini da un file (disegni SVG, font TrueType, ecc.)

* si assegna un codice a ogni simbolo importato, quindi si inserisce il nuovo simbolo nell'elenco dei simboli di JSesh.

![Interfaccia di importazione nuovi simboli](importSigns1.png)

### Importazione di disegni

Importare disegni è semplice. JSesh può leggere:

* font TrueType
* file .tml e bzr, che possono essere creati con il predecessore di JSesh, tksesh.
* File SVG

Basta cliccare sul pulsante "Importa file" e selezionare il file che contiene le tue immagini. Puoi utilizzare i pulsanti di navigazione (quelli con le frecce) per sfogliare i simboli disponibili.

### Assegnare un nome al simbolo

Dovete quindi assegnare un nome al simbolo. JSesh cercherà di indovinare un nome dal nome del file, ma potrebbe sbagliarsi.

**Nota** Assegnare un nome non significa che il simbolo sia stato salvato nella vostra libreria. Non viene fatto nulla finché non avete premuto il pulsante Inserisci.

### Ottimizzare i simboli

In alcuni casi, le dimensioni o l'orientamento dei simboli non saranno corretti. Ad esempio, nell'immagine qui sotto, l'anatra è troppo grande e il suo orientamento è errato.

![Ottimizzazione](./importSigns2.png)

È possibile correggere questo problema:

* i pulsanti ![](./importSigns3.png?classes=inline) e ![](importSigns4.png?classes=inline) possono essere utilizzati per modificare l'orientamento del simbolo;
* il pulsante "Altezza completa" imposta il simbolo sulle stesse dimensioni del simbolo A1;
* Se clicchi sulla finestra del simbolo e trascini il mouse, la posizione del mouse imposterà l'altezza del simbolo.

![Inserimento del simbolo a forma di anatra come UG1M2N0](importSigns5.png)

Quando il simbolo è pronto, **clicca sul pulsante Inserisci**. In caso contrario, non accadrà nulla.

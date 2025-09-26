---
title: Editare con il mouse
taxonomy:
    category: docs
---

La modifica con il mouse è un processo semplice ma lento. In genere, viene combinato con altri metodi di modifica.

## Impostazione della posizione del cursore

Per impostare la posizione del cursore, clicca sul pannello dei geroglifici nel punto in cui desideri posizionarlo.

## Inserimento dei simboli tramite menu e palette

Il modo più veloce per inserire i simboli è utilizzare la tastiera (fare riferimento alla sezione “Modifica tramite tastiera”) e digitare i codici Manuel de Codage o le traslitterazioni. Tuttavia, i simboli possono anche essere selezionati da un menu o dalla palette dei simboli.

### Il pulsante simboli

Il pulsante simbolo elenca solo i simboli originariamente elencati nella grammatica di Gardiner, inclusa una categoria aggiuntiva “Ff” per i simboli derivati dalla scrittura ieratica. Questo pulsante si trova nella parte inferiore della finestra JSesh.

### La palette dei simboli

La palette dei simboli è stata creata per offrire una soluzione migliore rispetto al menu. Visualizza tutti i simboli disponibili e fornisce opzioni di ricerca avanzate.

Per aprire la palette dei simboli, utilizzare il menu `Strumenti/Nascondi Mostra palette geroglifica`.

L'utilizzo di base della palette è piuttosto semplice: selezionare la famiglia di simboli di interesse (utilizzando l'elenco a discesa (b)), quindi fare doppio clic sul segno che si desidera inserire nel pannello (e).

Non tutti i simboli vengono visualizzati (normalmente, la palette non mostra i simboli varianti). Per visualizzare tutti i segni di una famiglia, selezionare la casella “Mostra tutto” (h).
Cliccando una sola volta su un simbolo, questo verrà selezionato. Le informazioni sul simbolo (codice, valori, ecc.) verranno visualizzate nel pannello (i). Ulteriori informazioni saranno disponibili selezionando la scheda "Descrizione simbolo" (a).

Si prega di notare che la maggior parte delle informazioni contenute in JSesh sono qui a scopo di ricerca. In particolare, i dettagli sul significato dei valori non sono visualizzati completamente. Ad esempio, utilizziamo “bin” come valore per G37, ma solo perché è un mnemonico conveniente. In realtà, il formato interno di JSesh consente di memorizzare maggiori informazioni sui valori. Un altro esempio è Y1; per questo, manterremo il mnemonico “sS” e aggiungeremo il probabilmente migliore ‘sXA’. Ulteriori informazioni scientifiche sul segno saranno incluse nella “Descrizione del segno” (che al momento è piuttosto vuota).


![Sign Palette](palette_en.png)


#### Controlli avanzati

b
: Il "selettore di famiglia" contiene due famiglie speciali: "palette utente" e "ultimi segni utilizzati". Vedi sotto per maggiori informazioni sulla palette utente. "Ultimi segni utilizzati" contiene tutti i segni selezionati dall'utente nella palette durante questa sessione. Dovrebbe essere utile se gli stessi segni compaiono spesso.

c
: Il controllo "sottofamiglia" consente di limitare l'elenco ai segni che condividono determinate caratteristiche. Ad esempio, se si è selezionata la famiglia "Dio", è possibile limitare la ricerca alle divinità "con la testa di falco".

d
: Il filtro di traslitterazione consente di cercare i segni utilizzando la loro traslitterazione. La traslitterazione utilizzata può essere il valore fonetico di un segno (per fonogrammi e ideogrammi), oppure un valore tipico di una parola in cui appare il segno. Se si seleziona la casella "mostra tutto", verranno utilizzati tutti i valori noti a JSesh (DA COMPILARE).

f
: Selettore della palette utente. Se si seleziona questa casella, il segno attualmente selezionato verrà aggiunto alla palette utente.

g
: Se si clicca sul pulsante "parte di", JSesh visualizzerà tutti i segni che contengono il segno attualmente selezionato (se lo sa). In futuro, potrebbe utilizzare la casella "seleziona tutto" per scegliere fino a che punto andare. Ogni ulteriore clic estenderà l'insieme dei segni visualizzati (il successivo elencherà parti, parti di parti, ecc.)

j
: seleziona varianti note del segno corrente. Il termine "variante" è qui usato in modo piuttosto generico. Potrebbe trattarsi di vere e proprie
varianti linguistiche (ad esempio, Z7 è una variante di G43), oppure potrebbe significare "segni che sono graficamente basati su un altro". Ad esempio, A17A è una variante di A17 in questo senso, anche se i suoi usi linguistici sono piuttosto diversi. Ogni ulteriore clic estenderà l'insieme. Un secondo clic aggiungerebbe una variante di varianti, ecc.

#### Palette utente

La palette utente consente all'utente di comporre il proprio elenco di simboli preferiti. Aggiungere un simbolo alla palette è semplice: basta selezionarlo e selezionare il controllo "palette utente" (f) nella parte inferiore della palette. Il contenuto della palette utente viene salvato automaticamente, quindi la palette verrà ripristinata al successivo avvio di JSesh. Rimuovere un simbolo dalla palette è semplice: basta selezionarlo e deselezionare il controllo "palette utente".

Tutti i simboli selezionati per l'inclusione nella palette utente verranno visualizzati quando si seleziona la famiglia speciale "palette utente".

#### Puoi aiutare

Troverete una descrizione dei file utilizzati dalla palette in appendice a questa documentazione. Se avete una buona conoscenza dei geroglifici, potete contribuire a migliorare JSesh estendendo le informazioni che utilizza. Contattate l'autore (serge.rosmorduc AT qenherkhopeshef.org) per ulteriori informazioni.

### Aggiungere un simbolo selezionato da un menu

Il menu dei geroglifici semplificato consente di accedere ai simboli dell'elenco Gardiner standard. Basta selezionare un segno e verrà aggiunto alla posizione del cursore.

È possibile accedervi cliccando sul pulsante "geroglifici di base" nella parte inferiore della finestra di JSesh.

## Selezione di una zona

La selezione si trova tra il cursore e il cosiddetto segno. L'intera selezione è disegnata in azzurro. Alcune operazioni sono possibili solo se è selezionata una zona di testo.

Per selezionare una zona di testo, è possibile utilizzare diversi metodi:

* Stile Mac: Maiusc + clic su un punto del testo; verrà selezionato tutto il testo tra questo punto e il cursore;
* Stile Unix: lo stesso, ma con il tasto destro del mouse. Questo potrebbe cambiare in futuro se decidessi di utilizzare i menu contestuali.
* Selezione da tastiera: Maiusc + freccia sinistra o destra seleziona e sposta.
* Trascinamento del mouse

## Raggruppamento dei simboli

Questo si fa utilizzando il menu "Manipolazione del testo". È possibile raggruppare i simboli in gruppi verticali o orizzontali, selezionando i simboli (o i quadranti) e scegliendo "Raggruppa orizzontalmente" o "Raggruppa verticalmente". Si noti che è possibile suddividere i gruppi con il menu "Esplodi gruppo". Tutti i tipi di gruppi possono essere "esplosi".

"Raggruppa orizzontalmente" ha la scorciatoia da tastiera "Ctrl-h"

"Raggruppa verticalmente" ha la scorciatoia da tastiera "Ctrl-g"

## Legature

JSesh conosce diversi "gruppi speciali", o legature, che vanno oltre le capacità dei quadranti "quadrati". Ad esempio, "w" e "t" saranno probabilmente disposte in questo modo: ![](w_and_t.png?classes=inline). Per ottenere questo tipo di disposizione, seleziona i simboli che vuoi legare e usa il menu Manipolazione del testo/Elementi di legatura.

Tuttavia, JSesh non sa come legare tutti i gruppi, anche se ne conosce alcuni piuttosto "sportivi": legatura
![](stp_n_ra1.png?classes=inline) gives ![](stp_n_ra2.png?classes=inline).

### Legature complesse

Alcune legature possono essere considerate come la legatura di un segno e di un gruppo.

Consideriamo il gruppo ![](mr_xAswt.png?classes=inline). Può essere inteso come una legatura tra il segno <span class="mdc">F20</span> e il gruppo <span class="mdc">xAst:xAst:xAst</span>. Tali legature possono essere create tramite i menu "Manipolazione testo/Gruppo legature con geroglifico" o "Manipolazione testo/Gruppo legature con geroglifico". Nel primo caso, il gruppo è "davanti" al geroglifico, nel secondo caso (che corrisponde al nostro esempio), il geroglifico è "davanti" al gruppo.

Per ogni segno, JSesh cerca di trovare due aree. Una per le legature "anteriori" e una per le legature "posteriori". Alcuni simboli hanno la loro "area di legatura" già impostata. Per altri simboli, viene calcolata automaticamente. A dire il vero, JSesh prova a vedere se riesce a inserire un rettangolo nell'area in basso a sinistra dei simboli (per l'orientamento da sinistra a destra). Quest'area sarebbe l'area di "inizio". Per l'area di "fine", vengono esaminati due punti. Innanzitutto, l'angolo in alto a destra dei segni (come nella legatura), e poi un'ampia area in basso a sinistra, come nel caso.
Il creatore di segni può fornire altre aree, come in ![](Hm_kA.png?classes=inline).

Si noti che un segno può essere legato contemporaneamente a un gruppo prima e a un gruppo dopo.

## Modifica dei gruppi

Quando si incontra un gruppo molto specifico, di tipo unico, in cui si desidera posizionare i segni esattamente dove si desidera, è possibile selezionare la voce di menu "Modifica gruppo". Il gruppo modificato sarà il gruppo selezionato, se è presente una selezione (evidenziata in blu), oppure l'ultimo gruppo prima del cursore, se non è presente alcuna selezione.

Si aprirà la seguente finestra:

![Editor dei gruppi](groupEditor_it.png "Editor dei gruppi")

Potrai spostare i simboli, ridimensionarli e ruotarli. Nota che il ridimensionamento e la rotazione sono attivati ​​da due pulsanti. Per spostare un cartello, cliccaci sopra e trascinalo dove vuoi. Per ruotarlo o ridimensionarlo, clicca e trascina uno dei piccoli riquadri rossi attorno al cartello attualmente selezionato.

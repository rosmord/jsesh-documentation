---
title: Appendice B: il file di descrizione dei simboli
taxonomy:
    category: docs
    tag: []
---

Attenzione: contenuto tecnicamente esplicito. Anime pure, distogliete lo sguardo. È stato creato un sistema più intuitivo.

In alternativa, potete modificare direttamente il file di descrizione del file. Per farlo, vi serve un editor semplice: il Blocco note potrebbe funzionare su Windows, mentre software come TextWrangler possono essere utilizzati su Mac OS X. I file XML sono composti da testo normale.

JSesh non accetta file malformati, quindi potreste non riuscire ad avviarlo. In questo caso, correggete signs_definition.xml o rinominatelo in modo che venga ignorato. In futuro aggiungerò un editor intuitivo, ma non lo farò finché il formato non sarà completamente definito.
Il file deve avere il seguente formato:

~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE signs PUBLIC "-//ORG/QENHERKHOPESHEF//DTD SIGNDESCRIPTION 1.0" "sign_description.dtd">
<signs>

<!-- qui le definizioni dei tuoi simboli -->

</signs>
~~~

IÈ importante avere esattamente questo contenuto, in particolare la riga DOCTYPE.

Ecco un piccolo esempio (in realtà, una parte del file di descrizione dei simboli standard di JSesh). Questo file descrive i simboli C1 e C1A. Come potete vedere, sono classificati in diverse categorie. Sono entrambi divinità con testa umana e personaggi seduti. Viene fornita la traslitterazione di C1. Ne abbiamo fornita una anche per C1A. Il codice ''"relevance='1'"'' significa che questa traslitterazione è qui solo a scopo informativo. In realtà, il formato XML è stato preparato per ospitare molti dati diversi, il che non è ancora realmente utilizzato da JSesh, e sono molto interessato a ricevere suggerimenti al riguardo. La definizione del formato (il suo "dtd") è fornita subito dopo questa appendice.

~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE signs PUBLIC "-//ORG/QENHERKHOPESHEF//DTD SIGNDESCRIPTION 1.0" "sign_description.dtd">
<signs>

<!-- Poiché C è attualmente la parte più completa dei font JSesh, cerchiamo di coprirla in modo completo. -->

<tagCategory tag="human-headed deity" label="human-headed deity"/>
<tagCategory tag="hawk-headed deity" label="hawk-headed deity"/>
<tagCategory tag="ibis-headed deity" label="ibis-headed deity"/>
<tagCategory tag="ram-headed deity" label="ram-headed deity"/>

<sign sign="C1">
 <hasTranslitteration sign="C1" translitteration="ra"/>
 <hasTag tag="human-headed deity"/>
 <hasTag tag="seated"/>
 <contains partCode="N6"/>
</sign>

<sign sign="C1A">
 <similarTo baseSign="C1"/>
 <hasTranslitteration translitteration="ra" relevance="1"/>
 <hasTag tag="human-headed deity"/>
 <hasTag tag="seated"/>
 <contains partCode="N6"/>
 <contains partCode="S40"/>
</sign>
</signs>
~~~

Si noti che i tag devono essere definiti prima di essere utilizzati (come tagCategory). Un tag ha un nome e un'etichetta; è effettivamente possibile definire etichette in più lingue, sebbene questa funzionalità non sia attualmente utilizzata da JSesh.

## DTD per la descrizione dei simboli

Per i più tecnici, ecco l'attuale DTD utilizzato per le descrizioni dei simboli. È ancora sperimentale ed è già stato modificato dalla versione 2.4.13.

~~~xml
<!-- DTD utilizzato per descrivere le caratteristiche dei simboli. -->
<!-- CATALOG NAME : "-//ORG/QENHERKHOPESHEF//DTD SIGNDESCRIPTION 1.0" --> 

<!ENTITY % signInfo "variantOf|hasTransliteration|partOf|contains|signDescription|isDeterminative|hasTag|phantom"
>

<!ELEMENT signs (sign|determinativeCategory|tagCategory|tagLabel|%signInfo;)*>

<!-- L'elemento sign è facoltativo, ma consente di avere un file meglio strutturato. -->

<!ELEMENT sign (%signInfo;)* >

<!ATTLIST sign
    sign CDATA #REQUIRED
 alwaysDisplay (y|n) 'n'
>

<!--
La nozione di variante qui utilizzata è in qualche modo ad hoc.
Il problema delle varianti è che dietro di essa si celano due nozioni diverse, entrambe utili nel nostro software.
La prima nozione è quella di variante LINGUISTICA. Un simbolo è una variante linguistica di un altro se ha gli stessi usi.
Ad esempio, Y2 è una variante linguistica di Y1. Ora, anche Y2 "assomiglia" a Y1. La chiameremo "variazione grafica".
Entrambe le nozioni sono indipendenti, sebbene statisticamente collegate. Ad esempio, Z7 è una variante linguistica di G43, ma non una
sua variante grafica.

La nozione di "assomigliare" a un altro simbolo è coperta dall'attributo "isSimilar".

In molti casi, soprattutto per i determinativi, i segni non sono sempre completamente sostituibili tra loro.
Per consentire l'uso di informazioni sulle "varianti" nelle ricerche, introduciamo l'attributo "linguistico".

Sia B una variante di A.
"pieno" significa che tutti gli usi di B sono anche possibili usi di A, e tutti gli usi di A sono usi di B.
"altro" significa che B è più specifico di A, o che il grado è sconosciuto.
"parziale" significa che gli usi di A e B si intersecano, ma hanno anche usi significativamente diversi.
Ad esempio, il simbolo D36 (ayin) è una variante parziale di D37 (di), poiché D36 può scrivere "di". Tuttavia,
in questo caso, non considererei D37 come una variante di D36, perché causerebbe più danni che benefici.
"no" si usa quando il simbolo non è affatto una variante linguistica. In questo caso, isSimilar è normalmente "y".

-->

<!ELEMENT variantOf EMPTY>
<!ATTLIST variantOf
 sign CDATA #IMPLIED
 baseSign CDATA #REQUIRED
 isSimilar (y|n) 'y'
 linguistic (full|partial|other|no|unspecified)  'unspecified'
>



<!ELEMENT hasTransliteration EMPTY>
<!-- Lo scopo principale della traslitterazione è aiutare a trovare un simbolo. -->
<!-- Ulteriori informazioni utili qui -->
<!--
L'attributo "use" spiega dove sarà visibile la traslitterazione in JSesh.
'keyboard' significa che il simbolo è tipico di questa traslitterazione, ovvero dovrebbe essere utilizzato nel software principale quando si usa "space" per spostarsi tra i possibili segni.
'palette' significa che il simbolo è un valore non troppo insolito per una data traslitterazione.
Dovrebbe essere accessibile tramite la palette.
'informative' significa che il valore è qui solo a scopo informativo.

type consente di specificare da dove proviene il valore. Potrebbe essere che un simbolo sia un vero e proprio fonogramma (ad esempio G1 per aleph), un ideogramma, un'abbreviazione o semplicemente tipico di certe parole (ad esempio, "bin" non è un valore reale per G37, ma è tipico. G37, tuttavia, è un'abbreviazione nota per Sri).
-->

<!ATTLIST hasTransliteration
 sign CDATA #IMPLIED
 transliteration CDATA #REQUIRED
 use (keyboard|palette|informative) 'keyboard'
 type (phonogram|ideogram|abbreviation|typical) 'phonogram'
>

<!ELEMENT hasShape EMPTY>
<!ATTLIST hasShape
 sign CDATA #IMPLIED
 shape (tallNarrow|lowBroad|lowNarrow) #REQUIRED
 order CDATA #IMPLIED
>

<!ELEMENT partOf EMPTY>
<!ATTLIST partOf
 sign CDATA #IMPLIED
 baseSign CDATA #REQUIRED
>

<!-- Più facile da usare (e da dichiarare) rispetto a isPartOf -->

<!ELEMENT contains EMPTY>
<!ATTLIST contains
 sign CDATA #IMPLIED
 partCode CDATA #REQUIRED
>


<!ELEMENT determinativeCategory EMPTY>
<!ATTLIST determinativeCategory
 category CDATA #REQUIRED
 lang NMTOKEN 'en'
 label CDATA #REQUIRED
>

<!ELEMENT isDeterminative EMPTY>
<!ATTLIST isDeterminative
 sign CDATA #IMPLIED
 category CDATA #REQUIRED
>

<!ELEMENT hasTag EMPTY>
<!ATTLIST hasTag
 sign CDATA #IMPLIED
 tag CDATA #REQUIRED
>

<!-- Dichiara un tag (senza alcuna etichetta) -->
<!ELEMENT tagCategory (tagLabel)*>
<!ATTLIST tagCategory
 tag CDATA #REQUIRED
>

<!-- Dichiara un'etichetta per un tag. -->
<!ELEMENT tagLabel EMPTY>
<!ATTLIST tagLabel
 tag CDATA #IMPLIED
 lang NMTOKEN 'en'
 label CDATA #REQUIRED
>

<!-- descrizione del segno, in formato manuel de codage.
- lang può essere usato per descrivere la lingua. Usa "fr" per il francese, "de" per il tedesco...
-->
<!ELEMENT signDescription (#PCDATA)>
<!ATTLIST signDescription
 sign CDATA #IMPLIED
 lang CDATA 'en'
>

<!-- Un phantom è un codice ridondante. Indica che un dato codice è l'esatto equivalente di un altro.
Questo può essere utilizzato per scopi di normalizzazione. Ad esempio, ci sono alcuni segni che hanno codifiche diverse
in winglyph, JSesh e Inscribe. L'uso di phantom a) evita di avere più segni
e b) consente di creare un testo normalizzato.
-->

<!ELEMENT phantom EMPTY>
<!ATTLIST phantom
 baseSign CDATA #REQUIRED
 existsIn CDATA 'jsesh'
>
~~~

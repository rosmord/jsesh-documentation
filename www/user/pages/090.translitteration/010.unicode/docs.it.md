---
title: Utilizzo di Font UNICODE
taxonomy:
    category: docs
    tag: []
---

Per utilizzare un font Unicode, è necessario disporre di un font con i segni corretti. Troverete [una pagina sulla traslitterazione](https://jsesh.qenherkhopeshef.org/fr/varia/transliteration) sul sito web di JSesh; [Daniel Werning](https://aaew.bbaw.de/egyptological-unicode-fonts) gestisce un elenco simile, che potrebbe essere più aggiornato.


![](fontsprefsunicodetranslit.png)

- Si dovrebbe aprire il menu "Preferenze" (su Mac, si trova nel menu "JSesh"; altrove, nel menu "Modifica").
- Si va alla scheda "Preferenze font".
- Si seleziona un font per la traslitterazione
- Si apre il pannello "Mostra opzioni" e seleziona "Font di traslitterazione Unicode"

## Problemi attuali con i font Unicode

L'attuale supporto per i font di traslitterazione nei sistemi operativi e nei software non è buono. Anche Java su Mac, e quindi anche JSesh, presenta problemi.

I veri problemi sono H̱ e yod

### H maiuscola

Su alcuni sistemi, la H (come nell'accento ariete *H̱nmw*) viene visualizzata male. Dipende dal font **e** dal software **e** dal sistema. Nella maggior parte dei casi, è accettabile. Un'eccezione fastidiosa è che non dà un buon risultato con JSesh **su Mac OS X**. A quanto pare, il sistema di rendering offre risultati migliori su Windows. Nota che se incolli il testo in un word processor, probabilmente otterrai comunque un buon risultato.

### Yod

**obsoleto - aggiungi il codice A7BC**.

Unicode offre diverse opzioni. Ho selezionato le due soluzioni migliori (la terza, che utilizza una sorta di semicerchio dell'accento yod, riproduce semplicemente un trucco usato quando si usavano le macchine da scrivere e si scrivevano a mano gli yod con le lettere "c"). Il problema è che, tecnicamente, il supporto per queste soluzioni è carente.

Lo yod dovrebbe essere codificato con una "i" (una i con il punto, non senza) e un accento. Il font dovrebbe contenere informazioni sufficienti per visualizzare correttamente questi segni. Il problema è che molti software non analizzano il contenuto del font e lavorano in autonomia. Il risultato è che il punto non viene rimosso su molti sistemi (incluso JSesh su Mac). Il posizionamento dell'accento davanti alla "I" maiuscola è un altro problema.

Con una configurazione corretta, è possibile ottenere buoni risultati con OpenOffice e Word.

Le due possibilità per yod sono:

- U+0313 Poiché i + "virgola sopra" è già utilizzato in altre lingue, le sue probabilità di essere supportato correttamente sono maggiori. L'unico problema è che nella visualizzazione normale di questa combinazione per la "I" maiuscola, l'accento dovrebbe essere sopra la I. Come sapete, la visualizzazione corretta per yod maiuscola prevede l'accento davanti alla "I". Se potete conviverci, questa soluzione è la più sicura. Offre buoni risultati nella maggior parte dei casi (ma non con Java e Mac OS X, quindi la visualizzazione di JSesh su Mac non è corretta).

- U+0486 Questo accento ha l'interessante caratteristica di non essere utilizzato per nient'altro sulle lettere latine. Quindi un font può posizionarlo liberamente davanti alla "I" maiuscola. In teoria, questa è la soluzione migliore. In pratica, funziona con alcuni software, ma non con tutti. OpenOffice offre buoni risultati, così come il semplice software TextEdit su Mac. Potrei avere successo con Word su Mac abilitando tutte le legature.

JSesh non supporta l'attuale sistema IFAO/Unicode. Questo standard era una "patch" temporanea che utilizzava i simboli Unicode disponibili, realizzata quando non era disponibile alcuna codifica per la traslitterazione egizia.
Ora che "Aleph" e "Ayin" hanno un codice, voglio incoraggiarne (o meglio, imporne) l'uso.

### Riferimenti

* [Articolo di Wikipedia su traslitterazione e Unicode](http://en.wikipedia.org/wiki/Transliteration_of_Ancient_Egyptian)


---
title: Informazioni avanzate in Inkscape
taxonomy:
    category: docs
    tag: []
---

## Introduzione

JSesh dispone ora di un meccanismo di legatura relativamente avanzato, che non è valido quanto quello di RES, ma fornisce risultati ragionevoli nella maggior parte dei casi. In molti casi, JSesh è in grado di "indovinare" dove dovrebbero inserirsi i gruppi legati, ma può anche richiedere un aiuto aggiuntivo. Questo aiuto può essere fornito direttamente nel file SVG del simbolo e abbiamo deciso di utilizzare i meccanismi di Inkscape a questo scopo.

## Zone di legatura

Per ogni simbolo, JSesh cercherà di calcolare due zone di legatura, una per le legature dei gruppi prima del simbolo, l'altra per le legature dei gruppi dopo il simbolo. **Queste zone possono essere calcolate automaticamente**, ma l'autore del simbolo può anche fornirle.

![Il simbolo A17 con le sue due zone di legatura](zones1.png?classes=caption "Il simbolo A17 con le sue due zone di legatura")

Per creare una delle due zone di legatura in Inkscape, procedi come segue:

- crea un rettangolo in cui il gruppo dovrebbe rientrare. Nota che l'intero gruppo verrà ridimensionato per adattarsi a quel punto, quindi disegnalo abbastanza grande. Di solito disegno questi rettangoli in rosso, ma è solo una convenzione.
- apri il menu contestuale del rettangolo (clicca con il pulsante destro del mouse sul rettangolo) e seleziona Proprietà oggetto. Apparirà la finestra delle proprietà oggetto (Figura "Proprietà zona" di seguito). Definisci l'ID come "zona1" o "zona2". Non dimenticare di cliccare sul pulsante Definisci per convalidare la modifica. Cancella anche l'etichetta (ulteriori informazioni su questo argomento nella sezione chiamata "Gravità delle zone di legatura").

Certamente, stiamo usando le informazioni relative a ID ed etichetta in un modo in cui non dovrebbero essere usate. Il motivo è puramente pragmatico. È molto più semplice fare le cose in questo modo, poiché il creatore del simbolo non ha bisogno di conoscere l'organizzazione interna del formato XML.

![](./zoneProperties.png?classes=caption "Proprietà della zona")

## Gravità delle zone di legatura

Il gruppo legato andrà da qualche parte nella zona di legatura. Ma dove esattamente? Può trovarsi al centro dell'area o rimanere su uno dei suoi lati. In effetti, il comportamento dell'algoritmo di layout non è sempre lo stesso. In ![𓅱 e 𓏏 ligatured](./w_and_t.png?classes=inline), la "t" tende a posizionarsi in basso a sinistra dell'area rettangolare. In ![](./Hm_kA.png?classes=inline), il segno U36 <span class="mdc">U36</span> è più o meno centrato, sia orizzontalmente che verticalmente. JSesh consente agli autori di segni di progettare il comportamento delle "zone di legatura", nel modo seguente. Ricordate l'etichetta del paragrafo precedente? Puoi impostarlo su

~~~
gravity:specifiche di gravità.
~~~

dove le specifiche di gravità possono contenere

* `s` o `e` per chiedere al gruppo di attenersi al lato **inizio** o al lato **fine** della zona[^1]. Se non vengono specificati né `s` né `e`, il gruppo verrà centrato orizzontalmente.
* `t` o `b` per chiedere al gruppo di attenersi alla parte superiore o inferiore della zona. Se non vengono specificati né "t" né "b", il gruppo verrà centrato verticalmente.

“Proprietà della zona”, ''gravity:te'' significa che il gruppo che verrebbe legato nella zona1 (davanti al segno "figlio") si attaccherebbe alla parte superiore del rettangolo rosso e rimarrebbe vicino al segno, ad esempio ![](./W_Xrd.png?classes=inline).

[^1]: `start` e `end` sono tratti da M.-J. RES di Nederhof ed evitare l'uso di "sinistra" e "destra", che non sono realmente utilizzabili per i geroglifici.

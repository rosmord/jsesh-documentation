# Sito web per la documentazione su JSesh

(giusto una prova ...)

Il vecchio sito di documentazione di JSesh utilizzava dokuwiki, un software molto valido, ma non molto facile da gestire.

Ho deciso di spostare la maggior parte del mio codice su [grav](https://getgrav.org/), che ritengo sarà più facile da usare per me (ha meno problemi di sicurezza perché non sono presenti funzioni di modifica).

Per prima cosa "tradurrò" tutte le pagine di documentazione JSesh esistenti in markdown e pubblicherò il codice sorgente di questa documentazione su github.

## Aiuto con la documentazione

La documentazione JSesh utilizza file relativamente semplici, nel formato [`markdown`](https://learn.getgrav.org/17/content/markdown).

Per scrivere una traduzione della documentazione, è necessario creare file `.md`, come avviene ad esempio nella cartella `www/user/pages/040.editing/010.mouse`, che è la parte della documentazione relativa all'uso del mouse:

| nome file       | utilizzo                                |
| --------------- | --------------------------------------- |
| docs.es.md      | versione spagnola della pagina          |
| docs.fr.md      | versione francese                       |
| docs.md         | versione predefinita (inglese)          |
| groupEditor.png | un'immagine utilizzate da queste pagine |
| Hm_kA.png       | un'immagine utilizzate da queste pagine |
| mr_xAswt.png    | un'immagine utilizzate da queste pagine |
| palette_en.png  | un'immagine utilizzate da queste pagine |
| stp_n_ra1.png   | un'immagine utilizzate da queste pagine |
| stp_n_ra2.png   | un'immagine utilizzate da queste pagine |
| w_and_t.png     | un'immagine utilizzate da queste pagine |


`.es` e `.fr` sono i codici per la lingua utilizzata. Si possono trovare nella [descrizione di ISO 639](https://en.wikipedia.org/wiki/List_of_ISO_639_language_codes).


Se guardiamo il contenuto di `docs.md`, ad esempio, vediamo

~~~markdown
---
title: Modifica con il mouse // il titolo della pagina, che dovrebbe essere tradotto
author:... se realizzate la traduzione, potete inserire qui il vostro nome...
taxonomy:
    category: docs
---

...

La modifica con il mouse è un processo semplice ma lento. In genere, viene combinata con altri metodi di modifica.

## Impostare la posizione del Cursore (un titolo di secondo livello (diciamo, sezione invece di capitolo)

...

un'immagine :

![Palette dei simboli](palette_en.png)


~~~

Il markdown è piuttosto semplice. È possibile utilizzare la documentazione esistente come guida. In generale, se si traduce la documentazione, si utilizzerà la stessa struttura della documentazione esistente, quindi è possibile:

- copiare il file che si vuole tradurre, aggiungendo il codice della lingua corretta :
  ~~~
    cp docs.md docs.it.md
  ~~~

- modificare il nuovo file sostituendo il testo originale con la sua traduzione.

Si Potrebbero voler tradurre alcune immagini. È abbastanza semplice. Si crea semplicemente una nuova immagine con il contenuto tradotto.

Quindi, nel file markdown, sostituisci il nome dell'immagine originale con quello tradotto.


## Miglioramento del markdown per questo sito

Questo sito consente di :

- aggiungere didascalie alle immagini come questa:
  ~~~markdown
  ![](./tagEditor.png?classes=caption "La finestra di creazione dei tag")
  ~~~

  E'necessario aggiungere `?classes=caption` dopo il nome dell'immagine, poi la didascalia stessa, tra apici.

- usare immagini in linea. Normalmente, le immagini si trovano su una riga a parte. Se si vuole che facciano parte del testo, usare `classes=inline` : 

  ~~~markdown
  ![](./importSigns3.png?classes=inline)
  ~~~

- usare una versione semplificata del *Manuel de Codage* per citare testi geroglifici. Si deve scrivere una sezione `<span>` con classe `mdc`:

  ~~~markdown
  Può essere inteso come una legatura tra il segno <span class="mdc">F20</span> e il gruppo <span class="mdc">xAst:xAst:xAst</span>.
  ~~~

Da tenere presente che l'asterisco `*` ha un significato speciale per il markdown e che potrebbe essere necessario anteporvi il carattere `\`:

~~~markdown
 <span class='mdc'>p\*t:pt</span>
~~~


## Dove sono i file ?

Tutti i file che si potrebbeero dover modificare o copiare si trovano in `www/user/pages`.

Alcuni di essi si chiamano `chapter.md`, altri `docs.md`.

## Esecuzione di una copia locale della documentazione.

Se si desidera realizzare una traduzione nella tua lingua, le pagine si trovano in `user/pages`. Si cercano i file che terminano in `.md`. Per tradurre un file, si crea semplicemente, nella stessa posizione, un file con lo stesso nome, ma con estensione `.LANG.md`, dove LANG è il codice della tua lingua. Potete contattarmi se volete.


~~~bash
cd www
./bin/grav serve
~~~

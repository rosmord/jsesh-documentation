---
title: Editare con la tastiera
taxonomy:
    category: docs
---

## Digitazione di geroglifici

Per inserire i simboli geroglifici utilizzando la tastiera, clicca all'interno della finestra principale (quella che mostra il testo geroglifico vero e proprio, non il campo "Manuel de Codage").

Quando digiti una lettera o un numero nella finestra principale, questo appare nel piccolo pannello situato nell'angolo in basso a sinistra di JSesh. Questo pannello ti consente di inserire i codici "Manuel de Codage" in modo efficiente.


* Molti simboli hanno codici fonetici, che corrispondono alla loro traslitterazione;
* tutti i simboli sono accessibili tramite il loro codice nella grammatica di Gardiner. Per trovare il codice, puoi cliccare sul pulsante "Geroglifici di base" o consultare la palette dei geroglifici.

Una volta digitato il codice, devi convalidarlo. Per convalidare, digita uno qualsiasi tra i caratteri `spazio`, '`:`', '`*`', '`-`', `invio`.

Il simboli verrà aggiunto al testo geroglifico.

I codici fonetici possono corrispondere a più di un simbolo. Ad esempio, iw corrisponde a uno tra <span class="mdc">N18</span>, <span class="mdc">D54</span>, <span class="mdc">E9</span>, <span class="mdc">E14</span> e <span class="mdc">F51</span>. Il simbolo "ufficiale" per iw è <span class="mdc">iw</span>, secondo il *manuel* (una scelta relativamente strana, dato che <span class="mdc">D54</span> sembra più frequente). Tuttavia, potresti voler usare un altro simbolo. In questo caso, è abbastanza semplice: premi la **barra spaziatrice** e il sistema scorrerà le possibilità, una alla volta.

L'ultima scelta verrà mantenuta la prossima volta che digiterai il codice in questa sessione.

### Codici fonetici

I simboli monolitteri hanno i seguenti codici, che vengono utilizzati anche quando si digita la traslitterazione:

| Codice | Lettera   |
| ------ | --------- |
| A      | ꜣ (aleph) |
| i      | ꞽ (yod)   |
| y      | y         |
| a      | ꜥ (ayin)  |
| w      | w         |
| b      | b         |
| p      | p         |
| f      | f         |
| m      | m         |
| n      | n         |
| r      | r         |
| l      | l         |
| h      | h         |
| H      | ḥ         |
| x      | ḫ         |
| X      | ẖ         |
| z      | z         |
| s      | s         |
| S      | s         |
| q      | ḳ         |
| k      | k         |
| g      | g         |
| t      | t         |
| T      | ṯ         |
| d      | d         |
| D      | ḏ         |

W è utilizzato anche per Z7, M per Aa15 e N per S3.

## Raggruppamento dei simboli

Il simbolo digitato durante la convalida può essere utilizzato per raggruppare i geroglifici. Sia 'spazio' che '-`' hanno il semplice effetto di aggiungere il simbolo successivo in un nuovo quadrato.

* '`:`' e '`*`' aggiungeranno il simbolo successivo rispettivamente sotto e accanto all'ultimo simbolo inserito.
* 'invio' ha due conseguenze: convalida un simbolo (se presente) e aggiunge una nuova riga.

Se non è stato inserito alcun codice (ovvero, se si accede alla finestra del codice), il tipo di simbolo di raggruppamento precedente raggrupperà gli ultimi due quadrati. Sembra un po' strano, ma vedrete che è abbastanza naturale. Potete usarlo per raggruppare i simboli in un secondo momento. In realtà, è un comportamento che ho riscontrato inaspettatamente durante la scrittura di TkSesh e che ho mantenuto, perché l'ho trovato utile.

### *Exempli gratia*

Se vuoi digitare la parola <span class="mdc">p*t:pt</span>, puoi:

* digitare 'p', poi '`*`', 't', '`:`', 'pt'
* digitare 'p', 't', poi '`*`', `spazio` (che in un certo senso convalida '`*`'), pt, '`:`' e `spazio`.

---
title: Suggerimenti e trucchi sulla codifica del testo geroglifico
taxonomy:
    category: docs
---


Prima di descrivere il manuel de codage in sé, vorrei fare una o due considerazioni su come si dovrebbe codificare un testo geroglifico.

In genere, si ha una fonte, che potrebbe essere a) una fonte stampata, con geroglifici composti, b) una fotografia o un facsimile accurato del testo originale, oppure c) un geroglifico manoscritto tratto da una pubblicazione egittologica (ad esempio, l'Urkunden).

Bisogna decidere quanto fedele all'originale si debba essere, e non è una questione semplice. Il primo punto è che si può essere certi che **il testo del Manuel de Codage non possa essere un facsimile**, quindi, in un modo o nell'altro, tradirà l'originale. Se il testo è in definitiva un testo ieratico, si sta già creando qualcosa di completamente diverso.

Ora, quando si ha un segno, si dovrebbe cercare la variante più precisa o usarne una in qualche modo standardizzata? Per rispondere a questa domanda, dovresti chiederti se questa variante sia rilevante nel testo e nell'uso che intendi farne. Ad esempio, nei testi canaiani di Sethi I, il pronome di prima persona usa molte varianti di A40 <span class='mdc'>A40</span>. Se intendi che il testo sia destinato allo studio grammaticale, non è molto rilevante. Se ti chiedi se sia un gioco libero di aggiungere diversità al testo, allora potresti prenderti il ​​tempo di codificare le varianti.

Di norma, **se sei un principiante in egiziano**, ti consiglio di codificare il segno "standard", poiché ti costringerà a **leggere il testo, non a copiare i segni**. Il problema che si presenta quando si vuole essere molto precisi è che si trovano molti casi di varianti che comunque non hanno codifica, e si corre il rischio di fuorviare i lettori dando una falsa impressione di accuratezza... e spesso, scegliendo un segno irrilevante che semplicemente sembra quello desiderato.

Quando la fonte è una versione manoscritta di un testo, come nell'Urkunden, bisogna fare attenzione a un punto: a meno che un segno non sia molto particolare, un egittologo di solito disegnerà i suoi glifi nel modo più semplice. Ciò significa, ad esempio, che userà V23A (<span class='mdc'>V23A</span>) invece di V22 (<span class='mdc'>V22</span>), che è il normale segno geroglifico. Bisogna capirlo, e quando la selezione di un segno è semplicemente causata dalla mano dell'autore, renderla con il segno "standard". D'altra parte, quando l'autore ha disegnato una forma di segno molto specifica, potrebbe valere la pena di prestargli maggiore attenzione.

## Codifica dei testi ieratici

La regola di cui sopra è ancora più stringente per i testi ieratici. Non ha senso fare una distinzione tra <span class='mdc'>V23A</span> e <span class='mdc'>V22</span>, poiché entrambi vengono resi allo stesso modo in ieratico!

Ora, ci sono diverse peculiarità dello ieratico che meritano maggiore attenzione. Queste sono state evidenziate da Sir Alan Gardiner nel suo articolo [“The Transcription of New Kingdom Hieratic”, *JEA* 15 (1929), pp. 48-55](https://www.jstor.org/stable/3854012). La resa dei testi ieratici dovrebbe suggerire il modo in cui sono posizionati i segni originali, in modo da consentire al lettore di comprenderne il motivo e di tornare all'originale quando necessario.

JSesh include una serie di segni utili per la resa dei testi ieratici:

| Simbolo                        | Codice| Uso                                                                                                                                                                                                             |
| ------------------------------ | ----- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <span class='mdc'>Ff1</span> | Ff1 | un segno specifico dei testi ramessidi, che funge da una sorta di "carattere jolly". È diverso dal segno Z5 (<span class='mdc'>Z5</span>). È possibile ottenerlo in JSesh digitando "," (virgola) e poi la barra spaziatrice. |
| <span class='mdc'>Ff100</span> | Ff100 | un segno non standard, **riempitore di spazio punto**. Usalo per rappresentare i vari punti che uno scriba può usare, quando non sono una punteggiatura. |
| <span class='mdc'>Ff101</span> | Ff101 | un segno non standard, **riempitore di spazio orizzontale**. Usalo per rappresentare vari segni orizzontali privi di significato che lo scriba può usare per riempire gli spazi vuoti. |

JSesh include anche segni specifici per i numeri nei testi ieratici. In questi testi, il "determinativo" Z1 è spesso più piccolo della "cifra" Z1. Una resa poco accurata potrebbe far sì che <span class='mdc'>h:r-W:ra-Z1-Z1-Z1</span> venga letto come hrw 3, mentre l'originale ha <span class='mdc'>h:r-W:ra-Z1-Ff302</span>, che è chiaramente hrw 2.

## Layout dei simboli

Utilizzate le varie funzionalità di "legatura" di JSesh e **se tutto il resto fallisce** ricorrete all'"editor di gruppo". Inoltre, non perdete tempo cercando di ottenere esattamente le stesse dimensioni e proporzioni dei simboli originali, a meno che non intendiate discuterne.

Alcuni punti interessanti:

Nel gruppo "M17-M17", i simboli dovrebbero spesso essere più vicini di quanto consenta la spaziatura standard di JSesh (in realtà, questo è già stato affermato da Sir A. Gardiner nel catalogo dei suoi font). Se si scrive `i*i:k` (ovvero, due yod raggruppati orizzontalmente e una "k" sotto di essi), il gruppo creato da JSesh è ![](pAyk2.png?classes=inline). Per ottenere il layout migliore: ![](pAyk1.png?classes=inline) è semplice: devi solo legare i due yod (digita "i" "&" "i", ad esempio).

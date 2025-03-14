---
title: Editar con el teclado
taxonomy:
    category: docs
    tag: []
---

## Escribir jeroglíficos

Cuando escribes una letra o un número en la ventana principal, esta letra o número aparece en el pequeño panel inferior izquiero de JSesh. Esto te permite entrar códigos Manuel de Codage.

Muchos signos tienen códigos fonéticos, que se corresponden con su transliteración; Se puede acceder a todos los signos usando el código correspondiente de la gramática de Gardiner. Para encontrar el código, puedes mirar en los menús "jeroglíficos".

Una vez se ha entrado el código, debes validarlo. Para validarlo escribe uno de los signos siguientes: espacio, ':', '*', '-', enter
El signo se añadirá al texto jeroglífico.

Los códigos fonéticos pueden corresponder con más de un signo. Por ejemplo `iw` se corresponde con  <span class="mdc">N18</span>,  <span class="mdc">D54</span>, <span class="mdc">E9</span>,  <span class="mdc">E14</span> y <span class="mdc">F51</span>. El signo "oficial" para iw es <span class='mdc'>iw</span>  de acuerdo con el manuel. Sin embargo, te puede interesar otro signo. En este caso es fácil : pulsa la barra de espacio y el sistema te irá mostrando las posibilidades una a una.

Tu última selección se guardará para la próxima vez que escibas ese código en esa sesión.

## Agrupando signos

El signo que escribas al validar se puede usar para agrupar los jeroglíficos. 'Espacio' y '-' hacen que el signo siguiente se añanda en un cuadro nuevo.

* ':' y '*' añadirán el signo siguiente debajo o al lado respectivamente del último signo entrado.

* 'enter' tiene dos consecuencias : valida el signo (si lo hay) y añade una nueva línea.
* 
Si no se ha entrado ningún código, el signo de agrupación previo agrupará los dos últimos cuadros. Parece un poco extraño, pero verás que es bastante natural. Puedes usarlo para agrupar signo en un momento posterior.

## Exempli gratia

Si quieres escribir la palabra <span class='mdc'>p\*t:pt</span> *p.t*, puedes :

- escribir 'p', luego '*', 't', ':', 'pt'
- escribir 'p', 't', luego '*', espacio (que valida a '*'), pt, ':', y espacio.

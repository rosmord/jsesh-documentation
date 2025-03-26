---
title: Editar con el ratón
author: Martí Blesa
taxonomy:
    category: docs
---

Editar con el ratón es un proceso muy sencillo pero muy lento. Normalmente
lo alternarás con alguno de los otros dos. Puedes hacer esto :

## Marcar la posición del cursor

Para marcar la posición actual del cursor, simplemente haz click en el panel
de los jeroglíficos.

## Seleccionar una zona
La selección está entre el cursor y lo que se llama la marca. Toda la
selección se dibuja en azul claro. Algunas operaciones son sólo posibles
si el texto está seleccionado.

Para seleccionar una zona de texto puedes usar varios sistemas :

- Estilo Mac : haz click mientras pulsas mayúsculas en un punto del texto ; todo el texto entre este punto y el cursor se seleccionará ;
- Estilo Unix : similar pero usándo el botón derecho del ratón. Esto quizá se cambiará un dia si decido usar menús contextuales.
- Selección con el teclado : mayúsculas + flecha izquierda o flecha derecha selecciona y mueve.
- Arrastrando con el ratón

## Añadir un signo escogido de un menú
El menú hieroglyphs te da acceso a los signos de la lista
stándard de Gardiner. Simplemente selecciona un signo y se añadirá en la
posición del cursor.

## Agrupando signos
Esto se hace con el menú "Text manipulation". Puedes agrupar signos en
grupos verticales o horizontales seleccionando los signos (o cuadros), y
seleccionando o bien "group horizontal" o "group
vertical". Puedes romper los grupos con el menú "explode group". Todos los
grupos se puede "exploded".

- "Group Horizontal" tiene el atajo de teclado Ctrl-h
- "Group Vertical" tiene el atajo de teclado Ctrl-g

## Ligaturas
JSesh conoce varios "grupos especiales".

## Editando grupos
Cuando enceuntras un grupo muy específico, uno realmente raro, donde quieres
situar los signos exactamente donde los quieres, puedes seleccionar el menú
edit group. El grupo editado será o bien el seleccionao, si hay
una selección (marcado con una línea azul), o el último grupo antes del
cursor si no hay ninguno seleccionado.
Abrirá esta ventana :

![](./groupEditor.png?classes=caption "El editor de grupos")

Podrás mover los signos, escalarlos y rotarlos. El escalado y la rotación
se activan con dos botones. para mover un signo, pulsa sobre él y arrástralo
dónde lo quieras. Para rotarlo o escalarlo, pulsa y arrastra una de las
pequeñas cajas rojas alrededor del signo seleccionado.

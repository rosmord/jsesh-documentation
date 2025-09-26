---
title: Ottenere il codice
taxonomy:
    category: docs
    tag: []
---


## Ottenere il codice

Il metodo preferito è usare git, con il comando:

~~~bash
git clone https://github.com/rosmord/jsesh.git
~~~

Normalmente, il branch **master** contiene codice aggiornato e compilabile. È l'unico che consiglierei di clonare. Gli altri branch sono:

* produzione: correzioni in corso e piccole modifiche, che verranno applicate al branch master. Si tratta di lavoro in corso, quindi non aspettatevi che compili sempre.
* sviluppo: lavoro in corso per la prossima versione di JSesh
* jfx-test: lavoro per vedere come adattare JSesh a Java FX.

## Compilazione del codice

run :

~~~bash
mvn install    
~~~


Prima di ciò, potresti scegliere quale versione di JSesh vuoi compilare. Sono presenti diverse release. Quindi, potresti fare qualcosa del tipo

~~~bash
  git checkout release-5.3
    mvn clean install    
~~~

per compilare la versione 5.3 di JSesh. tutti i tag possono essere elencati digitando

~~~bash
    git tag
~~~

Se si desidera *eseguire* JSesh, il modulo è **jseshAppli**. L'ultima versione di jsesh-installer fornisce due cartelle, una per Mac e una per Windows, con distribuzioni quasi pronte all'uso. La fase di produzione è attualmente manuale, consultare il file README.md alla radice del progetto JSesh.


Dopo aver eseguito `mvn install`, le librerie JSesh saranno disponibili nel tuo archivio Maven e potrai utilizzarle per i tuoi progetti.

Poi, potrai utilizzare le librerie JSesh nel tuo programma facendo riferimento al file pom.xml.
Ad esempio:

~~~xml
<code>
<dependency>
  <groupId>org.qenherkhopeshef</groupId>
    <artifactId>jseshGlyphs</artifactId>
    <version>5.3</version>
  </dependency>
  <dependency>
    <groupId>org.qenherkhopeshef</groupId>
    <artifactId>jsesh</artifactId>
    <version>5.3</version>
  </dependency>
  <dependency>
  <groupId>org.qenherkhopeshef</groupId>
    <artifactId>qenherkhopeshefUtils</artifactId>
    <version>5.3</version>
  </dependency>                
~~~

Si noti che, da JSesh 6.7 in poi, il groupId verrà modificato in
<groupId>org.qenherkhopeshef.jsesh</groupId>
per semplificare la gestione dei repository Maven (voglio poter rimuovere facilmente tutte le vecchie versioni di JSesh con un semplice comando rm sul mio computer).

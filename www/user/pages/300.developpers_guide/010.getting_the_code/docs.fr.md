---
title: Obtenir le code
taxonomy:
    category: docs
    tag: []
---


## Obtenir le code

La méthode préférée est d'utiliser git, avec la commande :

~~~bash
git clone https://github.com/rosmord/jsesh.git
~~~

Normalement, la branche **master** contient du code à jour et compilable. C'est la seule que je suggère de cloner. Les autres branches sont :

* production : corrections en cours et petits changements, qui seront appliqués à la branche master. C'est un travail en cours, alors ne vous attendez pas à ce qu'elle se laisse compiler tout le temps.
* development : travail en cours pour la prochaine version de JSesh.
* jfx-test : quelques travaux pour voir comment adapter JSesh à JavaFX.

## Compilation du code

Lancez :

~~~bash
mvn install
~~~

Avant cela, vous pouvez choisir la version de JSesh que vous souhaitez compiler. Diverses versions sont étiquetées. Vous pourriez donc faire quelque chose comme :

~~~bash
git checkout release-5.3
mvn clean install
~~~

pour compiler JSesh version 5.3. Tous les tags peuvent être listés en tapant :

~~~bash
git tag
~~~

Si vous voulez *exécuter* JSesh, le module est **jseshAppli**. La dernière version de jsesh-installer fournit deux dossiers, un pour Mac et un pour Windows, avec des distributions presque prêtes. La fin de la construction de la distribution est actuellement manuelle : voir le fichier README.md à la racine du projet JSesh.

Une fois `mvn install` exécuté, les bibliothèques JSesh sont disponibles dans votre dépôt Maven local et vous pouvez les utiliser pour vos projets.

Vous pouvez ensuite utiliser les bibliothèques JSesh dans votre programme en les référençant dans votre fichier pom.xml. Par exemple :

~~~xml
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

Notez qu'à partir de JSesh 6.7, le groupId sera remplacé par `org.qenherkhopeshef.jsesh`, afin de simplifier la gestion des dépôts Maven (je veux pouvoir supprimer facilement toutes les anciennes versions de JSesh avec un simple `rm` sur mon ordinateur).

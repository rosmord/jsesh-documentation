---
title: 'Obtenir le code'
taxonomy:
    category: docs
    tag: []
---

## Obtenir le code

La méthode recommandée est d'utiliser git :

~~~bash
git clone https://github.com/rosmord/jsesh.git
cd jsesh
~~~

La branche **master** contient normalement du code à jour et compilable. Les versions publiées sont étiquetées : `git tag` les liste, et `git checkout` en sélectionne une. Par exemple, pour compiler la version 8.0.8 :

~~~bash
git checkout release-8.0.8
~~~

## Compilation

JSesh nécessite **Java 25**. Il n'est pas nécessaire d'installer Gradle : le projet contient le « wrapper » Gradle (`gradlew`), et Gradle peut télécharger lui-même un JDK adapté (support des toolchains).

Compiler les sources
: `./gradlew build`

Lancer JSesh directement (depuis le dossier racine du projet)
: `./gradlew jseshAppli:run`

Lancer l'éditeur d'information sur les signes
: `./gradlew signInfoAppli:run`

Construire la distribution pour la plateforme courante
: `./gradlew jpackage`. Le résultat se trouve dans `jsesh-installer/build/jpackage`.

Rendre les bibliothèques disponibles pour vos propres projets
: `./gradlew publishToMavenLocal`. Les bibliothèques sont installées dans votre dépôt Maven local (`~/.m2/repository`). Voir [Utiliser JSesh dans votre projet](/developpers_guide/jsesh_8/using_jsesh_in_your_project).

Le numéro de version est défini dans le fichier `gradle.properties`, à la racine du projet (`version=...`).

JSesh peut aussi être chargé dans un IDE (Eclipse, NetBeans, IntelliJ, VSCode) grâce à son support de Gradle.

## Les modules

| Module | Rôle |
|---|---|
| `jsesh` | la bibliothèque principale : analyseur, modèle de document, rendu, composants d'édition |
| `jseshGlyphs` | les polices hiéroglyphiques |
| `jseshAppli` | l'application JSesh |
| `jseshLabels` | les textes des menus, boutons, etc. (pour faciliter la traduction) |
| `jseshSearch` | le module de recherche |
| `jhotdrawfw` | le cadre d'application, adapté de JHotDraw 7 |
| `qenherkhopeshefUtils` | utilitaires divers pour JSesh et les programmes Swing |
| `mdwlexer` | un petit cadre d'analyse lexicale, utilisé par l'analyseur lexical du Manuel de Codage |
| `signInfoAppli` | l'éditeur d'information sur les signes |
| `jsesh-texts` | la bibliothèque de textes |
| `jsesh-installer` | le système de construction des distributions |
| `jseshTests` | petits programmes vérifiant que JSesh fonctionne (utiles seulement si vous travaillez sur JSesh lui-même) |

En tant qu'utilisateur de la bibliothèque, vous aurez surtout besoin de `jsesh` et `jseshGlyphs`.

## Licences

Le code source de JSesh est distribué sous licence [CeCILL-C](https://cecill.info/licences/Licence_CeCILL-C_V1-fr.html), à peu près équivalente à la LGPL. Quelques fichiers utilisent des licences plus permissives (voir leurs en-têtes). Les polices dessinées par Serge J.-P. Thomas peuvent être utilisées avec JSesh, dans des programmes utilisant JSesh comme bibliothèque, et pour des publications, mais pas pour d'autres traitements de texte hiéroglyphiques. Voir le `README.md` du dépôt pour les détails.

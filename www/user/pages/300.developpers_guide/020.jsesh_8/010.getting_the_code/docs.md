---
title: Getting the code
taxonomy:
    category: docs
    tag: []
---

## Getting the code

The preferred way is to use git:

~~~bash
git clone https://github.com/rosmord/jsesh.git
cd jsesh
~~~

The **master** branch normally contains up-to-date and compilable code. Released versions are tagged: `git tag` lists them, and `git checkout` selects one. For instance, to build version 8.0.8:

~~~bash
git checkout release-8.0.8
~~~

## Building

JSesh needs **Java 25**. You don't need to install Gradle: the project contains the Gradle wrapper (`gradlew`), and Gradle can download a suitable JDK by itself (toolchain support).

Building the sources
: `./gradlew build`

Running JSesh directly (from the root folder of the project)
: `./gradlew jseshAppli:run`

Running the sign info editor
: `./gradlew signInfoAppli:run`

Building the distribution for the current platform
: `./gradlew jpackage`. You will find the result in `jsesh-installer/build/jpackage`.

Making the libraries available to your own projects
: `./gradlew publishToMavenLocal`. The libraries are installed in your local Maven repository (`~/.m2/repository`). See [Using JSesh in your project](/developpers_guide/jsesh_8/using_jsesh_in_your_project).

The version number is defined in the `gradle.properties` file at the root of the project (`version=...`).

JSesh can also be loaded in an IDE (Eclipse, NetBeans, IntelliJ, VSCode) with its Gradle support.

## The modules

| Module | Role |
|---|---|
| `jsesh` | the core library: parser, document model, rendering, editor components |
| `jseshGlyphs` | the hieroglyphic fonts |
| `jseshAppli` | the JSesh application |
| `jseshLabels` | the texts for menus, buttons, etc. (to ease translation) |
| `jseshSearch` | the search module |
| `jhotdrawfw` | the application framework, adapted from JHotDraw 7 |
| `qenherkhopeshefUtils` | various utilities for JSesh and Swing programs |
| `mdwlexer` | a small scanner framework, used by the Manuel de Codage lexer |
| `signInfoAppli` | the sign information editor |
| `jsesh-texts` | the text library |
| `jsesh-installer` | the system used to build the distributions |
| `jseshTests` | small programs used to check that JSesh works (only useful if you work on JSesh itself) |

As a library user, you will mostly need `jsesh` and `jseshGlyphs`.

## Licenses

The JSesh source code is distributed under the [CeCILL-C](https://cecill.info/licences/Licence_CeCILL-C_V1-en.txt) license, roughly equivalent to the LGPL. A few files use more permissive licenses (see their headers). The fonts drawn by Serge J.-P. Thomas may be used with JSesh, in programs using JSesh as a library, and for publications, but not for other hieroglyphic word processors. See the `README.md` of the repository for details.

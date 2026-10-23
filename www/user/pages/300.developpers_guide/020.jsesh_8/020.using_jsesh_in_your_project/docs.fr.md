---
title: 'Utiliser JSesh dans votre projet'
taxonomy:
    category: docs
    tag: []
---

## Utiliser JSesh dans votre projet

JSesh 8 est compilé avec Java 25, et ses bibliothèques sont publiées avec le groupId `org.qenherkhopeshef.jsesh`.

Vous aurez probablement besoin de :

- `jsesh`, la bibliothèque principale ;
- `jseshGlyphs`, si vous voulez la police hiéroglyphique standard de JSesh.

Pour l'export SVG, il faut aussi `org.qenherkhopeshef:jvectclipboard`.

Pour l'instant, les bibliothèques JSesh 8 ne sont pas publiées sur Maven Central. Il faut d'abord [les compiler et les installer dans votre dépôt Maven local](/developpers_guide/jsesh_8/getting_the_code) avec `./gradlew publishToMavenLocal`.

## Avec Gradle

~~~gradle
plugins {
    id 'java'
    id 'application'
}

java {
    toolchain {
        languageVersion = JavaLanguageVersion.of(25)
    }
}

ext {
    jseshVersion = "8.+"
}

repositories {
    mavenLocal() // Hopefully the jsesh library is there.
    mavenCentral()
}

dependencies {
    implementation "org.qenherkhopeshef.jsesh:jsesh:${jseshVersion}"
    implementation "org.qenherkhopeshef.jsesh:jseshGlyphs:${jseshVersion}"
    // only if you need SVG export:
    implementation "org.qenherkhopeshef:jvectclipboard:8.1.1"
}
~~~

`8.+` sélectionne la version 8.x la plus récente disponible. Si vous préférez être explicite, utilisez la version indiquée dans le fichier `gradle.properties` de la version de JSesh que vous avez installée (il commence par `version=...`).

Chaque [démo](https://github.com/rosmord/jsesh-demos) contient un `build.gradle` complet dont vous pouvez partir.

## Avec Maven

Les mêmes bibliothèques s'utilisent bien sûr depuis un projet Maven :

~~~xml
<dependency>
  <groupId>org.qenherkhopeshef.jsesh</groupId>
  <artifactId>jsesh</artifactId>
  <version>8.1</version>
</dependency>
<dependency>
  <groupId>org.qenherkhopeshef.jsesh</groupId>
  <artifactId>jseshGlyphs</artifactId>
  <version>8.1</version>
</dependency>
~~~

Utilisez la version que vous avez compilée.

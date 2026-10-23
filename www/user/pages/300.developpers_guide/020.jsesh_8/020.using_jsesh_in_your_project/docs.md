---
title: Using JSesh in your project
taxonomy:
    category: docs
    tag: []
---

## Using JSesh in your project

JSesh 8 is built with Java 25, and its libraries are published with the group id `org.qenherkhopeshef.jsesh`.

You will probably need:

- `jsesh`, the core library;
- `jseshGlyphs`, if you want the standard JSesh hieroglyphic font.

For SVG export, you also need `org.qenherkhopeshef:jvectclipboard`.

As of today, the JSesh 8 libraries are not published on Maven Central. You first have to [build them and install them in your local Maven repository](/developpers_guide/jsesh_8/getting_the_code) with `./gradlew publishToMavenLocal`.

## With Gradle

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

`8.+` selects the most recent 8.x version available. If you prefer to be explicit, use the version found in the `gradle.properties` file of the version of JSesh you installed (it starts with `version=...`).

Each of the [demos](https://github.com/rosmord/jsesh-demos) contains a complete `build.gradle` you can start from.

## With Maven

The same libraries can of course be used from a Maven project:

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

Use the version you built.

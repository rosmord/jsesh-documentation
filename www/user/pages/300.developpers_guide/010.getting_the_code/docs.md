---
title: Getting the code
taxonomy:
    category: docs
    tag: []
---


## Getting the code

The preferred way is to use git, with the command:

~~~bash
git clone https://github.com/rosmord/jsesh.git
~~~

Normally, the **master** branch contains up-to-date and compilable code. It's the only one I would suggest to clone. Other branches are

* production: ongoing fixes and small changes, which will be applied to the master branch. That's ongoing work, so don't expect it to compile all the time.
* development: ongoing work for next version of JSesh
* jfx-test: some work to see how to adapt JSesh to Java FX. 

## Compiling the code

run :

~~~bash
mvn install    
~~~


Before that, you might choose which version of JSesh you want to compile. Various releases are tagged. So, you might  do something like 

~~~bash
  git checkout release-5.3
    mvn clean install    
~~~

to compile JSesh version 5.3. all tags can be listed by typing 

~~~bash
    git tag
~~~

If you want to *run* JSesh, the module is **jseshAppli**. The latest version of jsesh-installer provides two folders, one for Mac and one for Windows, with almost ready distributions - the end of the production-building is currently manual, see README.md at the root of the JSesh project.


When you have run `mvn install`, the Jsesh libraries are available in your own maven archive and you can use them for your projects.


Then, you can use the JSesh libraries in your program by referencing the in your pom.xml. 
For instance:

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

Note that, from JSesh 6.7 onward, the groupId will be changed to 
      <groupId>org.qenherkhopeshef.jsesh</groupId>
in order to simplify maven repositories management (I want to be able to easily remove all old versions of JSesh with a simple rm on my computer)

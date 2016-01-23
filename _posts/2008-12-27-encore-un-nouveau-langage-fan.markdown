---
author: grozeille
comments: true
date: 2008-12-27 22:58:24+00:00
layout: post
excerpt_separator: <!--more-->
slug: encore-un-nouveau-langage-fan
title: 'Encore un nouveau langage : FAN'
wordpress_id: 120
categories:
- Developpement
tags:
- .Net
- java
---

En lisant un article d'introduction du [langage FAN](http://www.fandev.org/) je trouve intéressant que ce dernier soit compatible .NET et Java.
En ce moment, .Net se voit enrichir de nombreux langages, aussi bien statiques ([F#](http://www.programmez.com/actualites.php?id_actu=3985) par exemple) que dynamiques ([Iron Python](http://www.codeplex.com/IronPythonStudio)). Les langages "standards" étant C#, VB.Net et C++/CLI.
Quand on développe sur la JVM, le langage "standard" reste Java. Mais cela ne veut pas dire qu'on a pas le choix : [Scala](http://www.scala-lang.org/), [Jython](http://www.jython.org/Project/), [Groovy](http://groovy.codehaus.org/)...

![aa496123net_logoen-usmsdn10](http://grozeille.files.wordpress.com/2008/12/aa496123net_logoen-usmsdn10.gif) + ![java_logo](http://grozeille.files.wordpress.com/2008/12/java_logo.gif?w=188) = FAN ?

<!--more-->

Mais le petit nouveau, FAN, cible aussi bien la JVM que la CLR.Net. Certes, les 2 mondes possèdent des concepts similaires, mais aussi très différents et qui risque de ne pas être possible d'exposé dans ce langage.
Ceci dit, la plupart des concepts sont haut-niveaux, et peuvent donc générer un bytecode en utilisant des concepts plus simples et bas niveau, comme un `foreach` peut être écrit sous la forme d'un `for`...

En l'occurrence, FAN introduit un concept déjà existant en C# mais absent en Java : les Nullables.
C'est l'objet de [cet article](http://www.jroller.com/scolebourne/date/20081023).

De nombreuses autres sucreries du langages C# sont introduites dans le JVM à l'aide de FAN comme les Closures. Je vous laisse découvrir tout ça sur [la documentation officielle](http://www.fandev.org/doc/docLang/index.html).
Je vous invites aussi à lire [cet autre article d'introduction](http://www.jroller.com/scolebourne/date/20080612) qui expose beaucoup d'avantages.

Pour ma part, j'adore :




  * gestion des `nullable`


  * valeur par défaut des arguments des méthodes (ce qui évite plein de surcharge inutile)


  * `property` implicite à la C#, pour toujours moins de code à écrire


  * `closure` en Java


  * pas de `;` superflux en fin de ligne


  * l'équivalent du mot clé `dynamic` du C#4 avec `object->variable` !


  * mot clé `once` qui évite de gérer manuellement le caching du résultat (genre : `if(truc == null) truc = new Truc(); return truc;")`


  * l'écriture des listes/maps et l'écriture des instanciations "à la JSON"


A noter aussi une gestion de "package" propre au langage, et qui n'expose pas toute l'API Java (JDK). Je n'ai pas trouvé d'infos concernant .Net à ce sujet, mais ce langage se veut vraiment comme une union des 2 mondes.

En attendant un pluggin Eclipse ou un addin VisualStudio Shell, ils livrent un mini IDE fort sympathique.

![flux](http://grozeille.files.wordpress.com/2008/12/flux.png?w=300)![](/DOCUME~1/mathias/LOCALS~1/Temp/moz-screenshot-1.jpg)

Et vous? Qu'en pensez-vous?

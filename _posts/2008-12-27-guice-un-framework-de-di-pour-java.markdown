---
author: grozeille
comments: true
date: 2008-12-27 23:39:16+00:00
layout: post
slug: guice-un-framework-de-di-pour-java
title: 'GUICE : un framework de DI pour Java'
wordpress_id: 130
categories:
- Developpement
tags:
- .Net
- IOC
- java
- spring
---

Je pense que la [Dependency Injection](http://en.wikipedia.org/wiki/Dependency_injection) est une valeur fondamentale à l'écriture d'un programme, et je l'utilise tous les jours.
Je suis un adorateur (voir expert) de [Spring](http://www.springsource.org/about)/[Spring.Net](http://www.springframework.net/), et j'affectionne l'écriture de la  structure du programme en XML.

Mais cette technique est très largement contestée :



	
  * nécessite un éditeur XML "intelligent" (ce qui est le cas grâce à  [SpringIDE](http://springide.org/blog/)) pour la complétion de la structure mais aussi des types.

	
  * interprétation au Runtime, et donc erreurs potentielles découvertes  qu'au dernier moment.

	
  * verbeux

	
  * mauvaises performance (lecture du XML...)


Ça a aussi ses avantages, c'est pour ça que je reste adorateur de  Spring, mais ce n'est pas le sujet...

J'ai déjà souvent eu ce débat avec [Romain](http://codingly.com/) dans le monde .Net (voir  [http://ninject.org](http://ninject.org/)).
Je connais très mal les alternatives à Spring dans le monde Java, mais  je connais celle de Google : [Guice](http://code.google.com/p/google-guice/).

Voici un [tuto/introduction très convaincante](http://www.ibm.com/developerworks/library/j-guice.html?ca=dgr-jw22Guice&S_tact=105AGX59&S_CMP=GRsitejw22). [](http://www.ibm.com/developerworks/library/j-guice.html?ca=dgr-jw22Guice&S_tact=105AGX59&S_CMP=GRsitejw22)

Pour ceux qui ne connaissent pas Ninject ou Guice, voici un peu le principe :
Au lieu de rédiger un XML, on utilise massivement les annotations  (attributs en .Net) pour spécifier les injections. Ceci est aussi  possible en Spring (technique dite `Autowire`) mais l'utilisation du XML reste nécessaire  pour personnaliser plus finement les dépendances entre instances.
Dans le cas de Guice, au lieu de rédiger un XML, on créer une classe `Module` qui réalise le mapping entre une interface et la classe  concrète à instancier/injecter.
On peut spécifier bien plus de chose que cela, mais je vous laisse  lire l'article pour découvrir par vous même.

Pour ceux qui veulent suivre le débat "Spring vs Guice" ou "XML vs Code", voici le point de vue de [la documentation officielle de Guice](http://code.google.com/p/google-guice/wiki/SpringComparison).

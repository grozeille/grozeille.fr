---
author: grozeille
comments: true
date: 2010-01-04 21:51:23+00:00
layout: post
slug: spring-fluent
title: Spring.Fluent
wordpress_id: 222
categories:
- Spring.Fluent
tags:
- .Net
- Spring.net
---

Certains le savent déjà, je suis un accro à [Spring.Net](http://www.springframework.net/) depuis ses débuts.
En fait, je suis devenu amoureux de Spring Java dès sa sortie... c'était les débuts de l'IOC.

[Spring](http://www.springsource.com/) est devenu un framework "standard de facto" dans le monde Java. Il inclut bien plus que de l'IOC: AOP, Web MVC, etc.
Aujourd'hui, Spring c'est aussi un serveur "JEE" d'un nouveau genre. Puis il y a eu l'acquisition d'Hyperic, puis c'est au tour de VMWare d'acquérir Spring...
Bref, c'est une vrai success story dans le monde Java.

Quand à Spring.Net, ce n'est pas encore ça. Le [projet Castle](http://www.castleproject.org/) est même lui plus avancé: framework IOC, AOP, Web MVC, etc.
Je crois que Castle était en avance sur son temps dans l'écosystème .Net, c'est peut-être la raison pourquoi il n'a pas pris la même ampleur que Spring Java.

Mais j'ai foie en Spring! Ce framework m'aide tout les jours à réaliser des **applications d'entreprises** complexes et robustes.

Mais une chose rebute TOUT développeur .Net: la configuration XML.
Le XML c'est verbeux, le XML ça ne se compile pas, on n'a pas intellisense avec le XML...
Bref, plein de raison de préférer des frameworks comme [AutoFac](http://code.google.com/p/autofac/) ou [Ninject](http://ninject.org/) qui propose une approche de configuration par code, voir à la sauce "fluent".

A ça, je réponds que:



	
  * la verbosité n'est pas dramatique quand on a la complétion. Je remarque aussi que la verbosité est reproché avec des fichiers XML de 1000 lignes... ce qui est tout aussi vrai avec un code source C# de 1000 lignes.

	
  * la complétion et la vérification du XML peut être faite à l'édition ou la compilation, c'est ce que fait  [Spring IDE](http://springide.org/blog/) sous Eclipse, mais pas de support VisualStudio pour le moment (même si [Resharper](http://www.jetbrains.com/resharper/) [arrive à la rescousse](http://www.springframework.net/docs/1.3.0/reference/html/vsnet.html#d4e9692))

	
  * on **PEUT** faire du Spring sans XML, même si les gens de Spring.Net n'ont pas été très cool sur l'API...


Comme l'API de Spring.Net est un peut obscure et pas très documenté sur son utilisation en dehors d'une configuration XML, j'ai décidé de faire une petite surcouche pour facilité l'écriture et que ce soit suffisamment intuitif pour ne pas avoir besoin d'une doc.

**De cette volonté est né le projet **[**Spring.Fluent**](http://github.com/grozeille/Spring.Fluent/)**!!**

C'est un projet OpenSource, ce qui veut dire que je ne vous interdit pas de m'aider à réaliser mon rêve :)
Ceci-dit, un projet similaire existe déjà: [http://code.google.com/p/fluent-spring/
](http://code.google.com/p/fluent-spring/)Alors pourquoi faire un fork? Car il m'a fallut 1 journée pour faire autant et même plus que ce le projet propose, et à ma façon qui me plait rien qu'à moi!

De plus, Mark Pollack à l'annonce de Spring.Net 1.3, a prétendu que la configuration "par code Fluent" sera un point de la prochaine version, à savoir la 2.0: [http://www.infoq.com/interviews/Spring.NET-1.3-2.0](http://www.infoq.com/interviews/Spring.NET-1.3-2.0)

Je souhaite à Mark et toutes l'équipe de Spring.Net de réussir, en attendant j'ai ma propre solution. Et si elle peut les inspirer pour Spring.Net 2.0, ce sera formidable. C'est pourquoi je pense ce cet "effort" n'est pas perdu: il n'est jamais inutile de contribuer au monde OpenSource et à faire connaitre ses opinions.

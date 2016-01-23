---
author: grozeille
comments: true
date: 2012-05-27 07:55:12+00:00
layout: post
slug: episode-9-mathias-decouvre-mef
title: 'Episode 9: Mathias découvre MEF'
wordpress_id: 517
categories:
- Developpement
- DotNetServer
tags:
- .Net
- com
- IOC
- mef
- VisualStudio shell
---

Après cette [petite pause sur COM](http://grozeille.com/2010/11/13/episode-8-mathias-decouvre-com) la dernière fois, revenons sur le sujet des [clients lourds et de la "composition"](http://grozeille.com/2010/11/13/episode-7-math…-techdays-2010).

Je vous ai déjà BEAUCOUP parlé de l’IDE Java Eclipse et la richesse de son framework de plugins basé sur OSGI.

Je vous ai parlé de .Net qui rattrape son retard à l’aide d’IOC et de MVVM.

Mais je ne vous ai pas encore parlé de VisualStudio.
Ce dernier offre depuis la version 2008 un noyau indépendant de l’IDE pouvant être utilisé pour n’importe quel type d’application : [VisualStudio Shell](http://www.microsoft.com/downloads/en/details.aspx?FamilyID=8e5aa7b6-8436-43f0-b778-00c3bca733d3&displaylang=en).

[![](http://grozeille.files.wordpress.com/2010/11/bb510103-isolatedmode_large.jpg?w=300)](http://grozeille.files.wordpress.com/2010/11/bb510103-isolatedmode_large.jpg)

Cella est possible à l'aide d'une gestion de « plugins » comme Eclipse (appelé « add-in »).
La gestion des add-ins de VisualStudio s’appuie sur COM (voila pourquoi il fallait que j'en parle avant ;) ).
Cela n'est pas étonnant puisque c'est LA technologie de communication inter-processus sur Windows.

Mais récemment, Microsoft a travaillé sur une nouvelle technologie d’activation de service et de "gestion de dépendances" et cette fois-ci 100% .Net. Cette dernière a été utilisée dans VisualStudio, afin de ne charger en mémoire que les add-in nécessaire suivant le besoin.

Cette technologie s’appelle MEF : [Managed Extensibility Framework](http://mef.codeplex.com/).
Et MEF fait du bruit : il est inclus officiellement dans .Net 4.0, Mono l'inclut dans la version 2.8 (car MEF est OpenSource, BRAVO Microsoft), et MEF est annoncé comme « remplaçant de l’IOC ».
En fait, même si on déclare des dépendances, ce n'est pas une solution IOC/DI...
D'ailleurs, je n'ai eu que de mauvais écho sur son sujet: mauvais usage, trop jeune?

Ce qui est bon à prendre, c'est l'aspect "attributs" pour déclarer ce qui serait visible à l'extérieur ou dans le conteneur IOC. Cela fait aussi pensé à la [JSR-299](http://in.relation.to/Bloggers/CommentsOnAnnotationsForDependencyInjection) qui propose des annotations standards en Java pour tout type de conteneur IOC.

J'ai aussi exploré d'autres pistes pour une gestion de "plugin": [Mono.Addin](http://monoaddins.codeplex.com/). Je trouve le principe très bien, et très inspirant, mais peut-être trop spécifique à ce pourquoi il a été inventé, cad, la gestion d'add-in dans Monodevelop.
Cette solution s'appuie aussi sur les attributs pour déclarer les Addins, donc c'est une bonne voie à suivre.

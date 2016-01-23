---
author: grozeille
comments: true
date: 2008-11-08 08:08:52+00:00
layout: post
slug: mono-nouveau-standard
title: 'Mono : nouveau standard ?'
wordpress_id: 101
categories:
- Developpement
- linux
tags:
- .Net
- linux
- mono
---

Pour ce qui ne sont pas au courant ou qui n'aurai pas vu la vidéo de la PDC, [voici l'article d'InfoQ sur Mono.Simd](http://www.infoq.com/news/2008/11/Mono-SMID).
J'aime bien le titre "Mono: Going Beyond the Standard", et c'est de ça que je vais parler...

J'ai posé la question lors de [la soirée ALT.Net](http://codingly.com/2008/11/05/altnet-en-france-mono-a-paris-pour-la-7eme-rencontre/) en présence de [Jean-Baptiste Evain](http://evain.net/blog/), à savoir si on ne va pas se retrouver avec 2 standards : .Net et Mono.
**ATTENTION**, je ne parle pas des spécifications de la VM ou du langage C#, mais des assembly fournies en standard avec le SDK.

<!-- more -->Pour comparer avec le monde Java, Sun établi des spécifications (JSR), et certifie une JDK car elle contient les "fonctionnalités" demandées. C'est indispensable pour le "[Write once, Run anyware](http://en.wikipedia.org/wiki/Write_once,_run_anywhere)".

Mais pour l'instant, Mono reste sur les traces de Microsoft, et il n'y a pas de volonté de standardisation commune, Microsoft faisant le standard _de facto_.

On dit même Mono être à la traine, car une application .Net ne marchera pas forcement sur Mono (à vérifier avec [MoMA](http://www.mono-project.com/MoMA)).
Mais on se rend déjà compte que seulement la [2ème mouture de Mono](http://www.mono-project.com/news/archive/2008/Oct-23.html) fournit son lot de nouveautés, et que l'inverse peut se produire (application Mono ne marchant pas « out of the box » sur la SDK de Microsoft).



	
  * Que nous réserve la version 3 ?

	
  * Mono va-t-il suivre un autre chemin (orienté jeux) ?

	
  * Va-t-on assister à une compétition (positive) .NetDK vs MonoDK ?

	
  * Pourra-t-on dire "je préfère l’implémentation de System.Collection.Generic.List de Mono, plutôt que celle de Microsoft" ?

	
  * Les développeurs choisiront-ils la version Libre pour que leurs applications soit le plus compatible possible, et pour être multi-plateforme (comme développer des WebServices sans utiliser WCF n’existant pas encore sous Mono) ?

	
  * Microsoft vont-ils intégrer le travail de Mono dans le .NetDK officiel ?


Un autre point : l'API de Linux est riche (oui oui!) et je trouve incroyable le nombre de binding Mono pour cette dernière :

	
  * [DBus](http://www.freedesktop.org/wiki/Software/dbus) : framework de communication inter-application orienté message

	
  * [GStreamer](http://gstreamer.freedesktop.org/) : framework multimedia

	
  * [Cairo](http://www.cairographics.org/) : framework vectoriel 2D

	
  * [Telepathy](http://telepathy.freedesktop.org/wiki/) : framework de chat (xmpp, sip, etc.)

	
  * [GTK](http://www.gtk.org/) : remplaçant des winforms ? ;)

	
  * etc.


Ils existent plusieurs applications Mono-Linux qui ne sont pas « portables » sous une autre plateforme, car trop liées aux API natives. Mais la communauté a la volonté de les faire porter sous Mac/Windows ([Tomboy](http://live.gnome.org/Tomboy/Win32),  [Banshee](http://abock.org/2008/10/20/cross-platform-thoughts-through-the-lense-of-banshee/)), et ça passe forcement par une migration de ces API natives.

Assiste-t-on à un Linux qui envahi notre Windows/Mac grâce à Mono ??

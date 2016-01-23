---
author: grozeille
comments: true
date: 2010-06-29 18:24:59+00:00
layout: post
slug: episode-3-mathias-decouvre-eclipse
title: 'Episode 3 : Mathias découvre Eclipse (et un peu OSGI)'
wordpress_id: 395
categories:
- Developpement
- DotNetServer
tags:
- .Net
- eclipse
- J2EE
- java
- osgi
---

Dans l'épisode 2, je vous ai dit à quel point les serveurs J2EE pouvaient être complexe dans la gestion d'application.
Il en est de même dans le monde des IDE avec la gestion des plugins.

Tout en étudiant J2EE, je suis tombé amoureux de mon IDE Java préféré : Eclipse. Pas seulement pour sont utilisation, mais aussi pour son architecture.

En effet, la réalisation de plugins pour Eclipse se fait de manière ultra puissante. A tel point que le « noyau » d’Eclipse peut être complètement extrait pour faire sa propre application qui n’a rien à voir avec un IDE : c’est le framework RCP (Rich Client Platform).
J’ai d’ailleurs à l’époque réalisé une application RCP pour la gestion de budget d’achat de livres pour les bibliothèques.

[![](http://grozeille.files.wordpress.com/2010/06/bibliographievista.jpg)](http://grozeille.files.wordpress.com/2010/06/bibliographievista.jpg)

Malheureusement, la pauvreté des composants graphique en Java faisait du tors à cette plateforme.
Mais je restais subjugué par le moteur de plugins :



	
  * Les plugins sont isolés afin que si un plugin crash, les autres continuent leur vie

	
  * Les plugins sont aussi isolé coté sécurité : un plugin ne peut pas accéder aux codes d’un autre plugin si ce dernier ne l’a pas explicitement rendu « publique »

	
  * Les plugins peuvent publier et consommer des services, avec un model très élégant

	
  * Il y a une gestion de dépendance entre les plugins, avec la prise en compte des versions

	
  * L’installation et la mise à jour des plugins se fait d’une simplicité déconcertante



[![](http://grozeille.files.wordpress.com/2010/06/16279.png)](http://grozeille.files.wordpress.com/2010/06/16279.png)

En fait, si la gestion des plugins est si balaise c’est car elle provient d’un standard de « développement par composant » : OSGI.

L’alliance OSGI est un organisme de personnes qui se mette d’accord ensemble sur des specs concernant les frameworks OSGI. C’est encore la que Java écrase .Net par sa maturité : il n’y a pas de monopole, il y a bien plusieurs acteurs derrière un « standard » ouvert qui va connaitre de multiples implémentations.

OSGI est donc un framework complexe de gestion de « modules » qui exposent des « services ». N’hésitez pas à lire le WIKI qui explique ça très bien : [http://en.wikipedia.org/wiki/OSGi](http://en.wikipedia.org/wiki/OSGi)

En conclusion, Eclipse est une plateforme riche en plugins grâce au coté Open-Source de l'IDE, à l'API de plugins très bien faite mais aussi à l'aide du plugins pour développer des plugins :)

Qu'en est-il du coté .Net? VisualStudio a-t-il le même succès concernant le développement ce plugins? Offre-t-il une architecture de plugin aussi puissante? On verra ça dans un autre épisode ;)

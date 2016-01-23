---
author: grozeille
comments: true
date: 2010-07-09 21:32:14+00:00
layout: post
slug: episode-4%c2%a0-mathias-decouvre-spring-et-un-peu-plus-osgi
title: 'Episode 4 : Mathias découvre Spring (et un peu plus OSGI)'
wordpress_id: 417
categories:
- Developpement
- DotNetServer
tags:
- .Net
- java
- osgi
- spring
---

Dans l'[Episode 2](http://grozeille.com/2010/06/29/episode-2-mathias-decouvre-j2ee/), je vous ai parlé de ma découverte de J2EE.
Si j'ai été émerveillé par la plateforme, j'avoue qu'elle était assez complexe.

C'est alors que la lourdeur des framework J2EE a donné naissance à une alternative qui s’est voulu plus simple : [Spring](http://en.wikipedia.org/wiki/Spring_Framework).

J'aime bien Spring, je pense que vous le savez déjà :)
C'est pour moi en quelque sorte l'équivalent de l'esprit d'[ALT.Net](http://www.altnetfr.org/), mais en Java.

Ce fut alors la mode des [IOC](http://en.wikipedia.org/wiki/Inversion_of_control), et de l'approche orienté POJO. Quand j’ai découvert cela, je me suis rendu compte à quel point le framework d’Eclipse RCP pouvait être compliqué…
La gestion de dépendance et de publication/consommation de service devenaient extrêmement simple.

La ou Spring n’était qu’un framework, « [SpringSource DM Server](http://www.springsource.com/products/dmserver) » est, quand à lui, un vrai serveur J2EE mais avec une architecture complètement différente de ses concurrents : il est basé sur le même moteur [OSGI qu’Eclipse](http://en.wikipedia.org/wiki/Equinox_(OSGi)) !

L’installation de nouvelles applications vous semble pénible ? SpringSource DM Server offre un « AppStore » pour installer un nouveau service et ses dépendances en 2 cliques!

Pour ceux qui ont lu mon [billet sur WebMatrix](http://grozeille.com/2010/07/09/episode-bonus-microsoft-ma-entendu-ou-pas/), la fonctionnalité n'est pas tout à fait la même que c'elle du produit Microsoft.Vous pouvez ici installer bien d'autres choses que des applications Web: des ESB, des serveurs Web (car oui, en Java, on a le choix entre Tomcat, Jetty et autres), etc.
Vous voulez installer un serveur de Messaging ? Installer [ActiveMQ](http://activemq.apache.org/) en quelques cliques : [http://www.springsource.com/repository/app/bundle/version/detail?name=com.springsource.org.apache.activemq&version=5.3.0](http://www.springsource.com/repository/app/bundle/version/detail?name=com.springsource.org.apache.activemq&version=5.3.0)

Vous trouvez plus d’infos sur [http://www.springsource.com/products/dmserver/repository](http://www.springsource.com/products/dmserver/repository)

[![](http://grozeille.files.wordpress.com/2010/07/spring-context.png?w=300)](http://grozeille.files.wordpress.com/2010/07/spring-context.png)
En plus de tout ces avantages, SpringSource DM Serveur offre un interface d’administration d'un pure merveille, j’en bave quand je vois que Microsoft reste attaché à sa MMC…
Et comme si ça ne suffisait pas, SpringSource ont racheté [Hyperic](http://www.hyperic.com/) qui est une appli Web de Monitoring applicatif, ce qui rend l’administration de votre serveur  encore plus professionnel.

Petite conclusion:



	
  * l'IOC c'est cool, vive l'approche POJO

	
  * OSGI c'est de la bombe. Cela permet aussi bien de gérer des plugins dans un IDE, que des middleware dans un serveur d'applications

	
  * l'installation d'une plateforme applicative doit être simple et facile, autant que de lancer un Setup de EasyPHP ou de cliquer sur un lien d'un "AppStore"

	
  * vive les interfaces Web d'administration, à mort la MMC



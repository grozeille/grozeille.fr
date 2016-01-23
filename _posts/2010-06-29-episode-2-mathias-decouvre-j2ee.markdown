---
author: grozeille
comments: true
date: 2010-06-29 06:09:07+00:00
layout: post
slug: episode-2-mathias-decouvre-j2ee
title: 'Episode 2 : Mathias découvre J2EE'
wordpress_id: 390
categories:
- Developpement
- DotNetServer
tags:
- .Net
- J2EE
---

En sortant de mes études, je me suis rapidement retrouvé dans le moule en adoptant Java. J'ai alors découvert les serveurs « conteneur de servlets » ou serveur J2EE, ce qui était quand même plus puissant que PHP…

Je vous ai parlé d'EASYPHP, avec lequel l'utilisateur avait une interface Web pour administrer sont serveur Apache: en 2 clicks n'importe qui peut créer un nouveau site web, sans connaitre le fameux "apache.conf"

Je suis fondamentalement contre la MMC de Windows, et je pense que IIS devrait aussi fournir une interface Web.
Encore aujourd’hui, je suis jaloux de la piètre interface de Tomcat qui permet de déployer à chaud une application web Java à distance avec une interface web, et de pouvoir gérer son cycle de vie (start/stop/reload).

[![](http://grozeille.files.wordpress.com/2010/06/tomcat.png)](http://grozeille.files.wordpress.com/2010/06/tomcat.png)

Ca parait rien comme ça, mais il n’y a pas d’équivalent pour gérer les applications Web .Net, donc oui, je suis jaloux.

Tomcat n'est pas un serveur J2EE, on ne peut y déployer que des applications Web: WAR (Wab ARchive).
Mais un serveur J2EE est plus puissant: on peut y déployer des applications "service" (JAR/EAR) voir des tâches schédulées.
De plus, les applications offrent souvent des "MBean": Managed Bean. Ce sont des objets qui sont accessibles à travers une couche de service, et tout les serveurs J2EE offrent une interface Web pour les gérer.
Vous pouvez ainsi exposer la bean "HttpCache" avec le service "Clear" par exemple. Bref, c'est le paradis des admins.

Alors quand vous allez voir les pages Web d'administration de JBoss ou SpringSource, on se dit qu'il manque clairement quelque chose à la plateforme .Net.

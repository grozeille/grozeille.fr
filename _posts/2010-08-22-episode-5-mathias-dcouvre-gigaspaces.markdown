---
author: grozeille
comments: true
date: 2010-08-22 14:16:51+00:00
layout: post
slug: episode-5-mathias-dcouvre-gigaspaces
title: 'Episode 5 : Mathias découvre Gigaspaces'
wordpress_id: 437
categories:
- Developpement
- DotNetServer
tags:
- .Net
- Cluster
- Gigaspaces
---

<strong>Mathias:</strong> Re, désolé j’étais AFK… les vacances, tout ça…


Donc voila, je suis de retour avec un cerveau presque lavé.
Et comme j’ai commencé une série, il fallait bien que le la termine ;)

Dans [l’épisode 4](http://grozeille.com/2010/07/09/episode-4%c2%a0-mathias-decouvre-spring-et-un-peu-plus-osgi/) je vous ai parlé de Spring Java, le serveur d’application.
Je vais maintenant vous parler de [Gigaspaces](http://www.gigaspaces.com/), car j’y ai bossé un petit peu, et ça a changé ma façon de penser.

Pour commencer: MAIS C’EST QUOI GIGASPACES?

C’est plusieurs choses à la fois. Ce qui est drôle c’est que le terme à la mode en ce moment est "No-SQL" et Gigaspaces est cité comme faisant partie de la catégorie.

D’autres appellent ça un "[Tuple Space](http://en.wikipedia.org/wiki/Tuple_space)" mais on parle plus souvent de "In-Memory Data Grid" ou "Distributed Caching".

Et comme "distributed" rime souvent aujourd’hui avec "Cloud", il y a la des mots clés bien commerciaux ;)

Mais comme je sais que vous, lecteurs, vous n’êtes pas la pour acheter une licence, mais vous êtes plutôt des Geeks du code, je vais expliquer cela de manière plus "pratique".

Gigaspace est un cache mémoire: c’est un serveur qui fournie comme service de stocker et lire des données de type "clé+valeur" en utilisant la mémoire du serveur.
Un cache est pratique dans diverses situations:



	
  * Vous stockez en mémoire une donnée lu depuis une base de donnée, afin de la lire plus rapidement les prochaines fois

	
  * Vous stockez en mémoire une donnée calculée, qui va être traité par un autre programme

	
  * Vous stockez des "messages" afin de communiquer de manière asynchrone avec d’autres programmes


En général, quand on souhaite partager des données entre 2 programmes, on utilise une base de donnée. Mais quand cette donnée change souvent, ou vous avez besoin d’une lecture très rapide, il est préférable de la stocker dans une mémoire partagée.

L’inconvénient de la mémoire, c’est qu’elle est plus rare que l’espace disque. Gigaspaces permet d’avoir un "cluster" de serveurs, vous pouvez donc additionner la mémoire d’autant de serveur que vous voulez.

Un autre inconvénient c’est que la mémoire est volatile, et en cas de crash du serveur, cette dernière est perdue.
Gigaspaces permet d’avoir des nœuds "backup" dans le cluster, ce qui veut dire que la mémoire est répliquée sur un serveur de secours au cas ou le premier plante. Bien sûr, vous pouvez avoir autant de backup que vous voulez.

…OUAI, ET ALORS?

Si Gigaspaces fournit un service avec une très faible latence et met l’accent sur les performances, ce qui m’intéresse c’est l’aspect "Cluster".

[![](http://grozeille.files.wordpress.com/2010/08/app_arch_on_cloud11.jpg)](http://grozeille.files.wordpress.com/2010/08/app_arch_on_cloud11.jpg)

Sur cette architecture, il est possible de déployer un programme de tout type: le déploiement du ZIP se fait en 2 clicks sur tous les nœuds du cluster, avec une gestion d’activation Primary/Backup.

Que ce programme soit un cache ou un serveur Web, je trouve l’idée très séduisante: c’est la dessus que repose le Cloud Computing.

Bien évidement, si l’ont décide d’avoir plusieurs applications "Primaire" pour répartir la charge, ces dernières devront prendre en compte cet aspect dans l’architecture (communication entre nœuds primaires, mémoire partagée).

Il est aussi possible de basculer l’état actif/inactif d’un nœud en fonction d’une mesure de charge: si le serveur 1 manque de mémoire, l’application se désactive pour se re-activer sur le serveur 2.

Je voulais aussi parler d’un dernier truc sympathique concernant Gigaspaces: le point d’entré d’une application déployée n’est pas un EXE ou un JAR, mais un fichier XML Spring! Il n’est donc pas nécessaire de coder un Bootstrap qui va seulement charger ce fichier de configuration…

Vous avez peut-être compris ou je voulais en venir: je souhaite un serveur d'application .Net sur lequel on peut déployer une application facilement sans ce soucier de l'infrastructure: que ce soit un serveur Windows ou Linux, qu'il y ai 3 instances primaires ou 6 instances primaires avec 2 backups, que les services consommés soient locaux ou distant...

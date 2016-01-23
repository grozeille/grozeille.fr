---
author: grozeille
comments: true
date: 2012-05-30 17:57:58+00:00
layout: post
slug: episode-12-mathias-decouvre-topshelf
title: Episode 12 - Mathias découvre Topshelf
wordpress_id: 548
categories:
- Developpement
- DotNetServer
tags:
- .Net
---

Je vous l'avez bien dit que j'ajouterai des épisodes pour faire durer le suspens :)

Il était primordial que je parle de [TopShelf](topshelf-project.com), qui a forcement marqué mon existence.
Pour résumé Topshelf, je dirais que c'est... un serveur d'application!
Je vais peut-être trop loin en disant ça, mais c'est la voie qu'il est en train de prendre...

[![](http://grozeille.files.wordpress.com/2012/05/slide-1.png?w=300)](http://grozeille.files.wordpress.com/2012/05/slide-1.png)

Une des premières fonctionnalités de Topshelf, est de pouvoir développer une application qui peut s'exécuter en mode "console" ou en mode "service Windows": vous n'avez plus d'excuse pour avoir besoin des droits d'admin ! ;)

La deuxième, tout aussi importante, est de pouvoir déployer votre application sans avoir besoin de redémarrer votre service Windows: Topshelf agit comme une application Web ASP.Net, ne lock pas vos DLLs, exécute votre application dans un AppDomain isolé, et relance l'application après détection d'un changement de celles-ci.
C'est donc bien un "conteneur d'application" !
Vous pouvez y déployer autant d'application que vous voulez dans un service Windows sous la forme d'une DLL, le bootstrap de Topshelf s'occupe de son cycle de vie.

Suite naturelle de son évolution, Topshelf est fourni maintenant avec une "application" déployé par défaut: Topshelf Dashboard. Cette dernière offre un portail Web pour pouvoir stopper/démarrer ces applications.
Ça ressemble donc fortement à mon projet :)
Il est clair que c'est une très bonne source d'inspiration pour améliorer encore plus mon projet.

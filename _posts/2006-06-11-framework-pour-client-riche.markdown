---
author: grozeille
comments: true
date: 2006-06-11 09:37:18+00:00
layout: post
slug: framework-pour-client-riche
title: Framework pour "client riche"
wordpress_id: 13
excerpt_separator: <!--more-->
categories:
- Developpement
tags:
- .Net
- Framework
- Winforms
---

Il existe de nombreux framework d'application web, tel que [Spring](http://www.springframework.org/), [Struts](http://struts.apache.org/), JavaServerFaces ou WebForms...
Mais qu'en est-il des "clients riches", cad, des applications graphiques faites en WinForms, GTK, etc...

Dans le monde Java, il y a [Eclipse RCP](http://wiki.eclipse.org/index.php/Rich_Client_Platform), qui est pour moi sans conteste le meilleur framework d'application. Il y a aussi [Spring RCP](http://spring-rich-c.sourceforge.net/) que je connais mal.

Dans le monde .Net, [CAB](http://www.gotdotnet.com/codegallery/codegallery.aspx?id=22f72167-af95-44ce-a6ca-f2eafbf2653c) est sans doute le plus connus, et pour cause c'est le framework propose par M$, mais il en existe d'autre comme [eXpressApp](http://www.devexpress.com/Products/NET/eXpressApp/) (de DevExpress).

On peut aussi se faire son propre framework... et je vais essayer de lister les avantages et inconvenients de coder soi meme ou d'utiliser l'existant car, bien evidement, aucune solution n'est parfaite et la bonne solution est celle qui s'adapte le mieux au besoin...

<!--more-->

Un framework existant c'est bien, c'est puissant, c'est deja code, mais on n'en a pas la maitrise. S'il y a un bug, on laisse a l'equipe du framework le soin de le corriger. Mais puisqu'on en a pas la maitrise, on ne choisi pas non plus les evolutions et les possibilites du framework.
Meme si le travail de realisation du framework est deja fait, il faut tout de meme une formation (qu'on a pas si les personnes concernees font elle meme leur propre framework). Dans tout les cas, un framework existant "puissant" et "souple" est synonyme de "complexe". La formation n'est donc pas a negliger. En parlant de formation, je parle par experience de mes heures de developpement avec Eclipse RCP, quand on connait mal le framework on voit qu'on peut faire une meme chose de plusieurs façon et on ne sais jamais si c'est la bonne... et il n'y a rien de plus frustrant quand de simple petite chose deviennent vite complexe a realiser car le framework "enterre" tout et qu'on connait pas ses points d'entree pour atteindre la fonctionnalite voulue.Les frameworks "souples" le sont car ils doivent s'adapter aux besoins de chaque developpeur... Ce qui veut dire qu'il y a toujours une partie "parametrage" ou realisation d'un code commun pour repondre aux besoins de bases, avant de pouvoir utiliser les possibilites du framework. Exemple : je souhaite faire une application a l'aide d'eclipse RCP, mais en partant de rien j'ai une fenetre vide. Si je veux que ça ressemble a Outlook (barre de navigation laterale, menu principal, barre d'outil etc.) il me faut pas mal de code. Apres avoir realiser le "noyau" adapte a mes besoins, je peux commencer a coder les parties "metiers" de l'application.

J'ai choisi de faire mon propre framework, car je pense que les frameworks existants sont trops complexe pour repondre au besoin. Je souhaite un framework "simple" sans trops de fonctionnalites "inutiles"... le mot d'ordre : Lightweight.
Le temps de formation pour moi est null, et pour les autres est minime puisque le framework reste "au plus simple".
Bien sur je part pas de zero... toutes mes connaissances en Eclipse RCP se retrouve dans mon framework. Ce qui me donne un double avantage : quand j'ai besoin de repondre a un probleme, je regarde comment c'est fait dans eclipse et je m'en inspire.
Pourquoi ne pas utiliser Eclipse RCP alors ? Tout simplement car la philosophie de mon entreprise est de faire du .Net (car ils trouvent que Java c'est de la merde et que ne pas utiliser du M$ c'est anti-professionnel... vraiment, quand est-ce que le monde evoluera ?).
Donc, comme mon application est au plus simple, et repond seulement au besoin de mon projet, le "noyau" est deja code (du coup il n'est pas souple, mais il ne tend pas a l'etre car personne ne va re-utiliser se framework). La seul tache des membres de l'equipe c'est de comprendre le framework (qui je rappelle est simple) et de se concentrer a faire le code "metier". Bien evidement, cette solution n'est pas parfaite. Il me reste la responsabilite de corriger les bugs, et de faire evoluer le framework suivant le besoin. Mais je suis certain que les besoins n'atteindront pas ceux couvert par des Framework complexe... et que mon travail n'est donc pas du temps de perdu.

Bien evidement, je suis loin de l'avoir fini, et il peut toujours d'ameliorer suivant le besoin... mais je pense etre sur la bonne voie. Je vais essayer de commenter mes choix et rapporter le status de mon projet.

[![BmV3](http://grozeille.files.wordpress.com/2006/06/BmV3.thumbnail.png)](http://grozeille.files.wordpress.com/2006/06/BmV3.png)

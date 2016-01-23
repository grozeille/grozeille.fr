---
author: grozeille
comments: true
date: 2008-09-02 19:45:46+00:00
layout: post
excerpt_separator: <!--more-->
slug: google-chrome-rocks
title: Google-chrome rocks!!!
wordpress_id: 91
categories:
- Blabla
tags:
- google
- opensource
- web
---

[![](http://grozeille.files.wordpress.com/2008/09/google-chrome_d_253845ejpeg1.jpg)](http://grozeille.files.wordpress.com/2008/09/google-chrome_d_253845ejpeg1.jpg)

Cela fait du buzz en ce moment, Google sort son navigateur [Google-Chrome](http://www.google.com/chrome), et pour l'illustrer l'annonce est faire [sous forme de BD](http://www.google.com/googlebooks/chrome/)!!

Premièrement, j'adore la style "BD", car comme on le dit : "un schéma vaut parfois mieux qu'un long discours". Et on comprend tout de suite ce qu'ils veulent dire quand on voit la représentation "imagé".

J'aime bien donner mon point de vue, et je vais surtout m'attarder sur l'aspect "interface utilisateur" et "Web vs Desktop".

<!--more-->

J'avais déjà lu de nombreux trucs sur [la gestion des onglets dans les navigateurs](http://people.mozilla.com/~faaborg/files/prism/announcement/transition550.png), et en résumé on remarque que l'OS gère tellement mal les fenêtres, que l'on a inventé une nouvelle "barre de tâches" intégrée au navigateur (les onglets).
Certes, avec des gestionnaires de fenêtres tel que sous MacOS, avec Exposé, ou sous Linux, avec [Compiz](http://fr.youtube.com/watch?v=-LsrocISlyQ), il est facile de naviguer entre les fenêtres d'une même application sans avoir besoin d'onglet.
Quand on dit que le Web converge vers le Desktop, on s'aperçoit qu'un site n'est ni plus ni moins qu'une application. Cela est d'autant plus flagrant avec des sites comme GMail, ou Facebook. Personnellement, je les laisse toujours ouverts, et pour éviter de les fermer accidentellement, je les laisse dans une fenêtre séparée de ma navigation "temporaire".
De mon point de vue, ça ne devrait pas être le rôle du navigateur de gérer des fenêtres (onglets), mais plutôt celui de l'OS.


[![](http://grozeille.files.wordpress.com/2008/09/image-23.png?w=300)](http://grozeille.files.wordpress.com/2008/09/image-23.png)
"Mais il subsiste des onglets dans Google-Chrome!!??" me diriez-vous. En effet, je crois que c'est quelque chose qui fait partie des habitudes difficiles à perdre...
Mais un onglet est maintenant une entité bien distincte, et chaque onglet tourne maintenant dans un processus différent comme des applications différentes.
De plus, Google-Chrome propose aussi un mode "standalone" comme dans [Google Prism](http://labs.mozilla.com/2007/10/prism/), c'est à dire que l'application web (tel que Gmail) s'ouvre dans une fenêtre dédiée, sans barre de navigation etc... "_nul besoin, je suis dans Gmail, et je reste dans Gmail. Les boutons de navigations du site me suffisent._"
J'en profite pour dire que j'adore leur façon de gérer les popups (la BD [l'explique mieux](http://www.google.com/googlebooks/chrome/images/23.jpg) que mes mots ;))

Dans la troisième partie, ils parlent des onglets qui incluent leurs propres boutons de navigation ainsi que leur propre barre d'adresse. Comme je l'ai dit, chaque onglet est une application à part entière avec sa propre interface, et les boutons de navigations/barre d'adresse en font partie.
Il est vrai que j'utilise rarement la boite de recherche, car finalement je tape un mot dans la barre d'adresse, ce qui lance "google j'ai de la chance"... Que les deux soient "fusionnés", me semble naturel aussi. Google appelle ça "[l'omnibox](http://www.google.com/googlebooks/chrome/images/19.jpg)".
Enfin, Google corrigent [des bugs de "fonctionnalité"](http://www.google.com/googlebooks/chrome/images/20.jpg) de Firefox, comme le fait d'aller sur le site "_http://cnn.com_" quand je tape "_cnn_", et non la dernière page mémorisée dans l'historique, à savoir "_h__ttp://cnn.com/2008/politics/07/27/campaign.wrap/index....._"

Je suis aussi fan de l'idée de la recherche/complétion à l'aide de la touche "tab" dans l'omnibox. C'est peut-être un peu geek, mais ça me rappelle la complétion en ligne de commande sous Linux/MacOS ou MsDos.

Google expliquent aussi les sources des problèmes concernant les ressources et le caractère "[mono-threadé](http://www.google.com/googlebooks/chrome/images/4.jpg)" d'un navigateur.
Qui n'a pas déjà pesté sur la lenteur d'affichage des pages, d'exécution du Javascript, du freeze du navigateur à cause d'une pub flash, ou des 380mo en mémoire pris par Firefox ???
Gérer les ressources, c'est normalement le rôle de l'OS. Et je le répète : un site web n'est ni plus ni moins qu'une application, elle devrait alors avoir son propre processus, avec sa propre gestion de ressource, sans empêcher la navigation dans les autres onglets.

[![](http://grozeille.files.wordpress.com/2008/09/image-24.png?w=300)](http://grozeille.files.wordpress.com/2008/09/image-24.png)
Coté performance, on blame souvent Javascript....
Les applications web se rapprochant des applications Desktop, elles deviennent de plus en plus "dynamiques" et "user friendly". Pour se faire, on utilise Javascript depuis bien longtemps. Mais ce n'est que depuis peu (Web 2.0) que le Javascript est [exploité massivement](http://script.aculo.us/). Et c'est la qu'on se rend compte de ses limites en terme de fonctionnalité et de performance.
Certains contournent le problème, en intégrant un "plugin" tel que Flash/Java/Silverlight, et réalisent leurs sites en partie/entièrement avec. Parfois, le navigateur ne sert plus qu'à lancer le player flash, qui lui gère entièrement l'interface graphique.
Je suis fan de Javascript car ça reste léger, non propriétaire, et cela s'intègre bien avec le HTML. Vous allez me dire que je suis vieux jeux, et qu'il faudrait tout migrer immédiatement vers du Silverlight :) mais ça c'est un autre débat.

Google est repartie de ZERO pour réaliser son moteur Javascript, chose qui m'étonne peu. Mais ce qui m'a en tout cas fait rire, c'est de lire qu'ils font carrément une [machine virtuelle](http://www.google.com/googlebooks/chrome/images/13.jpg) ! L'avenir est aux machines virtuelles, tel que Java et .Net, que ce soit par leur gestion de la mémoire, ou les [optimisations de compilations](http://www.google.com/googlebooks/chrome/images/15.jpg). D'autres arguments sont cités dans la BD, et ils paraissent souvent évidents. Mais il n'y a qu'un géant comme Google qui peut dire "bon, les autres trucs c'est de la merde, on va tout refaire à zero en apprenant des erreurs du passé". Mine de rien, c'est un challenge énorme, et on a tendance à préférer ré-utiliser un existant même s'il faut le faire évoluer.

A la fin, ils parlent aussi un peu de [Google Gears](http://gears.google.com/). Pour moi, c'est comme si le navigateur était devenu une machine virtuelle pour héberger nos applications web, et Google Gears c'est le "framework", qui offre la possibilité d'étendre leurs fonctionnalités à l'aide de "librairies" réutilisables. L'écart Web-Desktop se resserre encore...

[![](http://grozeille.files.wordpress.com/2008/09/dlpage_lg.jpg?w=300)](http://grozeille.files.wordpress.com/2008/09/dlpage_lg.jpg)
Un petit mot sur la sécurité : le fait d'isoler les onglets dans des processus différents permet d'isoler les programmes "malveillant" des autres. Quand le processus est lui aussi découpé en plusieurs niveaux d'isolation, c'est encore mieux. Quelque chose m'a amusé concernant l'interaction entre l'utilisateur et la Sandbox : on dirait qu'il y a un pare-feu interne entre eux, et que seul l'utilisateur peux initier une "connexion" avec la sandbox, qui ne peux que lui répondre. [L'explication en image](http://www.google.com/googlebooks/chrome/images/29.jpg) est bien plus parlante -_-'

Je ne couvre pas tout, je vous laisse découvrir la BD par vous même.
Je suis sûr que ce navigateur va changer beaucoup de chose dans nos façons de développer des applications Web, et dans notre façon de surfer.

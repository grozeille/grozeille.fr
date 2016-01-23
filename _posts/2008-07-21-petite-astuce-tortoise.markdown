---
author: grozeille
comments: true
date: 2008-07-21 21:55:24+00:00
layout: post
excerpt_separator: <!--more-->
slug: petite-astuce-tortoise
title: Petite astuce Tortoise
wordpress_id: 77
categories:
- Developpement
tags:
- .Net
- Developpement
- gestion de projet
- svn
---

Vous connaissez sans doute tous les `properties` de svn ?
J'adore Tortoise, et ce dernier offre des fonctionnalités "supplémentaires" à l'aide de properties custom.
On cherche souvent à empêcher les autres membres de l'équipe à commiter sans commentaires. C'est possible à l'aide des properties, à condition d'utiliser Tortoise :)

[![](http://grozeille.files.wordpress.com/2008/07/tortoisesvnminlogsize.png?w=300)](http://grozeille.files.wordpress.com/2008/07/tortoisesvnminlogsize.png)

<!--more-->

Les properties de Tortoise commencent par `tsvn:`. En voici [la liste](http://tortoisesvn.net/docs/release/TortoiseSVN_fr/tsvn-dug-propertypage.html#tsvn-dug-propertypage-tsvn-props).
Celle qui nous intéresse est `tsvn:logminsize`. Ceci dit, ça ne va pas empêcher celui qui n'a vraiment pas envie d'en mettre de saisir n'importe-quoi, voir de passer par autre chose que Tortoise...

Certains utilise les [Hooks SVN](http://tortoisesvn.net/docs/release/TortoiseSVN_fr/tsvn-repository-hooks.html) pour annuler un commit si le commentaire est vide, mais le message d'erreur n'est pas explicite. Les Hooks sont tout simplement des scripts appelés par SVN lors d'une opération (avant commit, après commit, etc.).
Il faut souligner qu'il est possible d'affecter n'importe quel propriété, même si elle n'existe pas dans la liste, et les traiter par des Hooks "fait maison".

Tortoise propose même d'exécuter des [Hooks coté client](http://tortoisesvn.net/docs/release/TortoiseSVN_fr/tsvn-dug-settings.html#tsvn-dug-settings-hooks). Cela peut être utile quand on veut, par exemple, rentrer un commentaire dans le [Bug-tracker](http://en.wikipedia.org/wiki/Bugtracker) pour faire le lien avec le commit.

Et en lisant un peu plus la doc de Tortoise, on découvre qu'on peut aussi utiliser des objets COM comme des Hooks!! Et l'exemple porte justement sur [un lien "plus intime" avec le Bug-tracker](http://tortoisesvn.net/docs/release/TortoiseSVN_fr/tsvn-dug-settings.html#tsvn-dug-settings-hooks-issuetracker). Apparemment, les objets COM peuvent être utilisés comme des plugins pour offrir bien [d'autre possibilités](http://tortoisesvn.net/docs/release/TortoiseSVN_fr/tsvn-dug-bugtracker.html#tsvn-dug-bugtracker-ref).

En résumé, Tortoise est en mon sens l'outil idéal avec SVN, surtout depuis la [version 1.5](http://tortoisesvn.net/downloads) et les `merge` simplifiés :)
Les Hooks SVN permettent diverses choses, et le fait de pouvoir en exécuter coté client peut aussi s'avérer utile. Pouvoir étendre les fonctionnalités à l'aide de plugin COM rend Tortoise encore plus puissant. De plus, ce dernier [est codé en .Net](http://tortoisesvn.tigris.org/svn/tortoisesvn/trunk/), ce qui me donne encore plus envie de jouer avec :)

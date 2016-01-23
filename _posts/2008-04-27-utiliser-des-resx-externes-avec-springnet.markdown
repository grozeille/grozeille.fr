---
author: grozeille
comments: true
date: 2008-04-27 19:19:38+00:00
layout: post
excerpt_separator: <!--more-->
slug: utiliser-des-resx-externes-avec-springnet
title: Utiliser des *.resx externes (avec Spring.net)
wordpress_id: 32
categories:
- Developpement
tags:
- .Net
- I18N
- Spring.net
---

On a parfois besoin de livrer une application .Net avec les fichiers de ressources, afin qu'un traducteur, voir même un intégrateur, puisse faire les traductions au dernier moment.

Si cette personne doit recompiler l'application pour voir le fruit de son travail, ce n'est pas très pratique voir impossible: allez lui expliquer que VisualStudio n'est pas nécessaire et qu'il est possible de créer des ressources avec [ResGen.exe](http://msdn2.microsoft.com/fr-fr/library/ccec7sz1(VS.80).aspx) (et [al.exe](http://msdn2.microsoft.com/fr-fr/library/c405shex(VS.80).aspx) pour faire des [assembly satellites](http://msdn2.microsoft.com/fr-fr/library/sb6a8618(VS.80).aspx)). Très franchement, les traducteurs ne veulent pas de quelque chose d'aussi et vont vous fuir comme la peste si vous leur demander d'être des développeurs.

<!--more-->

La solution est donc d'utiliser simplement des fichier *.resx sans les compiler, et elle a plusieurs avantages:




  * le traducteur n'a pas à savoir comment compiler des ressources (ce n'est pas un développeur)


  * les fichiers *.resx sont sous la forme XML, et donc (très?) lisible (la structure propose même un champ "commentaire")


  * il existe bien sûr des éditeurs de fichiers *.resx pour ceux qui ne veulent même pas savoir ce que XML veut dire: [Resourcer for .net](http://www.aisto.com/roeder/dotnet/)


Vous pouvez retrouver ces explication sur [le blog suivant](http://blechie.com/WPierce/archive/2007/08/01/Using-Resx-Files-with-a-ResourceManager.aspx). [
](http://blechie.com/WPierce/archive/2007/08/01/Using-Resx-Files-with-a-ResourceManager.aspx)Et Oh joie! Ce blog explique comment réaliser un `ResourceManager` personnalisé capable de charger des fichiers .resx! C'est donc tous ce qu'il nous faut, nul besoin de réinventer un autre mécanisme de traduction maison.

Pour pousser la réflexion plus loin, je voulais utiliser Spring.net pour obtenir la traduction. Cette solution à pour avantage de ne passer que par le contexte pour obtenir cette dernière, peut importe dans quel fichier elle se trouve. Il suffit alors de paramétrer dans le fichier `App.Config` le chemin de chaque fichier *.resx.

Pour ce faire, rien de plus facile: Spring.net fournit une classe qui recense un certain nombre de `ResourceManager`. En référençant donc notre `ResxResourceManager` qui pointe sur notre fichier *.resx, le contexte Spring sera alors capable de fournir les bonnes traductions si on l'interroge. Pour obtenir une traduction dans la culture courante, il suffira alors d'écrire ceci:
```C#
ContextRegistry.GetContext().GetMessage("MaClef");
```
Le XML de configuration ressemble à ça:
```XML











```
Vous pouvez voire concrètement ce que ça donne avec [un petit exemple](http://www.box.net/shared/al00ws8w0s).

[![kick it on DotNetKicks.com](http://www.dotnetkicks.com/Services/Images/KickItImageGenerator.ashx?url=http%3a%2f%2fgrozeille.wordpress.com%2f2008%2f04%2f27%2futiliser-des-resx-externes-avec-springnet%2f&border=6699cc&bgcolor=99cc66&cbgcolor=f3f6ec)](http://www.dotnetkicks.com/kick/?url=http%3a%2f%2fgrozeille.wordpress.com%2f2008%2f04%2f27%2futiliser-des-resx-externes-avec-springnet%2f)

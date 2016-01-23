---
author: grozeille
comments: true
date: 2009-07-09 06:45:15+00:00
layout: post
slug: integration-continue-en-net
title: Intégration Continue en .Net
wordpress_id: 205
categories:
- Developpement
tags:
- .net cruise-control
- build
- tools
---

Bonjour les fans de .Net et d'[intégration continue](http://en.wikipedia.org/wiki/Continuous_integration)!
J'affectionne [Hudson](https://hudson.dev.java.net/) en ce moment, et je l'applique de plus en plus pour .Net. Je l'utilise en ce moment pour analyser le code et "gronder" les membres du projet qui codent "mal".
A défaut d'avoir un plugin [Sonar](http://sonar.codehaus.org/) pour .Net, Hudson et son [plugin Violations](http://wiki.hudson-ci.org/display/HUDSON/Violations) fait déjà pas mal de bon rapports.
Ce plugin supporte pas mal d'outils comme [FXCop](http://msdn.microsoft.com/en-us/library/bb429476(VS.80).aspx) ou [StyleCop](http://redsolo.blogspot.com/2008/05/hudson-adds-support-for-stylecop.html). Concernant ce dernier, le plugin bug avec les chemins absolus et les "\", j'aimerai bien le corriger mais je n'ai pas trop le temps :)
J'ai regardé les sources de ce plugin, et ça semble assez simple.
![HudsonMonitor](http://grozeille.files.wordpress.com/2009/07/img_0091.jpg?w=300)


_Ma petite application Winform qui lit le flux RSS pour afficher l'état des projets.
En ce moment c'est bien rouge... mais ça peut aussi être jaune ou vert ;) __
_


Il supporte aussi [CPD](http://pmd.sourceforge.net/cpd.html) qui détecte les Copier/Coller (sans doute la source de bug la plus importante dans équipe), mais il ne supporte pas le C#... Idem, j'aurai bien aimé avoir le temps de l'implémenter.
J'ai vu que [TeamCity](http://www.jetbrains.com/teamcity/) avait sa propre tâche "[Duplicates Finder](http://www.jetbrains.net/confluence/display/TCD3/Duplicates+Finder+(.NET))", mais ça n'a pas l'air d'être indépendant.
[NDepend](http://www.ndepend.com/) est magique et répond à ce besoin, mais il est payant, et non supporté par Hudson.
J'ai eu aussi envie de tester [Gendarme](http://www.mono-project.com/Gendarme). Encore une fois, si le temps me le permet, j'ajouterai bien le support des rapports Gendarme dans le plugin Hudson-Violations. En attendant, je peux toujours convertir le XML de Gendarme en XML FXCop (je n'ai pas encore étudié la faisabilité).





Je sais que faire évoluer Hudson ou CPD ou encore Sonar nécessite des connaissance en Java.
Mais le constat est que ces outils sont matures en Java, et les "pâles copies" en .Net ne sont pas à la hauteur (comme [CC.Net](http://cc.net/) par exemple).
L'investissement est très variable entre les différents projets (Violation, Sonar, etc), mais je suis convaincu qu'il en vaut le coup.





Et vous, qu'en pensez-vous?





Faut-il absolument faire du .Net pour du .Net? et s'investir sur un CC.Net vieillissant?
Hudson est-il un bon choix d'investissement?
Ne faut-il pas mieux privilégier l'investissement sur Sonar pour les rapports d'analyse?
Et la question la plus important: y a-t-il des personnes motivées par ça?
Je pense même que ça mérite un "meta-projet opensource" avec son site web, qui regroupe les outils de build et d'analyses de code en .Net, afin d'offrir une solution "packagée" pour .Net.














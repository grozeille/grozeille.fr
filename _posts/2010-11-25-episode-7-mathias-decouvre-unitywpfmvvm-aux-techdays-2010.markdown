---
author: grozeille
comments: true
date: 2010-11-25 21:07:07+00:00
layout: post
slug: episode-7-mathias-decouvre-unitywpfmvvm-aux-techdays-2010
title: 'Episode 7 : Mathias découvre Unity+WPF+MVVM aux Techdays 2010'
wordpress_id: 511
categories:
- Developpement
- DotNetServer
tags:
- .Net
- eclipse
- IOC
- mvc
- mvvm
- rcp
- unity
- WPF
---

Je vous ai parlé de ma découverte de .Net dans l'[épisode 6](http://grozeille.com/2010/11/13/episode-6-mathias-decouvre-net/).
J'ai constaté un gros contraste avec Java: j'avais l'impression que Java était compliqué (EJB et tout ça) et que .Net était simple.

Cette simplicité n'est pas toujours positive, on peut même dire que Microsoft est "maudit" par ce fléau: rester attractif pour les développeurs débutants.

En général, cela donne des frameworks "sales" avec un fort couplage du code métier avec les interfaces, impossible à tester unitairement bien sûr.

Pour pouvoir découpler tout cela, on distingue 3 couches:



	
  * L'interface, appelée "view" ou "presenter", c'est le moyen d'afficher l'information

	
  * La logique métier, appelée "model", c'est ce que l'on va pouvoir tester à l'aide de tests unitaires

	
  * Les actions ou commandes, qui représente une action de l'interface par l'utilisateur qui va déclencher un traitement


Mais quand on sépare les responsabilités en plusieurs objets, on se retrouve avec un nouveau problème : comment coupler les vues, contrôleurs, etc. ? Comment "broker" les actions ?

Il y a une solution à cela: l'[IOC](http://en.wikipedia.org/wiki/Inversion_of_control). On peut dire aussi que le[ Databinding](http://msdn.microsoft.com/en-us/library/ms752347.aspx) en est une autre.
Si Microsoft avait un train de retard sur les Framework IOC, ils connaissaient néanmoins déjà le problème depuis un moment, puisqu'ils l'avaient en partie résolu dans [CAB](http://msdn.microsoft.com/en-us/library/ff648747.aspx).
C’est donc sans surprise que Microsoft nous livre son framework d’IOC "officiel" basé sur l’existant de CAB : [Unity](http://unity.codeplex.com/).

A la sortie d'Unity, j'étais déjà tellement convaincu par Spring.net que je n'ai jamais adopté le framework de Microsoft. De plus, les alternatives OpenSources étaient  bien présentes: [Castle Windsor](http://www.castleproject.org/container/), [Ninject](http://ninject.org/), [Autofac](http://code.google.com/p/autofac/), etc.

A noter que les framework tel que CAB/RCP rendent vos clients lourds "extensibles", ce qui veut dire qu'un plugin va pouvoir greffer de "vues" dans l'interface, et s'abonner aux "commandes": chose tout à fait faisable avec de l'IOC.

Mais les frameworks IOC ne font pas tout, et ne suffisent pas à fournir une véritable architecture MVC pour client lourd, même s'ils peuvent nous y aider ([voir mon poste précédent](http://grozeille.com/2010/11/13/episode-6-mathias-decouvre-net/)).

Pour résoudre le fléau du couplage fort entre l'interface et le code métier, Microsoft a sortie quelque chose de révolutionnaire: WPF et Silverlight!
Avec la venue de WPF et Silverlight, la communauté .Net OpenSource a commencé à se pencher alors sur le problème du MVC pour les applications lourdes. Divers frameworks apparaissent alors, comme Prism: [http://compositewpf.codeplex.com/](http://compositewpf.codeplex.com/)


[![](http://grozeille.files.wordpress.com/2010/11/compositewpfapp1.png?w=300)](http://grozeille.files.wordpress.com/2010/11/compositewpfapp1.png)


[](http://grozeille.files.wordpress.com/2010/11/compositewpfapp1.png)

Mais le MVC, comme on le connait dans le monde Web, ne s'applique pas bien aux clients lourds, surtout si on veut exploiter le Databinding et les événements.

Très franchement, je ne me suis jamais vraiment passionné pour WPF/Prism/etc. mais je voyais bien que quelque chose de gros était en train de venir...
J'ai ensuite assisté aux [Techdays 2010](http://www.microsoft.com/france/vision/mstechdays10/) et j'en ai profité pour me mettre à jours sur le sujet.
Les sessions étaient d’ailleurs très accès sur Silverlight/WPF mais aussi sur le nouveau modèle [MVVM](http://en.wikipedia.org/wiki/Model_View_ViewModel) (Model-View-ViewModel), et avec une bonne dose d’Unity bien sûr…
J’ai alors été très agréablement surpris par ces présentations, surtout celle qui montre comment supprimer tout le « code behind » des interfaces XAML avec des ViewModel et des Commands.

**Pour mieux comprendre de quoi je parle, aller voir vite le [screencast ici](http://www.microsoft.com/france/vision/mstechdays10/Webcast.aspx?EID=5740b16f-770a-459c-9a93-4a321f4e8059)!!!**

Bref, je ne sais pas si vous me suivez, mais l’IOC, le RCP, le MVC, la gestion de plugins, tout ça c’est intimement lié !

Petit à petit, .Net rattrape le retard vis-à-vis d’Eclipse RCP !
On peut même dire que .Net a pris de l'avance avec Silverlight/WPF, puisque la rédaction des interfaces en XML n'est qu'au stade de proposition pour Eclipse 4: [http://wiki.eclipse.org/images/a/ab/XWT.pdf](http://wiki.eclipse.org/images/a/ab/XWT.pdf)

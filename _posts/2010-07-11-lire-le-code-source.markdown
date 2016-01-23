---
author: grozeille
comments: true
date: 2010-07-11 09:03:22+00:00
layout: post
slug: lire-le-code-source
title: Lire le code source...
wordpress_id: 423
categories:
- Developpement
tags:
- c++
- opensource
- sourcecode
---

... ce n'est pas aussi passionnant qu'un roman, mais c'est quelque chose que tout développeur devrait pratiquer.

Si vous n'êtes pas convaincu, allez lire ça [http://www.skorks.com/2010/05/why-i-love-reading-other-peoples-code-and-you-should-too/](http://www.skorks.com/2010/05/why-i-love-reading-other-peoples-code-and-you-should-too/)

A mes débuts, je "singeais" les autres, je copiais/collais du code trouvé sur le Net, sans forcement comprendre tout ce qu'il faisait.
En général, je trouvais ce code sur des forums comme [developpez.com](http://www.developpez.com/), [codes-sources](http://www.codes-sources.com/) ou [The code project](http://www.codeproject.com/).
J'avoue qu'aujourd'hui, je consulte rarement les forums (à part celui de [Ubuntu-FR](http://ubuntu-fr.org/), si vraiment je ne trouve pas l'info sur leur merveilleux [wiki](http://doc.ubuntu-fr.org/))

Le Web a évolué en 2.0. [Stackoverflow](http://stackoverflow.com/) en est un pur produit: c'est un "forum" que je conseille vivement pour trouver des solutions à vos problèmes.

Mais la meilleur façon d'apprendre, c'est encore de lire du code, du vrai, du brut.
Il n'y a pas de honte à ne pas être un "Shakespeare" du C#... certaines personnes écrivent des romans et d'autres des articles de magazines... on ne fait pas tous  le même boulot.

[caption id="attachment_427" align="aligncenter" width="300" caption="Mon vrai premier "ordinateur" a été un Amstrad CPC 6128, et pour jouer à un jeux... il fallait le coder en recopiant le listing du bouquin!"][![](http://grozeille.files.wordpress.com/2010/07/cpc6128_circles_listing1.gif?w=300)](http://grozeille.files.wordpress.com/2010/07/cpc6128_circles_listing1.gif)[/caption]

Aujourd'hui, le Web 2.0 vous offre un outil magique pour lire du code: j'ai nommé [http://www.google.com/codesearch](http://www.google.com/codesearch) !
C'est devenu un reflex pour moi: quand je ne comprend pas une fonction, au lieux d'aller consulter la [MSDN](http://msdn.microsoft.com/en-us/default.aspx), je cherche du code qui exploite cette dernière.

A noter que cette magie n'existerai pas sans l'émergence de l'OpenSource. S'il y avait principalement que [Sourceforge](http://sourceforge.net/) au début, vous pouvez maintenant héberger vos projets OpenSource sur de nombreux sites comme [Google Code](http://code.google.com/), [Github](http://github.com/), [Bitbucket](http://bitbucket.org/), [Codeplex](http://www.codeplex.com/), etc.

Bien sûr, les blogs restent une bonne source d'information. En ce moment vous pouvez y voir pas mal d'article sur les "CoRoutine" avec une utilisation astucieuse du mot clé "yield": [http://www.codinginstinct.com/2010/06/sequential-async-using-coroutines.html](http://www.codinginstinct.com/2010/06/sequential-async-using-coroutines.html)

Si j'ai réussie à vous donner envie de lire, je vous conseille de [regarder ceci](http://github.com/MarkNijhof/Fohjin).
J'ai découvert ce code lors de mon apprentissage de CQRS (cf [GoogleGroups d'ALT.Net](http://groups.google.fr/group/parisaltnet/browse_thread/thread/d98d42db4ef3721b)) et je le trouve très élégant (pas étonnant qu'on le trouve sur [http://elegantcode.com/](http://elegantcode.com/) :) )

Lire du code provenant d'autres langages peut aussi vous apporter beaucoup: ne restez pas enfermé dans vos habitudes, et regardez les pratiques des autres. C'est en cherchant quelque chose sur Google Code Search que je suis tombé sur le code suivant: [http://www.google.com/codesearch/p?hl=en#LH6NMiZyrsw/trunk/src/documentpresenter.vala](http://www.google.com/codesearch/p?hl=en#LH6NMiZyrsw/trunk/src/documentpresenter.vala)

Ça ressemble à du C#? Mais c'est du Vala. Le projet est un IDE, avec une architecture MVP (Model Vue Presenter) avec de l'injection de dépendance etc. Je le trouve très lisible, clair et concis.
Pour ceux qui ne connaissent pas Vala, regarder ici:  [http://live.gnome.org/Vala/QuickIntroForCSharpProgrammers](http://live.gnome.org/Vala/QuickIntroForCSharpProgrammers)

En parlant d'autres langages, je vous conseille quand même d'éviter de lire du [Brainfuck](http://en.wikipedia.org/wiki/Brainfuck) :)  je ne veux pas être responsable de votre autisme.

Je n'ai plus qu'a vous souhaitez bonne lecture ;) Mais allez bronzer un peu quand même :p

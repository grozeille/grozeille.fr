---
author: grozeille
comments: true
date: 2010-11-13 00:25:08+00:00
layout: post
slug: episode-6-mathias-decouvre-net
title: 'Episode 6: Mathias découvre .Net!'
wordpress_id: 503
categories:
- Developpement
- DotNetServer
tags:
- .Net
- eclipse
- mvc
- osgi
- rcp
- spring
---

En fait, je triche, les épisodes ne sont pas dans l’ordre chronologique.
Je n’ai pas découvert .Net après Java, mais en même temps.

C’était le 6 Janvier 2005, [j avais blogué](http://grozeille.com/2005/01/06/mono-le-retour/) à ce sujet: j’avais découvert qu’avec Mono, il était possible d'exécuter un même programme EXE sous Windows comme sous Linux ! J'en avais la larme à l'œil...

Ce qui m'a le plus impressionné c'était de voir qu'il était possible d'exécuter du Java dans .Net grâce à [IKVM ](http://www.ikvm.net/)! Cela marchait tellement bien qu’ils ont réussi à exécuter [Eclipse sous .Net](http://weblog.ikvm.net/PermaLink.aspx?guid=1aecaf4e-24c0-4f96-861b-f3b4473c7525) ! Mais ce n’était qu’expérimental à l'époque…

En découvrant .Net, j’ai tout de suite pris conscience du retard par rapport à Java, et j’ai alors voulu m’y atteler.
J’ai alors commencé à réaliser un framework « RCP » comme celui d’Eclipse, mais full .Net. Voici le résultat à l’époque :

[![](http://grozeille.files.wordpress.com/2010/11/oldrcp.png?w=300)](http://grozeille.files.wordpress.com/2010/11/oldrcp.png)

On pouvait réaliser des plugins qui fournissent des vues qui s’encrent dans différents endroits, que ce soit dans la fenêtre principale ou dans un onglet d’édition.
J'en était plutôt fier, encore aujourd'hui... j'ai bien envie de le porter avec les technos modernes d'aujourd'hui...

C’est aussi à cette époque que j’ai découvert [Spring](http://www.springsource.org/about), et au même titre [Spring.Net](http://www.springframework.net/), que j’ai utilisé dans mon entreprise pour réaliser, avec [Romain](http://codingly.com/), un framework MVC Winforms.

J’ai aussi découvert d’autres framework IOC, et par la même occasion CAB de Microsoft ([Composite Application Bloc](http://msdn.microsoft.com/en-us/library/ff648747.aspx)), mais sans en être convaincu.

[![](http://grozeille.files.wordpress.com/2010/11/ic15563.gif?w=300)](http://grozeille.files.wordpress.com/2010/11/ic15563.gif)

A l'époque, on commençait à parler d'OSGI, mais je n’avais pas assez de connaissance dans le domaine

En conclusion, je restais sur ma fin avec .Net, et j'en étais même frustré. Mais j'ai toujours été convaincu que c'était aussi "une terre d’opportunités" et que je pouvais faire quelque chose...
L'IOC, le MVC pour client riche, RCP, OSGI... les idées émergeaient déjà, mais n'était pas matures.

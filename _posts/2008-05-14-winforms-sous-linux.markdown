---
author: grozeille
comments: true
date: 2008-05-14 21:50:20+00:00
layout: post
excerpt_separator: <!--more-->
slug: winforms-sous-linux
title: Winforms sous Linux
wordpress_id: 57
categories:
- Blabla
- linux
tags:
- .Net
- GTK
- linux
- mono
- UI
- web
- WPF
---

Après 4 ans de développement, la communauté Mono est enfin parvenu à l'implémentation complète des Winforms : [http://tirania.org/blog/archive/2008/May-13.html](http://tirania.org/blog/archive/2008/May-13.html)

On peux se demander "oui, mais pourquoi faire?" et je ne trouve pas de réponse à la question. En effet, il arrive souvent qu'une application .Net possède du Legacy et donc des dépendances COM ou P/Invoke. Dans ce cas, on ne peut pas la migrer (pour tester si une migration est possible: [http://www.mono-project.com/Moma](http://www.mono-project.com/Moma))

Mais comme je suis exigent en terme d'interface, je n'aime pas avoir une application "alien" qui ne ressemble pas à mon environnement Linux (GTK/QT). Certes, il est prévu d'avoir un meilleur support du moteur de thème lors du prochain [GSoC](http://en.wikipedia.org/wiki/Google_Summer_of_Code), donc _wait and see_.

Rappelons que les Winforms sont une sur-couche .Net de l'API WIN32. Cette dernière n'existant pas sous Linux et MacOS, j'en profite alors pour féliciter les équipes de Mono pour leur implémentation "from scratch".

D'un autre coté, l'implémentation WPF chez Mono avance plutôt vite. D'ailleurs, la première release de [Moonlight vient de sortir](http://tirania.org/blog/archive/2008/May-13-1.html). Il n'y a pas de dépendance WIN32 dans ce cas, et je vois plus l'avenir des applications .Net dans ce sens. Mais l'approche WPF est d'avoir un thème propre à l'application, comme c'est le cas pour les sites Web, on obtient la même interface sous Linux et Windows (et MacOS). Mais finalement je trouve que ces interfaces ne s'intègrent à aucun des 3 environnements.


<!--more-->

J'avais déjà rédigé un billet sur la guerre entre les technologies de "présentation" dans le domaine du Web (Ajax/Flash/etc.). Je ne vous l'apprend pas, le monde "Desktop" et "Web" convergent. L'idée est plutôt simple: aujourd'hui on doit exécuter un OS qui héberge des applications "Desktop", et on doit exécuter un navigateur pour les applications Web. On obtient une certaines confusion entre la barre des tâches pour les application et les onglets pour les sites Web. Tout ceci est beaucoup mieux expliqué [sur ce blog](http://labs.mozilla.com/2007/10/prism/).

Mais de plus en plus, le navigateur ne sert qu'à exécuter un plugin (Silverlight/Flash/Java) qui lui charge l'application.
L'objectif est de lancer une application Web comme une application "Dekstop", en exécutant le dis plugin en _standalone_, ou de passer par un "mini navigateur" (qui ne sert que pour le rendu HTML+Ajax, sans navigation etc). C'est en tout cas ce que propose [Adobe Air](http://www.adobe.com/products/air/) ou [Mozilla Prism](http://wiki.mozilla.org/Prism).

Il va donc être difficile de distinguer une application "Desktop" ou "Web". Ceci me fait un peu penser aux Widgets du [Dashboard](http://upload.wikimedia.org/wikipedia/en/7/72/Leopard_Dashboard_BIG.png) sous MacOS (ou autre plagia).

Au même titre que le Web se rapproche du Bureau, les applications "lourdes" copient les techniques du Web question apparence. Il y a des tentatives d'utilisation de [CSS en Swing/SWT](http://blog.developpez.com/index.php?blog=119&title=moteur_css_pour_swing_et_swt_1), mais l'exemple le plus flagrant est la description de l'interface à l'aide de XML comme dans [XAML](http://en.wikipedia.org/wiki/XAML).

On obtient ainsi des applications "Desktop" ne copiant pas du tout le style standard de l'OS, mais [ayant son propre thème](http://music.aol.com/help/syndication/desktop-widgets?promoid=BTLNP) telle un site Web.

Le résultat peut s'avérer très jolie, très ergonomique, mais très "inconsistant" avec les autres applications. Pourquoi devrais-je apprendre une nouvelle interface? Pourquoi ne pas utilise un standard? Pourquoi ne pas me laisser choisir mon thème dans l'OS plutôt que de me l'imposer pour une application donnée?

Personnellement, je ne suis pas fan de toutes ces interfaces différentes, [et je ne suis pas le seul](http://arstechnica.com/articles/culture/microsoft-learn-from-apple-II.ars/4).
Pour revenir sur l'OS Linux, un grand effort est fourni pour rendre les interfaces homogènes. On peut par exemple citer le [projet Portland](http://en.wikipedia.org/wiki/Portland_Project) allant dans cette direction. Je peux alors apprécier ces efforts puisqu'il m'est devenu difficile de distinguer une application QT dans mon environnement GTK (essayez [Skype sous Linux ](http://www.skype.com/download/skype/linux/)pour vous en convaincre).

Je voulais aussi citer Redhat comme, à mon humble avis, les pionniers en matières d'homogénéisation avec leur thème [Bluecurve](http://en.wikipedia.org/wiki/Bluecurve) identique sous KDE est Gnome. D'autre projets ont suivis dans le même genre comme [Tango](http://tango.freedesktop.org/Tango_Desktop_Project).

Enfin, les interfaces graphiques sont en pleines évolutions ces derniers temps, avec l'exploitation des cartes graphiques récentes, offrant des "[eye candy](http://compiz.org/Home/Screenshots)" très alléchants. Le monde GTK est en [pleine réflexion](http://arstechnica.com/articles/culture/reinventing-gtk.ars) pour les futures versions, et les thèmes [supportent de plus en plus d'effet](http://www.cimitan.com/blog/2007/12/12/gtk-rgba-transparent-widgets-with-the-murrine-engine/).
Je préfère de loin cette approche ou l'OS propose un système de thème avancé (avec des techniques [proches du CSS](http://ubuntuforums.org/showthread.php?t=377397)) et l'applique à toutes les applications, rendant le tout homogène. Néanmoins, je distinguerai toujours les applications type "Widget" qui ressemblent plus à de "mini-site" ou "application Web" qui elle ont une apparence propre à elles.

Comment seront les interfaces des OS du futures? Va-t-on vers un gros bordel graphique, ou une homogénéisation? WPF va-t-il percer sous Linux? Quels vont être les applications Winforms qui vont être migré sous Linux?

---
author: grozeille
comments: true
date: 2010-03-11 14:37:29+00:00
layout: post
slug: outil-de-diffmerge
title: Outil de diff/merge
wordpress_id: 329
categories:
- Developpement
tags:
- diff
- merge
- svn
---

A l'origine, je voulais parler des différents outils de diff/merge car je n'étais pas fan de KDIFF3 fournit avec Tortoise HG.

Comme je suis un garçon qui se disperse, j'ai commencé à écrire un soit disant "petit billet" qui est devenu tellement gros, que j'ai oublié de quoi je voulais parler à l'origine.

Donc, pour ceux qui ne comprennent pas ce que c'est que Tortoise HG ou Mercurial, [lisez le billet précédent](http://grozeille.com/2010/03/11/gestionnaires-de-sources-decentralise/) ;)

Revenons à nos moutons: je ne suis pas fan de KDIFF3. J'avais fait une étude des différents outils de Diff/Merge pour Windows, et j'ai décidé de le publié pour la prospérité :)

Avant de commencer, je tiens à préciser la différence entre un Diff et un Merge:



	
  * Diff: comparaison entre 2 fichiers seulement.

	
  * Merge: comparaison entre 3 fichiers: l'original, le votre, et le modifier par quelqu'un d'autre. C'est comme ça qu'on résout les conflits quand il y en a avec un gestionnaire de source.






### KDiff3



[http://kdiff3.sourceforge.net/](http://kdiff3.sourceforge.net/)

[![](http://grozeille.files.wordpress.com/2010/03/kdiff3.png?w=300)](http://grozeille.files.wordpress.com/2010/03/kdiff3.png)

Outil à l'origine de [KDE](http://www.kde.org/). Je l'ai très peu utilisé, je me demande pourquoi...



### TortoiseMerge



[http://tortoisesvn.tigris.org/TortoiseMerge.html](http://tortoisesvn.tigris.org/TortoiseMerge.html)

[![](http://grozeille.files.wordpress.com/2010/03/tortoisemerge.png?w=300)](http://grozeille.files.wordpress.com/2010/03/tortoisemerge.png)

Fournit avec TortoiseSVN, il est très bien. Le choix des couleurs était parfois douteux, et rendait la lecture du code difficile (voir illisible) mais c'est corrigé depuis une certaine version.
Fonctionne bien avec les Merge, mais il est dommage de ne pas pouvoir éditer le source pendant la résolution d'un conflit (c'est très souvent nécessaire lors d'un conflit).
Il est aussi dommage de ne pas pouvoir ignorer le changement de type "espace" ou "tabulation".



### WinMerge



[http://winmerge.org/](http://winmerge.org/)

[![](http://grozeille.files.wordpress.com/2010/03/winmerge.png?w=300)](http://grozeille.files.wordpress.com/2010/03/winmerge.png)

Contrairement à ce que son nom indique, WinMerge ne fait pas les Merges, mais seulement les Diff.
Il est beaucoup plus clair et agréable que TortoiseMerge, et l'édition du source est possible pendant la comparaison (c'est pourquoi je l'utilise souvent).

WinMerge fonctionne aussi avec les répertoires, et ça c'est trop class :)



### DiffMerge



[http://www.sourcegear.com/diffmerge/](http://www.sourcegear.com/diffmerge/)

[![](http://grozeille.files.wordpress.com/2010/03/diffmerge1.png?w=300)](http://grozeille.files.wordpress.com/2010/03/diffmerge1.png)

Certains préfèrent la vue "3 colonnes" pour effectuer un Merge. C'est que que DiffMerge vous propose.



### Meld



[http://meld.sourceforge.net/](http://meld.sourceforge.net/)

[![](http://grozeille.files.wordpress.com/2010/03/meld1.png?w=300)](http://grozeille.files.wordpress.com/2010/03/meld1.png)

Si KDIFF3 vient du monde KDE, Meld vient du monde Gnome.

Je triche un peu: ce n'est pas un outil Windows. Mais il est possible de le faire marcher sous Windows (installation de Python+GTK): [http://live.gnome.org/Meld/Windows](http://live.gnome.org/Meld/Windows).
Je l'ai aussi fait marcher avec [CoLinux](http://www.colinux.org/) (Linux natif sous Windows).

<del>Si j'en ai la patience, je vous ferais un petit package prêt à installer (avec python+gtk embarqué).</del>
Comme j'ai eu la patience aujourd'hui, voici le Setup pour Windows de Meld (EN EXCLUSIVITE!!!): [http://bitbucket.org/grozeille/meld/downloads/Install.exe](http://bitbucket.org/grozeille/meld/downloads/Install.exe)



### Eclipse



[http://www.polarion.com/products/svn/subversive.php](http://www.polarion.com/products/svn/subversive.php)

[![](http://grozeille.files.wordpress.com/2010/03/sc6b.png?w=300)](http://grozeille.files.wordpress.com/2010/03/sc6b.png)

Je triche encore, mais pour ceux qui utilise SVN, Eclipse et son connecteur offre une vue "Synchronize" très pratique que je regrette sous VisualStudio.

Elle permet en effet de vous facilité la phase "j'update puis je commit" avec une vue globale de ce qui va se passer. L'éditeur permet de gérer aussi bien les Diff que les Merge.
Pour ma part, j'ai souvent un Eclipse d'ouvert pour diverses choses que VisualStudio ne fait pas (ou mal) comme l'édition de Javascript ou de schéma XSD ou WSDL.
Cela ne me gêne donc pas d'utiliser le même outil pour les Commit/Update SVN, mais j'avoue qu'Eclipse est loin d'être léger et qu'il est plus simple d'utiliser ToirtoiseMerge ou WinMerge dans certaines conditions.



### NotePad++



[http://notepad-plus.sourceforge.net/fr/site.htm](http://notepad-plus.sourceforge.net/fr/site.htm)

[![](http://grozeille.files.wordpress.com/2010/03/notepaddiff.png?w=300)](http://grozeille.files.wordpress.com/2010/03/notepaddiff.png)

Parfois, j'utilise Notepad++ pour un simple diff. C'est très léger mais pratique.



### WinDiff



[http://en.wikipedia.org/wiki/WinDiff](http://en.wikipedia.org/wiki/WinDiff)

[![](http://grozeille.files.wordpress.com/2010/03/windiff.png?w=300)](http://grozeille.files.wordpress.com/2010/03/windiff.png)

Saviez-vous qu'avec l'installation de VisualStudio, qui inclut le "Plateform SDK" vous aviez déjà à votre disposition un diff visuel?

J'avoue, il pique les yeux...



### Perforce Merge



[http://www.perforce.com/perforce/products/merge.html](http://www.perforce.com/perforce/products/merge.html)

[![](http://grozeille.files.wordpress.com/2010/03/perforcemerge.png?w=300)](http://grozeille.files.wordpress.com/2010/03/perforcemerge.png)

Perforce est un gestionnaire de code source, pas très populaire. Dans la suite d'outils offerts avec Perforce, il y a PerforceMerge, qui est gratuit.
J'avoue être agréablement surpris car il est clair et gère bien les Merges.



### Araxis



[http://www.araxis.com/merge/index.html](http://www.araxis.com/merge/index.html)

[![](http://grozeille.files.wordpress.com/2010/03/araxis.png?w=300)](http://grozeille.files.wordpress.com/2010/03/araxis.png)

Je triche ENCORE UNE FOIS: ce n'est PAS un outil gratuit.
Mais je trouve qu'il a le mérite d'être cité, car je l'ai déjà utilisé en entreprise, et qu'il est très efficace (avec vue Merge en 3 colonnes).



### Autres...



Pour tous ceux que je n'ai pas cités, vous avez une liste exhaustive sur Wikipedia: [http://en.wikipedia.org/wiki/Comparison_of_file_comparison_tools](http://en.wikipedia.org/wiki/Comparison_of_file_comparison_tools)

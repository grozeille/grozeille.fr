---
author: grozeille
comments: true
date: 2010-03-11 09:11:09+00:00
layout: post
slug: gestionnaires-de-sources-decentralise
title: Gestionnaires de sources décentralisé
wordpress_id: 321
categories:
- Developpement
tags:
- git
- hg
- mercurial
- scm
- svn
- tortoise
---

Voici un petit billet pour parler des outils de gestion de source, car j'ai voulu résumer tout ça dans un seul endroit.

Si j'ai beaucoup travaillé avec [Subversion (SVN)](http://subversion.tigris.org/) depuis de nombreuses années, j'en ai aussi payé les frais, et j'ai adopté aujourd'hui les gestionnaires de sources décentralisés.
SVN reste un très bon choix, et impose de bonnes pratiques sans imposer sa façon de travailler.
Mais j'ai souvent souffert des problèmes suivants:



	
  * Merges compliqués, peut-être résolu avec SVN 1.5 et TortoiseSVN 1.5, mais ça reste difficile par moment

	
  * Lenteur, que ce soit en Updatant/Commitant, ou avec l'utilisation de TortoiseSVN

	
  * "Rename" compliqué, puisqu'il faut faire un "Move" avec SVN et pas avec le FileSystem ou dans l'IDE



[caption id="attachment_326" align="aligncenter" width="400" caption="Trop facile les branches avec Tortoise! ;)"][![](http://grozeille.files.wordpress.com/2010/03/48479087_705a7f3087-1.jpg)](http://grozeille.files.wordpress.com/2010/03/48479087_705a7f3087-1.jpg)[/caption]

C'est pour ces raisons que je suis fan de [GIT](http://git-scm.com/) ou [Mercurial (HG)](http://mercurial.selenic.com/), avec une préférence pour ce dernier. J'avais commencé à utilisé GIT, mais un ami m'a dit qu'il trouvait Mercurial plus facile: après avoir fait l'essaie, je confirme!

Si j'ai opté pour SVN à l'époque, c'est sans doute grâce à l'outillage qui est autour:



	
  * [TortoiseSVN](http://tortoisesvn.tigris.org/)

	
  * [AnhkSVN](http://ankhsvn.open.collab.net/)

	
  * [VisualSVN](http://www.visualsvn.com/visualsvn/)

	
  * [VisualSVN Server](http://www.visualsvn.com/server/) (ou comment installer un Apache+SVN facilement en quelques cliques)

	
  * [Subversive](http://www.polarion.com/products/svn/subversive.php)

	
  * etc.





Ce fut aussi sans doute parce que SVN s'intégrait bien avec d'autres outils, comme les bugs-trackers ([Track](http://trac.edgewall.org/) ou [Redmine](http://www.redmine.org/)).

Si j'opte pour GIT ou Mercurial, c'est pour les mêmes raisons: les outils existent!
Pour GIT:



	
  * [msysgit](http://code.google.com/p/msysgit/)

	
  * [TortoiseGIT](http://code.google.com/p/tortoisegit/)

	
  * [Git Extension](http://sourceforge.net/projects/gitextensions/)

	
  * [EGit](http://www.eclipse.org/egit/)

	
  * [GitX](http://gitx.frim.nl/seeit.html)




Pour Mercurial:

	
  * [Tortoise HG](http://tortoisehg.bitbucket.org/)

	
  * [VisualHG](http://visualhg.codeplex.com/)

	
  * [Et plein d'autres...](http://mercurial.selenic.com/wiki/OtherTools)



La puissance de GIT et Mercurial c'est aussi de pouvoir convertir un repository SVN rapidement, ou même l'utiliser comme "main branch". A ce niveau, j'ai eu une meilleure expérience avec Mercurial.

Mais ce n'est pas tout, si GIT/HG explose en puissance, c'est qu'ils offrent un repository "officiel" gratuit!
Petite anecdote: je voulais faire de la place sur mon disque dur plein à craqué, et en faisant le ménage je suis tombé sur un dossier contenant des backups de mes sources de mes projets perso. Ce fut un beau moment de nostalgie, j'en reviens pas d'avoir fait un "simulateur de vie en 3D en Java" ou un projet avec "Eclipse RCP" ou encore un "framework RCP en .Net"...
Il ne fallait absolument pas perdre tout ça, il me fallait le mettre sur un SVN. A l'époque, j'avais des repos SVN locaux, mais pour ne rien perdre en cas de crash, je me suis dit que je vais tout backuper sur le plus gros disque du monde: Internet.
J'ai trouvé [Assembla](http://www.assembla.com/) à l'époque, qui inclut le bug-tracker Trac. J'aurai pu choisir [Google Code](http://code.google.com/hosting/), mais je n'y ai pas pensé. Quand à [CodePlex](http://www.codeplex.com/) ce n'était que du [TFS](http://en.wikipedia.org/wiki/Team_Foundation_Server) à l'époque, mais maintenant il y a un [pont SVN](http://www.codeplex.com/SvnBridge).

Avec la découverte de GIT, j'ai aussi découvert [GitHub](http://github.com/grozeille/) et ça a changé ma vie: Wiki light, bug-tracker light, interface Web très soigné, et très simple d'utilisation (très facile à créer plusieurs repos). [Gitorious](http://gitorious.org/~grozeille) est aussi un très bon choix, mais j'ai l'impression qu'il n'a pas connu le même succès.

Et c'est avec joie que j'ai découvert que Mercurial possède aussi son repository "officiel" tout comme GitHub: [BitBucket](http://bitbucket.org/). Les 2 sont très comparables, on dirait presque des clones.

J'ai une petite pensé pour [Bazaar](http://bazaar.canonical.com/en/) qui est aussi un gestionnaire de sources décentralisé, qui est très utilisé dans le monde Linux (produit de [Canonical](http://www.canonical.com/) donc très utilisé par [Ubuntu](http://www.ubuntu.com/)) mais qui n'a pas séduit la communauté des développeurs (manque d'outils? trop complexe? c'est la vie?) pour ceux qui veulent quand même le tester, [TortoiseBZR](http://wiki.bazaar.canonical.com/TortoiseBzr) existe.

Amusez-vous bien sur GIT ou Mercurial, apprenez à maitriser l'outil, car c'est grâce à vos connaissance que vous les verrez apparaitre dans vos entreprise.


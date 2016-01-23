---
author: grozeille
comments: true
date: 2009-05-24 15:18:50+00:00
layout: post
slug: alt-net-adaptive-object-modeling
title: 'ALT.Net: Adaptive Object Modeling'
wordpress_id: 176
categories:
- ALT.Net
- Developpement
---

Mardi 19 Mai a eu lieu la [session ALT.Ne](http://www.altnetfr.org/2009/05/05/altnet-paris-13-adaptive-object-modeling/)t sur l’Adaptive Object Modeling présenté par [Sébastien Ros](http://www.dotnetguru2.org/sebastienros/).
Je voulais simplement dire que j’étais content d’assister à cette rencontre : la présentation de Sébastien était courte et intéressante (et drôle en plus !). En résumé : le type de présentation qui ne nous laisse pas le temps de s’endormir.
Cela nous a aussi permis de débattre de divers sujet à la fin de la présentation : nous avons voté pour des sujets qui nous intéressent, puis nous nous somme divisé en 2 groupes pour en débattre. Cette formule nous permet de changer de groupe si le sujet finit par nous ennuyer :)
Bref, j’ai bien aimé cette rencontre qui revient sur l’esprit des premières. En plus, [Octo](http://www.octo.com/) nous a bien accueillis avec de succulents petits-fours :p


![ALT.Net](http://grozeille.files.wordpress.com/2009/05/altnet.gif) +   ![Petits-fours](http://grozeille.files.wordpress.com/2009/05/2124291918_fa4c5df217.jpg?w=150) =   ![Smiley](http://grozeille.files.wordpress.com/2009/05/spaceball.png?w=150)



<!-- more -->Pour revenir à la présentation de Sébastien : il a commencé par dire que nous faisions tous de l’Adaptive Object Modeling sans le savoir. Et en effet ! Je n’arrête pas d’en faire, sans en connaitre le nom. A la suite de cette présentation, je me rends mieux compte des similitudes de mes projets, des méthodes/patterns employés, et je peux prendre plus facilement du recule sur tout ça.

L’Adaptive Object Modeling c’est quoi : c’est le fait de modéliser une application qui est capable de s’adapter à un modèle métier.
Sébastien a cité 2 exemples : un gestionnaire de tâches (comme [Jira](http://www.atlassian.com/software/jira/)/[Trac](http://trac.edgewall.org/)/[Redmine](http://www.redmine.org/)) et une [GED](http://fr.wikipedia.org/wiki/Gestion_électronique_des_documents).


[![UML Adaptive Object Modeling](http://grozeille.files.wordpress.com/2009/05/adaptiveobjectmodeling011.png)](http://grozeille.files.wordpress.com/2009/05/adaptiveobjectmodeling011.png)



J’ai déjà travaillé sur ces 2 types de projets, mais pour ne pas plagier sa présentation, je vais prendre pour exemple une autre de mes expériences : un logiciel de vente (ok je triche, il a aussi cité cette exemple au tout début).
J’ai en effet travaillé sur une application pour vendre des cuisines, effectuer des devis, confirmer la vente par une facture, commander les meubles à l’aide de bon de commande, etc.
C’était chez un éditeur de logiciel, et le but était donc de faire un logiciel générique que l’ont peut vendre à divers clients.
Pour cela, il faut que l’application s’adapte au modèle métier de chaque client :



	
  * Certains vendent des meubles, d’autres de l’électroménager

	
  * Certains ont un workflow de validation des devis/factures complexe, d’autres non

	
  * Certains appliquent des règles de calcules de prix complexes (taxes, remises, formule de calcule de prix), d’autres vendent les produits à des prix fixes

	
  * Certains appellent un document « devis », d’autres une « quote » (français/canadiens)

	
  * Etc.


L’objectif est donc de modéliser un « méta-modèle » qui s’adapte à l’aide d’une configuration :

	
  * Un produit possède un type : il peut être un meuble, un frigo, etc.

	
  * Un type possède un ensemble d’attributs : un meuble possède une taille, un volume, une couleur, etc.


Bien sûr, un produit aura toujours un prix quel que soit son type. Ce dernier figurera toujours dans un devis, qui sera associé à un acheteur, etc. Il y a donc certaines choses « non générique » car communes à chaque client. Nous avons alors une logique « métier » commune : toutes applications de vente servent à calculer le prix d’un devis/facture.
Comme l’a dit Sébastien : le plus dur est de placer la barre entre le « tout spécifique » et le « tout générique ». C’est l’expérience et le contexte qui nous fera pencher la balance d’un coté plus que de l’autre.

![Balance](http://grozeille.files.wordpress.com/2009/05/272746539_1a85490513.jpg?w=300)

Il existe divers façons de configurer le modèle (XML, Base de données) mais le plus important est de savoir à qui s’adresse cette configuration. En effet, j’ai travaillé sur un projet qui a subit un échec car le client final était incapable de configurer un fichier XML….
Bien sûr, pour nous développeurs, cela nous semble évident avec des outils qui offrent la coloration syntaxique ou la complétion… mais pour le client, nous aurions du lui offrir une interface graphique agréable pour qu’il arrête de nous appeler tous les jours pour un changement de libellé…
Paramétrer des structures de données est aisé, mais paramétrer un comportement l’est moins. Il existe plusieurs solutions : ça peut se résumer à des « true/false » pour activer/désactiver des étapes d’un workflow, ou ça peut aller jusqu’à utiliser un [DSL](http://fr.wikipedia.org/wiki/Domain-specific_programming_language). Sébastien a parlé de modéliser un langage, et a pris comme exemple [WorkflowFundation](http://msdn.microsoft.com/fr-fr/netframework/aa663328.aspx).


[![UML Adaptive Behavior](http://grozeille.files.wordpress.com/2009/05/adaptiveobjectmodeling2.png)](http://grozeille.files.wordpress.com/2009/05/adaptiveobjectmodeling2.png)



Pour conclure, de nombreuses personnes se demandaient de l’intérêt de coder un « méta-model » générique, car la plus part, je pense, sont des consultants qui effectuent des projets spécifiques à leur client. L’intérêt de ce type de démarche est bien sûr de revendre le même logiciel à divers clients voir de vendre de la prestation pour configurer le logiciel (si la configuration devient complexe, comme c’est le cas pour les [ERP](http://en.wikipedia.org/wiki/Enterprise_resource_planning)). L’Adaptive Object Modeling s’adresse donc à des sociétés éditrices de logiciels qui visent un type de client.
Pour terminer, je voudrai revenir sur la difficulté énoncé par Sébastien concernant la balance Spécifique-Générique : j’ai vu certains projets se terminé par un échec car le chef de projet voulait faire « trop » générique en prévision des futurs clients… sauf que cela donne un logiciel qui ne répond même pas au besoin du premier client et qu’il est très difficile d’adapter aux besoins de ce dernier à cause de son aspect trop générique.
Je pense alors qu’il faut une approche « [bottom-up](http://en.wikipedia.org/wiki/Top-down_and_bottom-up_design) », c'est-à-dire de réaliser du spécifique pour le premier client, et rendre des parties génériques si le besoin des autres clients est similaire. On reste alors agile : [YAGNI](http://en.wikipedia.org/wiki/You_Ain't_Gonna_Need_It), on ne fait que ce qu’on a besoin. Ce n’est que lorsqu’on a un nouveau besoin (d’un autre client) qu’on procède à du refactoring pour rendre des morceaux du logiciel génériques. Par contre, cela demande de faire un effort sur la modularité (il est plus facile de refactorer un modèle de 10 classes, qu’un modèle d’1 classe constituée de 30000 lignes de codes…).

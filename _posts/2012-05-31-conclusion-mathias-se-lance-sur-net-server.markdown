---
author: grozeille
comments: true
date: 2012-05-31 20:05:06+00:00
layout: post
slug: conclusion-mathias-se-lance-sur-net-server
title: 'Conclusion: Mathias se lance sur .Net Server'
wordpress_id: 526
categories:
- Developpement
- DotNetServer
tags:
- .Net
---

Au cours des 12 derniers épisodes, je vous ai un peu raconté ma vie...
Mais je vous ai surtout fait partagé ce qui m'a sans doute le plus influencé dans le monde du développement .Net/Java.

Maintenant la boucle est bouclée: je me suis lancé sur le développement d'un serveur d'application .Net avec pour influence:



	
  * EasyPHP

	
  * Tomcat

	
  * Spring DM Server

	
  * OSGI

	
  * Spring.net

	
  * COM

	
  * Gigaspaces

	
  * Google Chrome

	
  * Eclipse RCP


Si je reviens au premier épisode d'[introduction : Mathias est heureux… mais pourquoi ?](http://grozeille.com/2010/06/27/introduction-mathias-est-heureux%e2%80%a6-mais-pourquoi/) je vous montre une pauvre screenshot d'une petite application Winform... mais qu'est-ce que ça cache?

[![](http://grozeille.files.wordpress.com/2010/11/yes.png?w=300)](http://grozeille.files.wordpress.com/2010/11/yes.png)

Et bien, cette application exploite mon "moteur à la OSGI" pour :



	
  * charger des plugins, soit dans un AppDomain, soit dans un processus

	
  * démarrer dynamiquement les instances de service IService qui font office de point d'entré du plugin

	
  * demander aux services de se dessiner dans la fenêtre principale


Cela donne quelque chose similaire à Google Chrome, puisque si vous "killer" un process correspondant à un plugin, cela n'affecte pas l'application.

Les plugins peuvent dépendre les uns des autres, ce qui veut dire que le moteur va démarrer les dépendances avant.
Les plugins peuvent communiquer entre eux, comme le fait l'application principale avec le point d'entré IService. Cette communication est faite en .Net remoting (pipe).

Mais ce moteur peut aussi  être utilisé en mode console pour agir comme un serveur d'application!
Vous pouvez alors:

	
  * lister les "Bundles" qui tourne

	
  * stopper/démarrer un Bundle, ce qui  va bien sûr démarrer les dépendances nécessaires

	
  * les bundles sont isolés dans des AppDomains ou Processus différents

	
  * installer un Bundle à partir d'un ZIP

	
  * installer un Bundle à partir d'un "repository" (comme dans Spring DM Server)

	
  * dans le cas de l'installation à partir d'un repository, le serveur va aussi télécharger et installer les dépendances, en tenant compte de la version bien sûr


[![](http://grozeille.files.wordpress.com/2010/11/kukulkanshell.png?w=300)](http://grozeille.files.wordpress.com/2010/11/kukulkanshell.png)

Vous en voulez plus?



	
  * Le Repository de Bundle n'est autre qu'une application de type Bundle

	
  * un Bundle peut être de type "Web", ce qui va démarrer une instance de XSP (serveur ASP.net de Mono)

	
  * le Bundle "BundleRepository.Web" fournit une interface Web à la gestion du Repository

	
  * le Bundle "WebManager" fournit une interface Web à la gestion des Bundles et du serveur d'application


[![](http://grozeille.files.wordpress.com/2010/11/bundlemanagerstartstop.png?w=300)](http://grozeille.files.wordpress.com/2010/11/bundlemanagerstartstop.png)

[![](http://grozeille.files.wordpress.com/2010/11/bundlemanagerinstall.png?w=300)](http://grozeille.files.wordpress.com/2010/11/bundlemanagerinstall.png)

[![](http://grozeille.files.wordpress.com/2010/11/bundlemanagerupdate.png?w=291)](http://grozeille.files.wordpress.com/2010/11/bundlemanagerupdate.png)

[![](http://grozeille.files.wordpress.com/2010/11/repositorywebui.png?w=300)](http://grozeille.files.wordpress.com/2010/11/repositorywebui.png)

Pas mal non?
Ce qui manque à tout cela:



	
  * Une meilleur gestion des dépendances, exprimée à l'aide d'un XML descripteur de service (comme le XML des plugin Eclipse) basé sur Spring.net

	
  * Une meilleur communication inter-processus que .Net Remoting, avec gestion d'un annuaire et d'un descripteur de service (comme un WSDL)

	
  * Des Bundles de type "Job schedulé", avec gestion de Workflow, tout cela avec une interface Web pour leur gestion

	
  * Le déploiement des Bundles sur plusieurs instances de serveurs (cluster) avec gestion de faillover

	
  * Un Bundle fournissant une couche de sécurité transverse

	
  * Un Bundle fournissant un accès à une source de donnée hébergé (SQLite)

	
  * Un Bundle fournissant un service de type cache (Memcache?)

	
  * Un Bundle fournissant un service de type Bus ([Laharsub](http://www.google.com/url?sa=D&q=http://www.infoq.com/news/2010/10/Laharsub&usg=AFQjCNEkeqsCu7d3RjBF-T63q0r1d696Og)?)

	
  * Un Bundle fournissant un service de "Perf. Counter"

	
  * Un Bundle fournissant un service de logging transverse

	
  * Une console d'administration à distance

	
  * Garantir la compatibilité avec Mono+Linux

	
  * Des gens motivés pour participer à ce projet OpenSource!

	
  * Héberger un "Plateform as a Service" sur le Could!!

	
  * Conquérir le Monde!!!


Alors, qu'en pensez-vous?

Le code source est sur BitBucket (il est aussi sur Github mais beaucoup plus vieux): [https://bitbucket.org/grozeille/nsynapse](https://bitbucket.org/grozeille/nsynapse)

(PS: je suis super mauvais en nom, j'aurai du l'appeler "carotte" ça passerait mieux)

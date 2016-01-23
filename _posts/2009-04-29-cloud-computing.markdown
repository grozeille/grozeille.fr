---
author: grozeille
comments: true
date: 2009-04-29 21:14:02+00:00
layout: post
slug: cloud-computing
title: Cloud computing
wordpress_id: 134
categories:
- Developpement
tags:
- aptana
- azure
- cloud
- eclipse
---

OK, je ne suis pas original, je parle d'un sujet "dans le vent" : le [Cloud Computing](http://en.wikipedia.org/wiki/Cloud_computing)...

**Cloud Computing: introduction avec Azure et Amazon
**

Grâce à la présentation chez [Fastconnect](http://www.fastconnect.fr/) par [Romain](http://codingly.com/), j'ai pu découvrir les joies de [Azure](http://www.microsoft.com/azure/default.mspx). C'est la solution Cloud de Microsoft qui est bien sûr très orientée .Net + VisualStudio.

On parle ici de "[Plateform as a Service](http://en.wikipedia.org/wiki/Platform_as_a_service)" puisque Azure nous offre de quoi héberger nos applications (web ou service) à l'aide d'une architecture "cloud".
On développe des applications qui effectuent des calcules distribués sur X machines, ou on héberge X sites web ASP.Net dont la charge est répartie entre eux.
En plus d'offrir une architecture "scalable", on a droit à certains services "bas niveau" comme le service de stockage de données binaires (full REST), une queue ou un stockage "à la [BigTable](http://en.wikipedia.org/wiki/BigTable)". On peut ensuite bénéficier de services plus "haut niveau" comme "[Live Search](http://en.wikipedia.org/wiki/Live_Search)" ou "[Live Calendar](http://en.wikipedia.org/wiki/Windows_Live_Calendar)".

Par comparaison, [Amazon avec EC2](http://aws.amazon.com/ec2/) propose un service "Cloud" orienté "Hardware as a Service" car on loue ici à des machines virtuelles, vierges ou avec des choses pré-installé (comme Linux Apache Msql PHP). La puissance de ces machines est aussi "scalable" à la demande, et on ne paie que ce que l'on utilise.
A la différence d'Azure, où la partie "Hardware" est complètement masquée (IIS7, WindowsServer2008, etc.). Azure offre une interface web d'administration pour surveiller l'utilisation du CPU ou de la mémoire, et on peut rapidement changer le nombre d'instances d'un site web à la demande.
Ceci dit, Amazon offre aussi des couches techniques comme le service de [stockage Amazon S3](http://aws.amazon.com/s3/).

Bref, le Cloud ce n'est pas qu'un hébergeur de site web ou une [Dedibox](http://www.dedibox.fr/), c'est surtout le fait de bénéficier des serveurs des gros mastodontes tel qu'Amazon ou Microsoft pour louer la puissance dont on a besoin, et profiter d'applications et de services pré-installés utilisables tout de suite. C'est aussi la possibilité d'utiliser des services techniques (Database, etc.) ou haut niveaux (Map, Calendar, etc.).

**Nouvelle solution de Cloud avec Aptana**

Azure offre de quoi développer un site ASP.Net Scalable rapidement, mais je vais faire le chieur en voulant développer une application Rails sous Eclipse!

C'est la que j'ai découvert [Aptana Cloud](http://www.aptana.com/cloud).
<!-- more -->
La solution d'Aptana est la suivante :



	
  * Comme Azure, Aptana masque la complexité et l'installation des machines virtuelles. On a donc du "Plateform as a Service". On a droit à une machine pré-installée avec Apache, MySQL, SFTP, SSH, SVN, etc.

	
  * Comme Azure, Aptana offre un IDE (Eclipse) avec un grand nombre de plugins pour développer, déployer et administrer le Cloud rapidement et facilement.

	
  * Comme Azure, Aptana offre une interface Web pour gérer sa machine, la puissance consommée et ce que ça nous coûte en fin de compte. Aptana fournit aussi la possibilité d'héberger un site en "staging mode", puis quand on est sûr de soi, on a la possibilité de le basculer en "public mode".
![Staging](http://grozeille.files.wordpress.com/2009/04/image-172.png)

	
  * Comme Amazon, la puissance et les prix sont scalables: on ne paye que ce dont on a besoin et on peut changer la puissance à la volé (le site indique $20 par mois, c'est parce qu'une machine de 256mo de RAM avec 5GB de disque coûte $0,027/heure)


![Pricing](http://grozeille.files.wordpress.com/2009/04/image-131.png?w=300)

Les points négatifs :



	
  * Pas d'architecture applicative "scalable": contrairement à Azure qui permet de changer en 3 clicks le nombre de processus ou le nombre d'instances d'un site. On dépend ici de la scalabilité de la machine virtuelle. Aptana est en partenariat avec [Joyent](http://www.joyent.com/) qui héberge ces machines.

	
  * Pas de services "haut niveau" comme ceux de Google (Google Maps, Google search, etc.) ou de Microsoft (Live Calendar, etc.). Mais rien ne nous empêche de les utiliser...

	
  * Services bas niveau limités: MySQL est OK, mais si l'on a besoin d'un stockage performant et distribué, on utilisera en plus les services d'Amazon (S3) ou Google (BigTable).


![Services](http://grozeille.files.wordpress.com/2009/04/image-16.png?w=300)

Voici pour moi les PLUS d'Aptana:



	
  * Plugins Eclipse de qualité avec un éditeur HTML/Javascript bien meilleur que celui par défaut (de [WTP](http://www.eclipse.org/webtools/))

	
  * Permet de faire des applications HTML classiques, PHP, Rails, Java, mais aussi Python, Adobe AIR, iPhone, Nokia WRT.

	
  * En quelques clicks dans le Wizard de création du projet, permet de choisir des frameworks Ajax parmi les plus connus ([jQuery](http://jquery.com/), [Dojo](http://www.dojotoolkit.org/), [ExtJS](http://extjs.com/), et j'en passe).

	
  * Fournit une documentation riche à l'aide de vidéos sur [Aptana TV](http://tv.aptana.com/).

	
  * Offre un nouveau type de développement full HTML+Javascript : [Jaxer](http://aptana.com/jaxer).


En résumé, Aptana offre mieux que de simples machines virtuelles :

	
  * un IDE puissant pour développer différents types d'applications

	
  * des machines virtuelles scalables pré-installées pour déployer dessus

	
  * une interface claire pour les administrer (statistiques, etc.)


Le Cloud donne des idées, et Aptana est une solution qui m'a l'air bien sérieuse. Je me suis laissé séduire grâce à l'offre d'essai gratuite, et je pense qu'à l'avenir j'utiliserai ce type de solutions si je veux développer et héberger un site Web.

![Eclipse](http://grozeille.files.wordpress.com/2009/04/image-12.png?w=300)

J'ai cité Jaxer dans les PLUS de la solution d'Aptana, mais j'en parlerai dans [mon prochain billet](http://grozeille.com/2009/04/29/jaxer/) ;)

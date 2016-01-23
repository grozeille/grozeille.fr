---
author: grozeille
comments: true
date: 2010-02-28 19:29:20+00:00
layout: post
excerpt_separator: <!--more-->
slug: dotnetserver
title: DotNetServer
wordpress_id: 280
categories:
- Developpement
- DotNetServer
tags:
- .Net
- DBus
- Gigaspaces
- J2EE
- linux
- mono
---

Comme je tarde à sortir mes posts sur les [Techdays](http://www.microsoft.com/france/mstechDays/) (et d'autres sujets, haha, surprise!), je vais en sortir un "tout petit".


## Pas de conteneur d'application en .Net... ou presque


En fait, c'est suite à une frustration absolue datant du premier jour ou j'ai découvert .Net (car je faisais du Java, avant, dans mon temps libre...).
Après avoir lourdement digéré [J2EE](http://en.wikipedia.org/wiki/J2EE), les [EJB](http://en.wikipedia.org/wiki/Ejb), [RMI/IIOP](http://en.wikipedia.org/wiki/Java_remote_method_invocation), j'ai été déçu de ne rien voir de tel en .Net.
Certains dirait que ce n'est pas une grosse perte ;) En effet, J2EE n'a rien de simple, mais c'est quand même parfois puissant.

Je trouve stressant qu'une application .Net "d'entreprise" doit forcement dépendre des services Windows, des tâches schédulées, ou d'IIS. Déployer une application Java sur Tomcat est d'une simplicité déconcertante, et Microsoft propose un équivalent seulement dans le future Windows Server 2008 R2 avec [Windows AppFabric](http://msdn.microsoft.com/en-us/windowsserver/ee695849.aspx).
Et encore, pour avoir vu la présentation aux Techdays, je suis plutôt déçu.

<!--more-->


## Gigaspaces? Un conteneur d'application malgré lui.


Ces derniers temps, de développe avec un DataGrid: [Gigaspaces](http://www.gigaspaces.com/). Ce dernier est en Java, mais possède une API .Net. Je bénéficie alors de son infrastructure pour déployer facilement mes applications .Net.
En effet, ce dernier fonctionne sur le principe de "container" tournant sur plusieurs machines, sur lesquels on peut déployer X instance d'une application, appelé "Processing Unit".
Comme Gigaspaces fournit une mémoire distribuée sur ces "containers" (c'est une peut l'objectif d'un DataGrid ;)), mes instances d'applications peuvent échanger des données via cette mémoire "partagée/distribuée".

Gigaspaces fournie une notion de "**Primary/Backup**" ce qui permet de rendre une instance active/inactive en cas de crash.
Il est même possible d'activer des "moniteurs" pour rendre une instance inactive s'il n'y a plus assez de ressource (CPU/Mémoire/etc.) sur une machine, et activer une autre instance sur une autre machine. La répartition de la charge est donc super bien gérée, et presque transparente puisqu'on déploie un "zip" de notre application, et le service "Manager" se charge de l'installer sur les "containers".

Mais voila, Gigaspaces c'est du lourd, du payant, et du Java.
Mon but est d'offrir quelque chose de similaire sans la performance de Gigaspaces ni sans la richesse de son API autour du cache.
Mon but est de pouvoir déployer une application Web, en uploadant un ZIP depuis une page d'administration, que cette dernière soit déployer sur X instances d'un coup, et qu'elles travaillent ensembles à l'aide d'un cache (Memcache et un très bon cache est suffisant pour mon besoin), d'une queue ou de service RPC.
Mon but est aussi de fournir un environnement d'exécution pure .Net, indépendant de l'OS, indépendant d'[IIS](http://en.wikipedia.org/wiki/Internet_Information_Services)/[MSMQ](http://en.wikipedia.org/wiki/MSMQ)/[DCOM](http://en.wikipedia.org/wiki/Distributed_Component_Object_Model)/etc, et donc compatible **Mono/Linux**.
C'est le "[**Write once, run anywhere**](http://en.wikipedia.org/wiki/Write_once,_run_anywhere)" de Java, mais en .Net.


## DotNetServer ou la quête du saint graal


J'ai donc commencé à voir comment héberger mes applications Web dans un container, à l'aide [d'XSP](http://www.mono-project.com/ASP.NET)...chose faite.
J'ai ensuite voulu calquer au modèle [OSGI](http://en.wikipedia.org/wiki/Osgi) pour le "conteneur d'application", avec séparation des applications par **AppDomain**, gestion de dépendance entre les applications, et cycle de vie de ces dernières.
Et enfin, j'ai cherché un moyen efficace de publier/souscrire à des services entre les applications.

J'ai passé ma journée à cherche un mécanisme de communication inter-AppDomain (ou inter-processus):




  * [PIPE/Mémoire partagée/Sémaphore](http://en.wikipedia.org/wiki/Inter-process_communication): ... je vais éviter de re-inventer la roue...


  * [.Net Remoting](http://en.wikipedia.org/wiki/.Net_Remoting): la solution officiel de Microsoft pour une communication Inter-AppDomain, même s'ils disent que .Net Remoting est obsolète pour laisser place à WCF


  * [WCF avec le NAMED-PIPE](http://en.wikipedia.org/wiki/Windows_Communication_Foundation): WCF n'existant pas sous Mono, je n'y pense même pas, surtout que c'est un peu une usine à gaz


  * [RMI/IIOP](http://iiop-net.sourceforge.net/): pourquoi pas, mais c'est une solution plutôt distribuée (basé sur .Net Remoting).


  * [COM/DCOM](http://en.wikipedia.org/wiki/Distributed_Component_Object_Model): Solution Microsoft pure, étant même préconiser par Microsoft à la place de remoting (car plus de sécurité, transaction distribué, etc.). Mais pure Microsoft/Windows = pas pour moi


  * [XPCOM](http://en.wikipedia.org/wiki/Xpcom): en gros, dans la famille Corba, je veux le fils, celui qui n'est pas chez Microsoft. C'est peut-être une solution à envisager, mais Corba est abandonné dans le monde Linux pour du DBus


  * [DBus](http://en.wikipedia.org/wiki/D-Bus): protocole inventé pour une communication inter-processus sous Linux, pour remplacer l'ORB de Gnome ou DCop de KDE. C'est clairement un équivalant à COM, sans être un "Corba'like", et c'est devenu standard sous Linux. De plus, [une implémentation pure .Net](http://www.ndesk.org/DBus) existe.


[![](http://grozeille.files.wordpress.com/2010/02/dbusexplorer1.png?w=300)](http://grozeille.files.wordpress.com/2010/02/dbusexplorer1.png)[![](http://grozeille.files.wordpress.com/2010/02/dbusexplorer2.png?w=300)](http://grozeille.files.wordpress.com/2010/02/dbusexplorer2.png)

Je me suis donc lancé sur DBus, tout comme J2EE à choisie RMI/IIOP... l'avenir me dira si j'ai fait le bon choix.

Bref, cela donne pas grand chose pour l'instant, mais voici le prototype:
[![](http://grozeille.files.wordpress.com/2010/02/dotnetserver.png)](http://grozeille.files.wordpress.com/2010/02/dotnetserver.png)

On voit ici que j'ai démarré un "bundle" qui est une instance d'XSP, le serveur ASP.net (qui dans cet exemple héberge 2 applications Webs **http://localhost:456/App1** et **htpp://localhost:456/App2**).
[![](http://grozeille.files.wordpress.com/2010/02/testxsp.png)](http://grozeille.files.wordpress.com/2010/02/testxsp.png)

J'ai aussi démarré le bundle "**MyAnotherBundle**", qui dépend de "**MyBundle**" qui dépend de "**DBusBundle**".
Ces derniers se chagent car ils ne l'étaient pas encore.




  * Le bundle **DBus** est simplement un démon DBus, qui offre un bus de message, un peut comme un broker dans Corba.


  * Le bundle **MyBundle** va alors publier des services auprès de DBus.


  * Le bundle **MyAnotherBundle** va alors consommer les services de MyBundle (il affiche le résultat de la fonction "sayHello" de MyBundle).


Comme je gère moi même les AppDomains, je configure leurs chemin de résolution de dépendance. Comme ça, chaque Bundle est installé dans un dossier, et n'a pas besoin de contenir TOUTES LES DLL qu'il a besoin, afin de ne pas les dupliquer entre les applications. Les DLL communes sont alors dans un dossier LIBS.

[![](http://grozeille.files.wordpress.com/2010/02/dotnetserverfolders.png)](http://grozeille.files.wordpress.com/2010/02/dotnetserverfolders.png)


## Conclusion


C'est loin d'être parfait et c'est un premier jet. Je ne sais pas si je vais avoir autant de motivation qu'aujourd'hui pour mener le projet à bien.
J'ai même découvert qu'un projet similaire existe: [http://www.dotnetpowered.com/appserver.aspx](http://www.dotnetpowered.com/appserver.aspx) mais il est mort depuis bien longtemps, et les sources sur le CSV ne sont plus disponible. Espérons qu'on n'en dise pas autant de mon projet dans plusieurs années ;)
Mon projet est ambitieux, mais si ça vous plait de jeter un oeil aux sources, voir même contribuer, n'hésitez pas à faire votre branche des sources GIT: http://github.com/grozeille/DotNetServer
Le README explique un peut plus mes intentions, ou les [schémas dans la doc](http://github.com/grozeille/DotNetServer/raw/master/Doc/DOTNETEE.pdf), il faudrait maintenant que je rende ça plus attirant dans le Wiki de github (ainsi qu'un nom plus cool, comme le nom d'un animal?)

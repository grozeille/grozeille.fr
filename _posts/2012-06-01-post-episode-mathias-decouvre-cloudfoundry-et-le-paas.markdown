---
author: grozeille
comments: true
date: 2012-06-01 12:42:58+00:00
layout: post
slug: post-episode-mathias-decouvre-cloudfoundry-et-le-paas
title: 'Post épisode: Mathias découvre Cloudfoundry et le PaaS'
wordpress_id: 564
categories:
- Developpement
- DotNetServer
tags:
- cloud
- cloudfoundry
- paas
---

Je vous ai donc parlé de mon projet NSynapse (qui commence à dater), et je voulais faire le rapprochement avec un PaaS: [CloudFoundry](http://www.cloudfoundry.com/).

Ce qui m'a donné envie d'en parler, c'est l'état d'avancement des solutions PaaS aujourd'hui, mais surtout la présentation de l'architecture interne de CloudFoundry: [Presentation:  Cloud Foundry: Design and Architecture](http://www.infoq.com/presentations/Cloud-Foundry-Design-and-Architecture)
Je vous conseil de la voir avant de lire ce qui suit.

Elle montre à quel point CloudFoundry n'est pas juste un outil de déploiement et de monitoring, mais c'est pour moi un serveur d'application nouvelle génération: multi-techno, avec gestion de scallabilité horizontale, etc.

[![](http://grozeille.files.wordpress.com/2012/05/capture-d_ecc81cran-2012-05-27-acc80-12-43-29.png)](http://grozeille.files.wordpress.com/2012/05/capture-d_ecc81cran-2012-05-27-acc80-12-43-29.png)

Ce serveur d'app, j'en ai rêvé pendant des années, et c'est aussi mon projet que je vais dévoiler dans l'épisode finale.


### 1. Conteneur d'application Web, mais pas que…


L'objectif de ce projet était de fournir un serveur d'application pour l'écosystème .Net, comme il en existe en Java (Tomcat/JBoss/Weblogic/etc.)
Cela explique l'[Episode 2: Mathias découvre J2EE](http://grozeille.com/2010/06/29/episode-2-mathias-decouvre-j2ee/)

Le but étant de faire quelque chose de cross-plateforme (compatible Mono) afin de ne pas dépendre de IIS et Windows.
Mais je voulais faire plus qu'un serveur Web IIS: je voulais que le serveur d'app contienne des applications de type Web mais aussi de type "Service Windows" ou "Daemon", ou encore de type "Tâche schedulée".
Cela explique l'[Episode 12: Mathias découvre Topshelf](http://grozeille.com/2012/05/27/episode-12-mathias-decouvre-topshelf)

On retrouve cette distinction dans de nombreux PaaS, comme Azure (Web Role et Worker Role).


### 2. Un mini PaaS


J'avais imaginé une solution qui soit un "bundle" à installer avec le serveur d'app, mais aussi plusieurs middlewares:




  * une base de donnée,


  * une [MOM](http://fr.wikipedia.org/wiki/Message-oriented_middleware),


  * un cache,


  * etc.


L'inspiration m'est venu de par la succès de [EasyPHP](http://www.easyphp.org/) qui offre tout ce qu'il faut pour faire une application sans avoir à installer quoi que ce soit d'autre.
Cela explique l'[Episode 1: Mathias découvre le PHP](http://grozeille.com/2010/06/27/episode-1-mathias-decouvre-php/)
Mais je voulais surtout démocratiser des middlewares comme les Queues ou les Caches en fournissant une implémentation par défaut.

Certains vont me dire que "[Windows AppFabric](http://msdn.microsoft.com/en-us/windowsserver/ee695849.aspx)" est la version "PaaS privé" de [Windows Azure](http://www.windowsazure.com/fr-fr/), et qu'il fournit déjà:




  * la possibilité de faire des applications Web (IIS)


  * la possibilité de faire des tâches schedulées ou des services windows


  * un MOM (MSMQ)


  * un cache distribué (anciennement [Velocity](http://msdn.microsoft.com/en-us/magazine/dd861287.aspx) maintenant [AppFabric Caching](http://msdn.microsoft.com/en-us/library/hh334305))


  * une base SQLServer


Mais tout ça est trop lié à l'OS Windows, et je voulais quelque chose qui s'installe aussi sur les plateformes Linux.


### 3. Packaging et déploiement multi-instances


Un autre objectif était de pouvoir déployer une application facilement, sur plusieurs serveurs de manière transparente.
Je voulais faire quelque chose qui se rapproche des déploiements de "[Processing Unit](http://www.gigaspaces.com/wiki/display/XAP9/Packaging+and+Deployment)" avec [Gigaspaces](http://www.gigaspaces.com/datagrid-product): on peut ainsi préciser le nombre d'instances, et le nombre de backup. Gigaspaces s'assure ensuite de déploiement ces instances sur les serveurs disponibles, et en cas de crash de l'un d'entre eux, Gigaspaces re-déploie l'instance qui a crashée sur un autre nœud du cluster.

Ce dernier peut être considéré comme un serveur d'App, car on peut y déployer:




  * des services, appelé Processing Unit, qui effectue des traitements dans le cache ou expose des services


  * [ des applications Web](http://www.gigaspaces.com/wiki/display/XAP9/Web+Processing+Unit+Container), des Processing Unit évoluées qui embarque un serveur d'App Jetty


Cela explique l'[Episode 5: Mathias découvre Gigaspaces](http://grozeille.com/2010/08/22/episode-5-mathias-dcouvre-gigaspaces/)

En parlant de Gigaspaces, ils ne m'ont pas attendu pour faire leur propre PaaS: [Cloudify](http://www.gigaspaces.com/cloudify) est un PaaS qui exploite les mêmes briques techniques de gestion de cluster (déploiement de multiples instances, monitoring, Self Healing) et le plus beau c'est que c'est gratuit et [OpenSource](https://github.com/CloudifySource/cloudify)!

Mais quand on dit "multi-instances", ça ne sert à rien s'il n'y a pas un load-balancer au dessus.
Je ne savais pas lequel prendre, et je ne suis pas arrivé à ce stade du développement, ma solution étant mono-serveur pour le moment.

Pour pouvoir déployer, il faut aussi packager. Mieux encore, je voulais gérer une notion de dépendance entre les packages, en m'inspirant d'[OSGI](http://fr.wikipedia.org/wiki/OSGi):




  * l'application A dépend de B en version 1.0


  * quand je déploie A, ça déploie d'abord B 1.0, le démarre, et passe au déploiement de A


Cela explique l'[Episode 3: Mathias découvre Eclipse (et un peu OSGI)
](http://grozeille.com/2010/06/29/episode-3-mathias-decouvre-eclipse/)Et l'[Episode 4 : Mathias découvre Spring (et un peu plus OSGI)](http://grozeille.com/2010/07/09/episode-4%C2%A0-mathias-decouvre-spring-et-un-peu-plus-osgi/)

Il m'a fallut alors inventer une API commune aux application (pour gérer le cycle de vie start/stop/restart) et un format de package (c'était avant qu'[OpenWrap](http://www.openwrap.org/) et [Nuget](http://docs.nuget.org/) existent).
J'avais étudié des solutions de "plugin", mais rien ne me satisfaisait.
En fait, ça se rapproche plus des notions de "Recipes/Cookbooks" qu'il y a dans les solutions comme [Puppet,](http://docs.puppetlabs.com/learning/manifests.html) [Chef](http://wiki.opscode.com/display/chef/Cookbooks) ou [Cloudify](http://www.cloudifysource.org/guide/developing/recipes_overview).


### 4. Binding de service transparent


Je ne voulais pas que cette notion de dépendance s'arrête aux applications .Net, je voulais l'étendre aux middlewares:




  * l'application A dépend de MySQL et de QPid


La notion de dépendance entre application .Net fonctionne, mais pas celle avec les middlewares.

Je voulais d'ailleurs m'abstraire de l'implémentation et avoir des dépendances de "services":


  * l'application A dépend d'un service SQL et Amqp: les implémentations seront fournies par MySQL et [QPid](http://qpid.apache.org/)


  * l'application A dépend du WebService "Pricing": l'implémentation sera fournie par l'application B


Cela explique l'[Episode 7: Mathias découvre Unity+WPF+MVVM](http://grozeille.com/2010/11/25/episode-7-mathias-decouvre-unitywpfmvvm-aux-techdays-2010/)
Et aussi l'[Episode 9: Mathias découvre MEF](http://grozeille.com/2012/05/27/episode-9-mathias-decouvre-mef/)

J'ai bloqué sur le sujet car je ne voyais pas comment marier la notion de dépendance vers des services avec la notion de dépendance d'application.
En fait, pour abstraire la notion de service, il me fallait faire une "[annuaire de services](http://fr.wikipedia.org/wiki/Architecture_orient%C3%A9e_services#L.27annuaire_de_services)" ou une découverte de service dynamique.
C'est pour cela que j'ai étudié [DBus Sharp](http://www.ndesk.org/DBusSharp) et le protocole [Zeroconf](http://en.wikipedia.org/wiki/Zero_configuration_networking) et aussi COM.
Cela explique "[DBus avec .Net](http://grozeille.com/2010/05/05/dbus-avec-net/)" et l'[Episode 8: Mathias découvre COM](http://grozeille.com/2011/04/19/episode-8-mathias-decouvre-com/)

Je voulais aussi abstraire la communication entre les service avec un "[Service Bus](http://fr.wikipedia.org/wiki/Enterprise_Service_Bus)" maison: l'objectif étant d'avoir une middleware entre les applications qui assure la communication, et ainsi les applications n'ont pas un lien "en dure" entre elles (ne connaissent pas l'IP de leurs dépendances).
[DCOM](http://fr.wikipedia.org/wiki/Distributed_Component_Object_Model) et [DBus](http://fr.wikipedia.org/wiki/Dbus) font exactement cela, mais je voulais quelque chose d'asynchrone avec une couche de "Messaging" comme "[NServiceBus](http://nservicebus.com/)" ou "[MassTransite](http://masstransit-project.com/)".
Je voulais faire un service bus maison car je voulais quelque chose de plus light que ce qui existe, je me suis alors lancé en utilisant [ZeroMQ](http://www.zeromq.org/) et le format [Protobuf](http://fr.wikipedia.org/wiki/Protocol_Buffers).
Vu l'ampleur du travail j'ai abandonné :)


### 5. En conclusion:


Si vous avez été suffisamment courageux pour lire tout ce qui précède, et que vous avez pris le temps de voir la présentation de l'architecture de CloudFoundry, vous allez voir qu'il y a de grosses similitudes:




  * Cloudfoundry possède un "conteneur d'application générique" qui peut être du Java, PHP etc. et pas seulement une application Web


  * Cloudfoundry fournie de base des services, comme MySQL, mais avec des services modernes, comme MongoDB et RabbitMQ


  * Cloudfoundry abstrait la notion de déploiement multi-site et d'instances, et vient avec un LoadBalancer  grâce à son Routeur


  * Cloudfoundry n'offre pas de dépendance entre applications, mais le fait entre les applications et les services, à l'aide du "bind de service"


  * Cloudfoundry utilise son propre format de packaging pour le déploiement (voir: [http://blog.cloudfoundry.com/2011/04/18/what-happens-when-you-vmc-push-an-application-to-cloud-foundry/](http://blog.cloudfoundry.com/2011/04/18/what-happens-when-you-vmc-push-an-application-to-cloud-foundry/) )


  * Cloudfoundry se repose sur une couche de messaging pour faire communiquer les différentes briques dans une environnement distribué


Je me dis alors que c'est la démarche à suivre, la bonne architecture.
Cloudfoundry ne fait pas encore tout ce que j'avais prévu, et plus aussi.
Est-ce que ça vaut toujours le coup de faire son propre "Cloudfoundry like", un PaaS simple et spécifique .Net ?
Étant donnée que Cloudfoundry peut aussi [contenir des applications .Net](http://www.ironfoundry.org/), est-ce qu'il ne vaut pas mieux parier dessus?

La question reste ouverte, mais ce projet m'aura appris pas mal de chose entre temps...

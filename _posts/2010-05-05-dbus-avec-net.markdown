---
author: grozeille
comments: true
date: 2010-05-05 06:17:46+00:00
layout: post
slug: dbus-avec-net
title: DBus avec .Net
wordpress_id: 362
categories:
- Blabla
- DotNetServer
tags:
- .Net
- DBus
- IPC
- mono
---

Pour ceux qui ne le savent pas, je travail sur un serveur d'application .Net indépendant de la plateforme Windows: [DotNetServer](http://grozeille.com/2010/02/28/dotnetserver/).

Après une version bonne pour une démo, j'ai voulu refactoriser le tout pour avoir quelque chose de viable.
Dans mon dernier billet, j'explique mon périple à la recherche d'un protocole de communication Inter-Processus, et j'ai choisi NDesk.DBus: l'implémentation full .Net de [D-Bus](http://en.wikipedia.org/wiki/D-Bus).

La solution était sexy:



	
  * Déclaration des services par interface, ne pouvant exposer QUE des types simples ou Struct. Cela force à réaliser qu'en matière de communication, une instance d'objet ne veut rien dire et qu'on communique que par DTO.

	
  * Support des méthodes, propriétés et événements

	
  * Channel par Socket/TCP ou par Pipe

	
  * Communication optimisé binaire (pas d'XML ou de SOAP....)

	
  * Exposition des services sur le Bus avec un contrat au format XML (comme un WSDL en quelque sorte)

	
  * Cross-platform: provient du monde Linux mais existe sous Windows

	
  * Un standard de communication Inter-Processus, de plus en plus utilisé sous Linux, remplaçant CORBA (avec Bonobo)


Mais voila, tout n'est pas rose, et DBus me donne du fil à retorde.
L'implémentation .Net n'est pas très propre:

	
  * API pas très utilisable car quasiment tout est Internal

	
  * Pas de doc?

	
  * Ça manque de convention, le source n'est pas très lisible, j'ai envie de passer un coup de Resharper dessus :)

	
  * Beaucoup, beaucoup de commentaire du genre "_//temporary hack_" ou "_//TODO_"... beaucoup de code commenté qui prouve que la personne a voulu faire bien mais n'a pas eu le temps

	
  * Quand j'exécute [DBusExplorer](http://www.ndesk.org/DBusExplorer) pour scanner mes services, cela plante 1 fois sur 2 mon client

	
  * Je n'arrive pas à faire marcher un service ou un client dans un Thread!!! Cela me bloque totalement


Je me demande si je ne vais pas revenir à une solution .Net Remoting:

	
  * implémentation .Net et Mono

	
  * channel IPC (par Pipe)

	
  * supporte les événements

	
  * DBus est vraiment orienté "Desktop" comme le D l'indique. J'en fait donc une utilisation détournée.


Mais une autre solution peut aussi faire l'affaire: [ProtoBuf](http://code.google.com/p/protobuf-net/wiki/Performance), un protocole performant inventé par Google.

Je vais tacher de vous tenir plus au courant, histoire aussi de recueillir des opinions concernant mes choix.

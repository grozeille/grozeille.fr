---
author: grozeille
comments: true
date: 2011-04-19 06:00:18+00:00
layout: post
slug: episode-8-mathias-decouvre-com
title: 'Episode 8: Mathias découvre COM'
wordpress_id: 514
categories:
- Developpement
- DotNetServer
tags:
- .Net
- com
- corba
- DBus
- WCF
---

Bonjour tout le monde, et merci de votre patience...
Ça fait presque 5 mois que je n'ai pas blogué, et que j'ai interrompu ma série "Mathias découvre..."
Comme j'en découvre tous les jours, j'ajouterai bien d'autres épisodes avant la conclusion finale, mais j'ai peur que ça dure une éternité :)
En réalité, je voulais "jouer la montre" avec ces blogs, afin de stabiliser mon projet et lui trouver un nom sympathique. Mais je n'ai pas vraiment trouvé le temps d'y travailler, alors je vais "pousser l’oisillon hors du nid", et j'ajusterai plus tard s'il ne vole pas très bien ;D

Je change de sujet par rapport aux précédents postes, et je m'attaque à un autre sujet épineux: la communication inter-processus.

Au début de ma vie professionnel, je n’ai pas commencé à travailler en .Net, mais en Delphi.

J’avoue que Delphi était séduisant. Avant .Net, c’était la manière la plus efficace de réaliser des applications Windows lourde avec un Designer d’interface unique. Et puis, n’oublions pas que l’inventeur du langage Delphi n’est autre que [Anders Hejlsberg](http://en.wikipedia.org/wiki/Anders_Hejlsberg), qui fut embauché par Microsoft pour inventer C# !

Quand .Net prenait de plus en plus d’ampleur,  j’ai alors réussi à convaincre tout le monde de s'y mettre.
Mais comme la migration devait se faire petit à petit, il fallait intégrer Delphi avec .Net.

Pour cela, j’ai découvert [COM](http://en.wikipedia.org/wiki/Component_Object_Model).
COM est une technologie 100% Microsoft, mais qui se base sur les mêmes principes que Corba.
COM permet de communiquer entre les applications, peu importe le langage. La communication se faisait en activant des services, à l’aide d’un contrat qui se rédigeait dans un langage indépendant du langage de compilation : IDL (Interface Definition Language).

[![](http://grozeille.files.wordpress.com/2010/11/0764549146fg08_16.jpg?w=300)](http://grozeille.files.wordpress.com/2010/11/0764549146fg08_16.jpg)

C’était magique : on pouvait inclure un UserControl .Net dans une application Delphi existante ! On pouvait aussi appeler des services .Net depuis Delphi, et vis vers ça !

Les services étaient d’ailleurs enregistrés auprès de Windows, dans la base de registre. Donc, quand un programme Delphi demande un service qui répond à une interface, Windows se charge de le localiser (DLL ou EXE) de l’héberger dans un conteneur (dans le cas de l’EXE, il lance ce dernier, dans le cas de la DLL, il l’host dans DLLHOST.exe) et d’instancier le service pour qu’il puisse être utilisé.

Et ce n’est pas tout ! Il y avait aussi DCOM qui est la version distribué de COM. Cela veut dire que si la DLL n’est pas sur la machine actuelle, Windows se charge d’interroger les autres serveurs DCOM pour qu’ils instancient le service à distance ! Tout cela avec une couche de sécurité ultra complexe !

De plus, le langage IDL supporte les méthodes, les propriétés, les événements, les paramètres de type « out », l’héritage d’interfaces, la gestion des versions, etc.…

Si vous souhaiter exposer des services sous Windows, cette technologie semble la plus appropriée.

Dans le monde des serveurs J2EE, ce fût Corba, concurrent direct à COM, qui remplissait ce rôle.

Mais voila : COM est 100% Windows, 100% Natif (non managé) ce qui rend le pont COM-.Net peu performant.

Concernant CORBA, il existe bien des connecteurs pour .Net, mais pas de serveur CORBA 100% managé.
De plus, CORBA est abandonné dans certains domaines à cause de sa lourdeur : les distributions Linux ont migré de CORBA à DBUS pour avoir aussi leur « équivalent à COM ». A noter que DBus existent en 100% .Net: [http://www.ndesk.org/DBusSharp](http://www.ndesk.org/DBusSharp)

Microsoft abandonne d’ailleurs COM pour sa technologie de communication phare : WCF.
Avant WCF, Microsoft avait introduit une autre solution 100% .Net: .Net Remoting. Mais ce dernier était trop simple et a fini par être abandonné, même si c'est toujours la technologie par défaut pour communiquer inter-AppDomain.

Alors, que choisir comme technologie de communication et d’activation de service ? Point à Point ou par un intermédiaire (Bus/Broker)? Quel format de message/marshalling doit-on utiliser?

Pour ma part: COM n'est pas multi-plateforme, je ne suis pas convaincu par l'usine à gaz WCF, DBusSharp est trop bugué, .Net remoting est trop simple/limité... je reste un sur ma fin.

Mais entre temps, j'ai découvert le "Messaging" et la communication asynchrone, qui est parfaite pour un environnement distribué. On ne peut pas remplacer le RPC par le Messaging dans tous les cas, mais il a falloir que j'exploite cette voie.

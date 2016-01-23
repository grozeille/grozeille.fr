---
author: grozeille
comments: true
date: 2009-05-31 15:05:25+00:00
layout: post
slug: alt-net-sur-laop
title: ALT.Net sur l'AOP
wordpress_id: 198
categories:
- ALT.Net
- Developpement
---

Je vous invite à venir à la session [ALT.Net sur l'AOP](http://www.altnetfr.org/2009/05/28/altnet-paris-14-aspect-oriented-programming-aop/) présenté par [Romain Verdier](http://codingly.com/) le Mercredi 17 juin.

Pour vous mettre dans le bain et vous permettre de vous informer sur le sujet avant la réunion, voici un exemple d'AOP super simple avec Postsharp : [http://bit.ly/71pej](http://bit.ly/71pej)

Dans le cadre de mon projet actuel, [l’AOP](http://fr.wikipedia.org/wiki/Programmation_orientée_aspect) aurait pu m’aider à décorer les méthodes qui nécessitent de l'impersonation (accès à des ressources critiques qui nécessite donc un compte privilégié) ou à gérer la sécurité+log+erreurs au niveau des WebServices (CheckClientCertificate+Log+SoapException).

J'utilise souvent l'AOP avec [Spring.net](http://www.springframework.net/doc/reference/html/aop-quickstart.html), qui utilise la méthode "création de proxy dynamiquement" ou appelé aussi "dynamic weaving".

Cette méthode consiste à créer des proxy dynamiquement qui encapsulent l'objet cible en ajoutant le code des aspects aux bons endroits. La limite de l'approche avec Spring.Net est que l'on perd en performance à la création de ces proxy, on ne peut exposer qu'une seule interface, et cela oblige à utiliser Spring.net pour se faire injecter l'instance.

Postsharp lui, fait tout à la compilation, c'est ce que l'on appelle le "static weaving". L'avantage est que l'on gagne en performance, on ne dépend pas de la façon d'instancier la classe, et la manière d'ajouter des aspects se fait par code (par attributs) se qui peut s'avérer plus agréable que de les déclarer dans un XML (ce que fait Spring.net). L'inconvénient est que cela oblige à posséder le code source de l'objet à "aspectiser" et de le compiler avec les aspects.
On peut citer [AspectDNG](http://aspectdng.tigris.org/nonav/doc/index.html) qui utilise aussi le "static weaving".

[Aspect#](http://www.castleproject.org/aspectsharp/index.html) utilise le "dynamic weaving" tout comme Spring.net. Ils utilisent tous la réflexion à l'aide de [System.Reflection.Emit](http://msdn.microsoft.com/en-us/library/system.reflection.emit.aspx) (fourni par défaut avec .Net) pour créer les proxy dynamiquement. Aspect# le fait par l'intermédiaire de [Castle.DynamicProxy](index.html) (utilisé aussi par [NHibernate](http://nhforge.org/Default.aspx) ou [RhinoMock](http://ayende.com/projects/rhino-mocks.aspx)).

Le débat à la session ALT.Net va certainement porter sur Réflexion vs Introspection: la réflexion est moins bonne en performance que l'introspection, car elle nécessite de charger tout le code en mémoire, alors que l'introspection analyse directement l'IL. Voici un petit post sur le débat: [http://bit.ly/2xq6aB](http://bit.ly/2xq6aB)

Romain a travaillé sur [Mono.Cecil.Decompiler](http://codingly.com/tag/cecildecompiler/) avec [Jean-Baptiste Evain](http://evain.net/blog/), il va donc sans doute nous parler des avantages de l'introspection avec [Mono.Cecil](http://www.mono-project.com/Cecil). Voici un [autre post](http://evain.net/blog/articles/2009/04/30/reflection-based-cil-reader) sur le sujet sur le blog de JB.

Voila, j'espère que vous serez ainsi mieux armés pour assister à la session :)

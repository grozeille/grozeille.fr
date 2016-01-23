---
author: grozeille
comments: true
date: 2008-04-30 23:20:52+00:00
layout: post
slug: timeout-wcf-au-bout-dun-certain-nombre-dappels
title: Timeout WCF au bout d'un certain nombre d'appels
wordpress_id: 50
categories:
- Developpement
tags:
- .Net
- Asp.net
- Spring.net
- tips
- WCF
---

Rien de plus stressant que de passer une journée entière sur un bug. Surtout si on n'a aucune idée du problème (pas d'exceptions, ni d'erreurs dans les logs) et que les recherches sur Internet sont infructueuses.
**Contexte** : une application Web Asp.Net communique avec un service WCF.
**Problème** : au bout d’un certain nombre d’appels (invariant) l’application Web n’arrive plus à joindre le serveur (Timeout).

<!-- more -->Pour conserver une trace de mon incompétence, voici donc la **solution**:
Pour qu'on puisse dialoguer avec un service WCF dans une page Asp.net, je leur injecte un proxy à l’aide de Spring (voir [Spring.net pour le web](http://www.springframework.net/doc-latest/reference/html/web.html#web-di)). Pour cela, j’utilise une "factory de proxy" à l’aide de l’interface [IFactoryObject](http://www.springframework.net/doc-latest/reference/html/objects.html#d0e4032).
Crédule que j’étais, j’imaginais que le fait de retourner `true` pour la propriété `IsSingleton` allait faire en sorte que Spring.net ne fasse appel qu’une seule fois à la méthode `GetObject()`.
Et bien non ! C'est à vous d’être cohérent: même si `IsSingleton` retourne `true`,  rien ne vous empêche de toujours retourner une instance différente dans la méthode `GetObject()`.

Pour en revenir à mon problème, vous l’aurez compris : ma méthode `GetObject()` retournait à chaque fois un nouveau proxy vers le service WCF.
**Résulat** : à chaque fois que Spring avait besoin d’injecter mon proxy à une page (postback par exemple), je créai une nouvelle connexion au serveur WCF. J'ai fini par atteindre le nombre de connexion max, et le serveur ne répondait plus.

Il est tout de même dommage que les [traces WCF](http://msdn.microsoft.com/en-us/library/ms732023.aspx) ne m'ont pas révélé d'exception expliquant cette limite max de connexion :(

Pour approfondir le sujet sur les `IFactoryObject` :
Un objet qui implémente `IFactoryObject` doit toujours être un singleton, si ce n’est pas le cas on obtient une exception:
[code language='xml']

[/code]
`
=> IFactoryObject must be defined as a singleton - IFactoryObjects themselves are not allowed to be prototypes.
`

La propriété `IsSingleton` de la factory indique seulement ce qu’elle est censée faire... mais sans aucune obligation/vérification du comportement. Dans mon cas, je retournais `true` mais rien ne m'a empêché de créer une nouvelle instance à chaque appel...

Dans le cas particulier d'une application Asp.net, on peut avoir des "presque singleton" en changeant le `scope`:
[code language='xml']

[/code]




  * scope="application" : c'est un singleton de toute l'application web. Firefox et Safari m'affiche toujours 1.


  * scope="session" : c'est un singleton pour chaque session cliente. Firefox et Safari m'affiche toujours 2 (1 instance pour Firefox +  1 instance pour Safari).


  * scope="request" : c'est un singleton dans le cadre de la requête. Firefox et Safari vois le compteur s'incrémenter à chaque rafraichissement de la page.


Pour [plus d'infos sur les scopes](http://www.springframework.net/doc-latest/reference/html/objects.html#d0e2577).

**Conclusion(s)** :




  1. Ce n'est pas la propriété `IsSingleton` qui détermine si Spring va faire appelle une ou plusieurs fois à votre Factory. C'est à elle de fournir le comportement adéquat.


  2. Un singleton n'en est pas toujours un... ça dépend du contexte. Dans tous les cas, pour éviter les erreurs comme la mienne, n'oublier pas d'utiliser la `destroyMethod` pour libérer les ressources. (l'interface `ILifeCycle` de Java [n'existe pas encore](http://jira.springframework.org/browse/SPRNET-753) dans Spring.net  mais la [1.2 sort en RC1 début mai](http://www.springframework.net/roadmap.html)...).


  3. Un "Timeout" peut vouloir dire "trop de connexion au serveur" :)


  4. Cette fameuse Factory de proxy WCF sera fournie dans Spring.net 1.2. j'aurais perdu moins de temps en [prenant les sources des nightbuilds](http://forum.springframework.net/showthread.php?t=2936)... vive l'OpenSource!

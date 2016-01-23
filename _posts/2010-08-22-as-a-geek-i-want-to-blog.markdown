---
author: grozeille
comments: true
date: 2010-08-22 15:42:18+00:00
layout: post
slug: as-a-geek-i-want-to-blog
title: As a Geek I want to blog
wordpress_id: 443
categories:
- Developpement
tags:
- .Net
- BDD
- Deleporter
- Mocks
- NUnit
- RhinoMocks
- Selenium
- SpecFlow
---

S’il y a bien quelque chose qui me fait stresser, c’est de livrer un logiciel sans être sûr qu’il fonctionne.

Livrer une version sans la tester, c’est un peu comme jouer à la roulette russe.
C’est pourquoi depuis longtemps je pratique les tests unitaires avec NUnit.

Mes tests étant de plus en plus complexe, j’ai appris aussi à utiliser RhinoMocks afin de simuler les dépendances de l’objet du test.

J’ai toujours fournis des efforts dans les tests: alors POURQUOI je stress toujours autant avant de livrer une version?

Simple: car malgré les tests et une bonne couverture, je livre toujours des bugs.
Le fait est que, les tests unitaires valident chaque briques de manière indépendante, mais pas toute l’application dans son ensemble.
De plus, faisant beaucoup d’application Web, je me dois de tester l’interface HTML + Javascript, ce que je ne fais pas pour l’instant.

J’ai bien eu des tentatives avec Selenium, mais sans trop de résultat.
J’ai bien envisagé [JSUnit](http://www.jsunit.net/), mais je n’y suis pas encore là.

Mais même si je test tout de manière indépendant, le plus gros des problèmes survient lors de l’intégration de toutes ces briques, avec par exemple des bugs dans les fichiers de configuration Spring.net.

Si Selenium me permet de tester cette intégration, j’ai tout de même un gros problème: je ne peux pas prédire les données de mon test, ce qui fait que parfois il passe, et parfois il ne passe pas.

J’ai aussi rencontré un autre problème avec les tests unitaire: la rédaction de ces derniers.
Quand je souhaite tester 2 scénarios différents, mais similaire à 90%, je me retrouve avec beaucoup de copier/coller.

Je factorise alors, mais mon test devient rapidement difficile à lire, alors que pourtant il peut servir de documentation du fonctionnement du code.

Après quelques recherches, et la lecture de [l’excellent blog de Steve Sanderson](http://blog.stevensanderson.com/category/bdd/), je me suis mis au [BDD](http://en.wikipedia.org/wiki/Behavior_Driven_Development)!

Le principe est de décrire un besoin utilisateur dans sa langue native: non, pas le C#… l’anglais!
Cela donne quelque chose comme:

`Feature: Test SpecFlow with Selenium and RhinoMocks
        In order to test Specflow
        As a geek
        I want to write stories with Specflow
        And test the application with Selenium
        And mock the backend with RhinoMocks`

Le truc, c’est que cela va me servir de Spec, ce qui va donc orienter la conception de mon application.

C’est déjà l’objectif du [TDD](http://en.wikipedia.org/wiki/Test-driven_development): concevoir une architecture à partir des tests, cela nous permet de réaliser QUE CE QUE L’ON A BESOIN: c’est le principe du [KISS](http://en.wikipedia.org/wiki/KISS_principle) ou [YAGNI](http://en.wikipedia.org/wiki/YAGNI).

Mais ces tests peuvent être difficile à concevoir, mais le BDD nous aide à décrire nos tests!
Si quelqu’un débarque sur le projet, et lit un test de 100 lignes de code, il va peut-être pas comprendre du premier coup. Mais s’il lit la version “Anglaise”, à moins qu’il ne sache pas lire, il va alors comprendre le test.

Cette magie se fait à l’aide de [SpecFlow](http://specflow.org/), qui est la version 100% .Net du très à la mode [Cucumber](http://cukes.info/) (ou [Cuke4Nuke](http://github.com/richardlawrence/Cuke4Nuke)).

Au programme: rédaction des tests “en Anglais”, intégration dans VisualStudio, et génération d’un test unitaire découpé en étapes (une étape par phrase).
Cela rend alors les tests unitaires vraiment TRES TRES lisibles.

Reprenons mon cas, ou je souhaite tester une application Web dans son ensemble.
Afin de tester l’interface Web, je vais implémenter les étapes de mon BDD à l’aide de [Selenium](http://seleniumhq.org/docs/05_selenium_rc.html#learning-the-api).

[![](http://grozeille.files.wordpress.com/2010/08/testspecflow1.png?w=300)](http://grozeille.files.wordpress.com/2010/08/testspecflow1.png)

OK, j’ai maintenant un test compréhensible par un utilisateur… J’ai un test NUnit C# correctement découpé et donc plus lisible par les développeurs. Je pars du test pour définir mon UI, qui elle même va orienter le design de mon Controller et ainsi de suite… Je simule les clicks de souris afin de naviguer dans le site, et je détecte les erreurs “d’intégration”…
Mais j’ai toujours un même problème: je ne maitrise pas les données de ma base afin de vérifier le fonctionnement de mon test.

Dans ce cas, il me faut simuler ma couche d’accès aux données à l’aide de mocks RhinoMocks.
Mais si mon test unitaire s’exécute sur un poste client, et que le site Web est hébergé sur un serveur dans un processus différent, comment puis-je faire mes mocks?

Grâce à Steve Sanderson, nous avons la solution, et elle s’appelle [DELEPORTER](http://blog.stevensanderson.com/2010/03/09/deleporter-cross-process-code-injection-for-aspnet/).

Le principe est plutôt simple: un module HTTP agit comme un serveur .Net Remoting.
Le client sérialise un Delegate (anonyme ou pas, ou lamdba) afin de l’envoyer sur le serveur et de l’exécuter dans son processus.

C’est clairement une grosse faille de sécurité, alors pensez à bien ségréguer les configurations de tests et celles de production!

Etant donné que j’utilise Spring.net pour l’injection de dépendance, je peux injecter de Mocks à l’aide d’une petite factory RhinoMock.
Mon test va ensuite définir le comportement de ces derniers pour mon cas de test.

Au final, cela donne:

[code language="csharp"]
// J'utilise Deleporter pour exécuter ce code coté Serveur
Deleporter.Run(() =>
{
        // je demande à Spring.net d'obtenir le MockRepository de RhinoMock
	var mocks = ContextRegistry.GetContext().GetObject("MockRepository") as MockRepository;

        // je demande à Spring.net d'obtenir le mock déjà créé et injecté
	var repository = ContextRegistry.GetContext().GetObject("MyRepository") as IMyRepository;

        // j'informe RhinoMock que je souhaite recoder le comportement de mon mock
	mocks.BackToRecord(repository);

        // Quand "GetMessage" sera appelé, je souhaite retourner "Welcome Mathias"
	Expect.Call(repository.GetMessage())
                .Repeat.Any()
                .Return(string.Format("Welcome {0}!", userName));

        // j'informe à RhinoMock que j'ai terminé de spécifier le comportement du mock
	mocks.Replay(repository);
});
[/code]

Il ne reste plus qu’à exécuter le test Selenium, vérifier les données de l'UI, et la boucle est bouclée!

Les sources de cet exemple sont disponibles sur mon BitBucket: [https://bitbucket.org/grozeille/testspecflow.mvc](https://bitbucket.org/grozeille/testspecflow.mvc)

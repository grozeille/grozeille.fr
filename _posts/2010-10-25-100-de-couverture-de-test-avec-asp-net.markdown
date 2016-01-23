---
author: grozeille
comments: true
date: 2010-10-25 21:48:02+00:00
layout: post
slug: 100-de-couverture-de-test-avec-asp-net
title: 100% de couverture de test avec ASP.Net
wordpress_id: 470
categories:
- Developpement
tags:
- .Net
- Asp.net
- coverage
- NUnit
- Selenium
- SpecFlow
---

Dans ma quête de la couverture de test absolue, j'ai décider de tester mon application ASP.Net avec des tests fonctionnels.
Pour cela, j'utilise le combo: [Specflow](http://specflow.org/)+[Selenium](http://seleniumhq.org/projects/remote-control/).

En terme de rédaction du test, cela donne ça:

[code]
﻿Feature: Test with ASP.net
	In order to get test coverage of my ASP.Net Application
	As a developper
	I want to run an embeded ASP.Net server in my NUnit test

@selenium
Scenario: Say Hello to Michel
	Given I'm on the default page
	When I enter the name "Michel"
	And I click the "SayHello" button
	Then the message is "Hello Michel"
[/code]

Grâce à Specflow, je peux donc rédiger mon scénario en anglais, très lisible par l'utilisateur qui va pouvoir ainsi exprimer son besoin.
Ces phrases sont ensuite couplées à des méthodes C# qui effectuent une partie du test. Exemple:

[code language="csharp"]
[When("I click the \"SayHello\" button")]
public void IClickTheSayHelloButton()
{
    selenium.Click("SayHelloButton");
    selenium.WaitForPageToLoad((1 * 60 * 1000).ToString());
}
[/code]

On remarque ici que j'utilise Selenium pour simuler le scénario et effectuer un click sur un bouton de la page.

Petite astuce: le scénario est "tagué" @selenium. Grâce à ce tag, je peux indiquer qu'il faut initialiser Selenium à chaque début de scénario tagué ainsi.

[code language="csharp"]
[BeforeScenario("selenium")]
public void BeforeScenario()
{
    var firefoxPath = Path.GetFullPath(
        Path.Combine(AppDomain.CurrentDomain.BaseDirectory, @"..\..\..\Libs\Firefox\firefox.exe"));
    var selenium = new DefaultSelenium("localhost",
                                       4444,
                                       @"*firefox " + firefoxPath,
                                       "http://localhost:8123");
    ScenarioContext.Current["selenium"] = selenium;
    selenium.Start();
}
[/code]

OK, je suis content avec ça, je peux maintenant rédiger des tests fonctionnels lisibles et les automatiser à l'aide de Selenium.
Mais cela ne me donne pas la couverture du code de mon application .Net qui se trouve hébergée sur un serveur IIS :(

Afin d'avoir la couverture du code de toute l'application, j'ai alors décider d'exécuter l'application ASP.Net à l'intérieur du processus du test unitaire!
Afin d'héberger l'application ASP.net, j'utilise pour cela la librairie de Mono: [XSP](http://www.mono-project.com/ASP.NET).
Pour cela, quelques lignes de codes suffisent:

[code language="csharp"]
[BeforeTestRun]
public static void BeforeTestRun()
{
    const int port = 8123;
    string path = Path.GetFullPath(@"..\..\..\MyApp.Web");
    const string webServerFileName = "Mono.WebServer2.dll";

    string sourcePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, webServerFileName);
    string destinationPath = Path.Combine(Path.Combine(path, "bin"), webServerFileName);

    File.Copy(sourcePath, destinationPath, true);

    var websource = new XSPWebSource(IPAddress.Any, port);
    webAppServer = new ApplicationServer(websource);
    webAppServer.AddApplication("localhost", port, "/", path);
    webAppServer.Start(true);
}

[AfterTestRun]
public static void AfterTestRun()
{
    webAppServer.Stop();
}
[/code]

Simple non?

Voila alors le résultat:
[![](http://grozeille.files.wordpress.com/2010/10/coverageaspnet.png)](http://grozeille.files.wordpress.com/2010/10/coverageaspnet.png)

Afin de pouvoir tester par vous même, vous pouvez télécharger les sources depuis [http://bitbucket.org/grozeille/testwithaspdotnet/src/](http://bitbucket.org/grozeille/testwithaspdotnet/src/), lancer le serveur Selenium à l'aide de **"SeleniumServer.bat**", lancer les tests avec "**Test.bat**", et voir le rapport de couverture de code avec** Libs\PartCover .NET 2\PartCover.Browser.exe** en ouvrant le fichier **Coverage.Xml**.
Ça, ça rox du poney!
[![](http://grozeille.files.wordpress.com/2010/10/affiche-mon-petit-poney-le-film-my-little-pony-the-movie-1986-1.jpg?w=233)](http://grozeille.files.wordpress.com/2010/10/affiche-mon-petit-poney-le-film-my-little-pony-the-movie-1986-1.jpg)

---
author: grozeille
comments: true
date: 2008-05-02 22:15:09+00:00
layout: post
excerpt_separator: <!--more-->
slug: a-la-conquete-du-web-30
title: A la conquête du Web 3.0
wordpress_id: 51
categories:
- Developpement
tags:
- .Net
- Flash
- Flex
- java
- JavaFX
- mono
- web
---

J'ai eu une discutions intéressante ce midi au sujet du buzz en ce moment: [Adobe open-source Flash](http://www.adobe.com/openscreenproject/)! Je vois ça comme un premier pas vers la conquête du Web 3.0. Une guerre déjà entamé entre Adobe, Microsoft et le monde libre.

<!--more-->

Haha, je sais que le terme _[Web 2.0](http://fr.wikipedia.org/wiki/Web_2.0)_ fait couler beaucoup d'encre (ou abîme les claviers) mais moi je le prend du point de vue du développeur:

Au début, il y avait le néant... puis l'informaticien inventa la page HTML! Dans sa foulé il inventa le Javascript... puis les applets Java... pas de chance, l'informaticien était en avance sur son temps...

Puis le Web s'est vu enrichir de nouveau média (Youtube, Deezer, etc.) Toute cette magie est possible grâce aux génies de [Macromédia](http://fr.wikipedia.org/wiki/Macromedia) inventeurs du Flash! (racheté par la suite par Adobe)
Le web est devenu plus beau, plus fun... et plus lourd tout de même.
Flash est aujourd'hui la techno incontesté pour les médias riches. Elle était aussi en avance sur son temps: les sites entièrement Flash était encore trop lourd pour les débits de l'époque. Ce n'est aujourd'hui plus un problème, mais si tous les sites ne sont pas en Flash, je l'explique pour plusieurs raisons:
Premièrement, cette technologie était boudé par le monde Linux qui se retrouvé avec un produit propriétaire, des versions en retard par rapport à celles sur Windows, et même souvent bugguées.
Les adeptes des standards W3C ne voient pas non plus Flash d'un très bon œil et préfère se concentrer sur la norme HTML+[ECMASCRIPT](http://fr.wikipedia.org/wiki/ECMAScript) (autrement dit: Javascript).

C'est la que le Web 2.0 atteint son paroxysme: les sites Web d'aujourd'hui exploitent à fond le Javascript ([Ajax](http://fr.wikipedia.org/wiki/Asynchronous_JavaScript_and_XML), [GWT](http://code.google.com/webtoolkit/), [Scriptaculous](http://script.aculo.us/), etc.). Cela donne des pages Web plus riches, plus interactives, plus animées, et plus légères!
Car oui, le bon vieux HTML avec un peu de Javascript c'est plus léger que du Flash. Certains dénonceront simplement les mauvais codeurs ActionScript qui sont souvent des graphistes reconvertis et qui font des choses non-optimisés...
Ceci dit, cette performance n'est possible que grâce aux [effort fournis par les navigateurs Web](http://www.apple.com/safari/) qui supportent [de mieux en mieux](http://www.korben.info/un-coup-de-boost-pour-firefox-3.html) le Javascript.
Mais voila, les vidéos ou encore d'autres choses ne sont pas possibles en HTML+Javascript aujourd'hui, et c'est pourquoi que Flash est encore très utilisé (surtout concernant la vidéo).

C'est la que Microsoft riposte avec [Silverlight](http://silverlight.net/) et ça va faire mal.
Imaginez: un plugin similaire à Flash, mais plus performant ([WPF](http://fr.wikipedia.org/wiki/Windows_Presentation_Foundation) utilisant gracieusement DirectX) avec des langages plus faciles à coder (C#, XAML, etc.) et des outils de développement/design très soignés (la série des [Expression](http://www.microsoft.com/expression/products/overview.aspx?key=blend)).

Mais la communauté pro-libre/pro-standard n'en reste pas la: [HTML5](http://en.wikipedia.org/wiki/HTML_5) est censé combler les lacunes vis-à-vis de Flash ou Silverlight.

Sun veut aussi être de la partie, après l'échec des applets, il tente nous proposer [JavaFX](https://openjfx.dev.java.net/downloads.html).
Les principales raisons de l'échec des applets sont:
- Java c'est gros et lourd à télécharger... imaginez un JRE de 30mo à l'époque des 56k!
- Ce <del>n'est</del> n'était pas non plus très performant, surtout en matière d'affichage.
- Il n'existe aucun outil pour graphiste pour faire des applets! C'est la que Macromédia avec Flash avait marqué un point.
- Ce <del>n'est</del> n'était pas libre... donc difficile à faire adopter par la communauté des développeurs.

Mais Sun propose des solutions:




  * [Java Kernel](http://weblogs.java.net/blog/enicholas/archive/2006/09/java_browser_ed.html): le principe est simple, il faut que le téléchargement d'une JRE soit négligeable (tout comme Flash). Pour ce faire, l'utilisateur télécharge une version "minimale" de la JRE, qui téléchargera des paquets supplémentaires seulement s'il y en a besoin.


  * Java2D/Swing [plus performant](http://java.sun.com/developer/technicalArticles/J2SE/Desktop/javase6/#Java_2D), ainsi que l'accélération avec DirectX (elle existait depuis peux de temps, mais désactivé par défaut car trop buggué). Cela permet aussi des effets comme la transparence etc.


  * [JavaFX](http://www.cnettv.com/9742-1_53-27434.html): ou comment créer un langage de description d'interface, pour créer plus simplement des animations etc.


  * Java est [open-source](http://openjdk.java.net/): à quand Java installé par défaut sous Linux? (Même si c'est maintenant un [paquet officiel d'Ubuntu](http://openjdk.java.net/install/#ubuntu))



Le seul hick qui va faire très très mal: toujours pas d'outil puissant pour les graphistes.
On peut aussi se demander pourquoi avoir inventer un n-ième langage de script, là où tout le monde optent pour le XML comme descripteur d'interface.

On remarque que "Open-source" est maintenant synonyme de "standard", et ça Adobe l'a compris. Fort se sa popularité, l'ouverture forcement va booster son engouement.
Microsoft n'est pas en reste dans ce domaine: depuis son alliance avec [Novell](http://www.novell.com/home/index.html), ils travaillent tous deux pour promouvoir [.Net sous Linux](http://www.mono-project.com/Main_Page) même si l'équivalent à Silverlight en libre, [Moonlight](http://www.mono-project.com/Moonlight), est encore loin de [voir le jour](http://www.youtube.com/watch?v=qRSO7p0HAIw&feature=related)...
On pouvait pointer du doigt le manque de _sérieux_ en matière de développement avec ActionScript, mais avec [Flex](http://www.adobe.com/products/flex/media/flexapp/) ce n'est plus vrai.

Avec toutes ces technos, on se demande si le navigateur ne servira plus qu'a charger un plugin Flash/Java/Silverlight, et déléguera le travail de rendu à ceux la. [Mozilla sonne l'alarme](http://osnews.com/story/19699/Mozilla-Warns-of-Flash-Silverlight-Agenda) et explique l'importance de HTML5.

Les paries sont lancés:
Les prochains sites-web, en Flash? HTML5+Javascript? Silverlight/Moonlight? JavaFX?

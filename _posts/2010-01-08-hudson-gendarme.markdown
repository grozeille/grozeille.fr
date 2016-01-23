---
author: grozeille
comments: true
date: 2010-01-08 00:21:09+00:00
layout: post
slug: hudson-gendarme
title: Hudson + Gendarme!
wordpress_id: 226
categories:
- Developpement
tags:
- .Net
- hudson
- mono
---

Petit billet pour vous annoncer fièrement la sortie de la version 0.7.5 du plugin "Violation" pour Hudson: [http://wiki.hudson-ci.org/display/HUDSON/Violations](http://wiki.hudson-ci.org/display/HUDSON/Violations)

J'y ai notamment contribué pour ajouter le support de [Gendarme](http://www.mono-project.com/Gendarme), l'outil d'analyse de code de Mono (équivalent à FXCop/StyleCop).
J'aurais aimé y contribué plus que cela (si j'avais eu le temps...) pour par exemple corriger les bugs sous IE ou les bugs sur les rapports FXCop/StyleCop avec des chemins relatifs.
Ces corrections de bugs me serrait très utiles dans le cadre de mon projet chez mon Client, puisque nous avons fait le choix d'utiliser Hudson comme plateforme d'intégration continue "multi-techno" (Java/C#/C++/Php).

Même si les développeurs Java exploite Hudson avec [Sonar](http://sonar.codehaus.org/) pour avoir un beau Dashboard sur des métriques de codes sources, nous exploitons les plugins d'Hudson pour les métriques .Net. En effet, le plugin Violation nous permet d'avoir des graph et des seuils d'alerte sur les rapports FXCop & Style. Nous combinons ça au plugin de [rapport de tests NUnit](http://wiki.hudson-ci.org/display/HUDSON/NUnit+Plugin), le plugin de [rapport de tests Selenium](http://wiki.hudson-ci.org/display/HUDSON/Seleniumhq+Plugin), ainsi que le [plugin Warning](http://wiki.hudson-ci.org/display/HUDSON/Warnings+Plugin) pour analyser les Warnings/Error à la compilation, et le plugin [Task Scanner](http://wiki.hudson-ci.org/display/HUDSON/Task+Scanner+Plugin) pour ne pas oublier de TODO dans le code ;) En plus de cela, on génère un rapport NCoverExplorer (HTML) accessible directement depuis Hudson.

Et vous? Comment faites-vous vos métriques dans l'intégration continue? Est-ce que vous connaissiez Gendarme et est-ce que vous l'avez déjà utilisé?

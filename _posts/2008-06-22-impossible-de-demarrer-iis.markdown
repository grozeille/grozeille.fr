---
author: grozeille
comments: true
date: 2008-06-22 14:22:13+00:00
layout: post
excerpt_separator: <!--more-->
slug: impossible-de-demarrer-iis
title: Impossible de démarrer IIS
wordpress_id: 65
categories:
- Developpement
tags:
- iss
- tips
- web
---

Il y a des astuces que j'estime devoir propager sur Internet, car ça peut éviter quelques arrachages de cheveux.

Symptôme: quand on souhaite démarrer IIS (6), ce dernier plante avec l'erreur "**Une erreur 0x8ffe2740 inattendue s'est produite**".

[![](http://grozeille.files.wordpress.com/2008/06/cannotstartiis2.jpg)](http://grozeille.files.wordpress.com/2008/06/cannotstartiis2.jpg)

<!--more-->

Le nom de l'erreur n'est pas très clair, et je me suis dit que le numéro hexa serait différent pour chaque PC. Mais j'ai finis par chercher ce numéro sur Google et je suis tombé sur l'explication: [http://support.microsoft.com/kb/816944/fr](http://support.microsoft.com/kb/816944/fr)

Pour résumer, le port utiliser par IIS (80 par défaut) est déjà utilisé.
Le port 80?? Mais qu'est-ce qui peut bien utiliser le port 80 sur mon PC fraichement installé???!!

Le site de Microsoft conseille d'utiliser 2 outils pour trouver le fautif: TCPView qui est une application "graphique", et FPort qui est en ligne de commande. Bien sûr, je choisi la version "graphique", sympa d'ailleurs mais qui ne trouve pas le fautif!!
Heureuse FPort, quand à lui, a bien trouver l'application qui utilise le port 80:

[![](http://grozeille.files.wordpress.com/2008/06/skypeport801.jpg)](http://grozeille.files.wordpress.com/2008/06/skypeport801.jpg)

Et oui, le fautif c'est Skype! Très étonnant... info trouvé sur [http://forum.skype.com/index.php?showtopic=42531](http://forum.skype.com/index.php?showtopic=42531)

Donc voila ce qu'il faut décocher pour corriger le problème:

[![](http://grozeille.files.wordpress.com/2008/06/skypeport80config2.jpg)](http://grozeille.files.wordpress.com/2008/06/skypeport80config2.jpg)

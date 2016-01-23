---
author: grozeille
comments: true
date: 2006-05-29 18:12:16+00:00
layout: post
slug: java-gnome
title: Java-Gnome
wordpress_id: 10
categories:
- Developpement
tags:
- gnome
- java
- linux
---

Comme vous le savez, l'environnement [Gnome](http://www.gnomefr.org/) sous linux utilise les composants graphiques de [GTK](http://www.gtk.org/), qui est a la fois portable mais qui de plus possede de nombreux "binding" dans de nombreux langages. Java n'est pas en reste, et en plus de GTK, [Gnome-Java](http://java-gnome.sourceforge.net) propose les "bindings" vers Glade, GConf, Cairo, etc...

Bref, tout pour faire une application qui s'integre bien dans Gnome, le tout realise dans l'elegant langage qu'est le Java , et  tout en pouvant benefficier du tres puissant IDE [Eclipse](http://java-gnome.sourceforge.net/cgi-bin/bin/view/Main/EclipseDevelopment). Et puis le fin du fin, c'est de generer un executable natif sous linux a l'aide [d'un script ANT](http://java-gnome.sourceforge.net/cgi-bin/bin/view/Main/AntNativeCompiles) qui compile avec GCJ (de toutes façon, vous avez deja vu Gnome sous Windows???).

Alors, apres une petite soire de dev, j'ai realise un petit carnet d'adresse en Java compile en natif :

[![Carnet d'adresse](http://grozeille.files.wordpress.com/2006/05/CarnetAdresse.thumbnail.png)](http://grozeille.files.wordpress.com/2006/05/CarnetAdresse.png)

Vous pouvez telecharger les sources [ici](http://kluba.mathias.free.fr/prog/CarnetAdresse-src.tar.gz) et les binaires [ici](http://kluba.mathias.free.fr/prog/CarnetAdresse-bin.tar.gz). 

Bien evidement, la question se pose pas mal dans la communaute : les futures applications Gnome... en C++, Java ou [Mono](http://www.mono-project.com/Mono_for_Gnome_Applications) ?

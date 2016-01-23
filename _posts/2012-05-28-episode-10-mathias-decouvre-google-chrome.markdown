---
author: grozeille
comments: true
date: 2012-05-28 10:14:19+00:00
layout: post
slug: episode-10-mathias-decouvre-google-chrome
title: 'Episode 10: Mathias découvre Google Chrome'
wordpress_id: 520
categories:
- Developpement
- DotNetServer
tags:
- google chrome
---

Il faillait que je vous parle de Google Chrome, car il m’a aussi beaucoup influencé !

Un navigateur est une application lourde composée de plusieurs vues et de plugins (ou extensions).
On peut même dire que les vues sont décrites en "une sorte d'XML" appelé HTML (non non, ce n'est pas du XAML).

Pour isoler chaque page et chaque plugin, Google a fait le choix de les séparer en différent processus.

[![](http://grozeille.files.wordpress.com/2010/11/chrome.png?w=300)](http://grozeille.files.wordpress.com/2010/11/chrome.png)

Et moi, j’ai trouvé ça** très très** malin !
Google avance la raison suivante : la gestion des ressources (mémoire, CPU) est le rôle de l’OS. Pourquoi réinventer cette gestion de ressource entre les plugins d’une même application ?

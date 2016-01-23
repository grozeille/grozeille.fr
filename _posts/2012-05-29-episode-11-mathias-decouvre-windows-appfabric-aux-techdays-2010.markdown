---
author: grozeille
comments: true
date: 2012-05-29 05:52:35+00:00
layout: post
slug: episode-11-mathias-decouvre-windows-appfabric-aux-techdays-2010
title: 'Episode 11: Mathias découvre Windows AppFabric aux Techdays 2010'
wordpress_id: 523
categories:
- Developpement
- DotNetServer
tags:
- Windows AppFabric
---

# Bon, assez parlé d’application RCP, parlons de serveurs d’applications.


Si Java a fait du chemin dans le domaine, .Net se résume à : RIEN !
Mais Microsoft tente de rectifier le tir en 2010 : [Windows AppFabric](http://msdn.microsoft.com/en-us/windowsserver/ee695849.aspx), le premier serveur d’application .Net.

[![](http://grozeille.files.wordpress.com/2010/11/p1000085_7679d50d.jpg?w=300)](http://grozeille.files.wordpress.com/2010/11/p1000085_7679d50d.jpg)

Mais j’ai été très déçu du résultat : Windows AppFabric n’est qu’un nom commercial pour désigner un serveur Windows 2008 avec tout ce qu’il y a d’installé dessus :



	
  * Serveur Web IIS

	
  * MMC de gestion du serveur, avec une nouvelle interface pour IIS permettant de déployer une application sur plusieurs serveurs (ENFIN !)

	
  * MSMQ pour le messaging

	
  * SQL Serveur pour la base de données

	
  * Velocity en tant que cache distribué


Mais voila, tout ces outils n’ont rien à voir les uns avec les autres, à par le fait qu’ils s’installent uniquement sur Windows.

On est très loin du serveur d’application J2EE qui héberge tout ces services et qui s’installent en quelques cliques avec gestion de dépendances.
On est très loin de Gigaspaces en terme de cache distribué.
On est très loin de l’interface Web pour gérer tout cela : si le serveur est obligatoirement un Windows, la MMC vous oblige aussi d’avoir comme poste client un Windows !

On est aussi très loin de la simplicité d’installation de EasyPHP.

Bref, je suis super déçu, mais pas surpris.

C’est pourquoi j’ai décidé de me lancer, et de développer mon propre serveur d’application .Net, CrossPlatform (Mono/Linux compatible), en prenant pour exemple ce qui existe dans le monde Java...

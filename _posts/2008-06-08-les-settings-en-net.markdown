---
author: grozeille
comments: true
date: 2008-06-08 17:33:32+00:00
layout: post
excerpt_separator: <!--more-->
slug: les-settings-en-net
title: Les Settings en .Net
wordpress_id: 60
categories:
- Developpement
tags:
- .Net
- settings
- Spring.net
- xml
---

La plateforme .Net fournit un mécanisme pour gérer les paramétrages. Il en existe 2 types : ceux de l'application et ceux de l'utilisateur. Au début de l'existance, il y avait la bonne vielle méthode du fichier `*.ini`, mais aujourd'hui le XML et devenu LE standard pour écrire des données dans un fichier "lisible" et structuré.

Il existe un autre standard : les applications .Net possède un fichier "mon_application.exe.config" qui n'est autre qu'un XML contenant le paramétrage de l'appliation. Ce fichier est structuré en 2 grosses parties: l'entête avec la section "configSections" qui décrit les sections du XML et les "parser" qui vont lire ces dernières. Puis il y a les sections proprement dites.

<!--more-->

Quand on veut utiliser des settings de l'application de type "clef=valeur", on peut les renseigner dans la section "applicationSettings". On peut ainsi facilement créer un paramétrage de l'application mais aussi pour chaque utilisateur à l'aide de la section "userSettings".
Voici un exemple de paramétrage:

```xml
<userSettings>
    <MonApp.Settings>
        <setting name="PreferredLanguage" serializeAs="String">
            <value>fr-FR</value>
        </setting>
    </MonApp.Settings>
</userSettings>
<applicationSettings>
    <MonApp.Settings>
        <setting name="TimeShowMsg" serializeAs="String">
            <value>5</value>
        </setting>
        <setting name="NotepadPath" serializeAs="String">
            <value>c:\windows\notepad.exe</value>
        </setting>
    </MonApp.Settings>
</applicationSettings>
```

VisualStudio propose une technique simple pour manipuler ces paramétrage. Il permet de créer un fichier `.settings` qui va tout simplement générer une classe pour accéder à tout ça, et qui va aussi permettre de sauvegarder les settings de l'utilisateur courant (dans un .config séparé dans `C:\Documents and Settings\UserName\Local Settings\AppName\`).

```C#
// on récupère la valeur d'une clef très simplement
String value = Settings.Default.MyKey;
// si elle a comme scope "user", on peut la modifier et la sauvegarder
Settings.Default.MyKey= value;
Settings.Default.Save();
```

Pour ma part, j'utilise massivement Spring.net et ses XML. Mes objets possèdent souvent des attributs qui ressemble à des paramètres (j'externalise au maximum). De plus, Spring.net propose de référencer d'autre XML, ce qui me permet de découper mon paramétrage en plusieurs fichiers pour différent domaine (Logging, Base de données, etc).

```XML
<!-- dans le App.config -->
<objects xmlns="http://www.springframework.net">
  <import resource="logging.xml"/>
  <import resource="database.xml"/>;
  <import resource="general.xml"/>
</objects>
```

```XML
<!-- dans general.xml -->
<objects xmlns="http://www.springframework.net">
  <object id="Setting" type="MonApp.Setting, MonApp">
    <property name="Timeout" value="100"/>
  </object>
</objects>
```

Mais il est vrai qu'un XML de Spring n'est pas facile à lire, car il ressemble à un code C# avec une suite de construction de classes. Il peut devenir vite complexe s'il y a beaucoup de classes de relations entre eux, ou si on utilise des concepts avancés de Spring.net (ObjectFactory par exemple).

Une des solutions les plus élégante pour un public informaticien, est de créer ses propres balises XML Spring.net, comme celles déjà existantes (Exemple: [paramétrage de base de données](http://www.springframework.net/doc-latest/reference/html/dbprovider.html#d0e11738).) On masque ainsi la complexité de la construction du programme en laissant une grande souplesse. Mais cette solution demande un certain effort dans la réalisation du parser XML.

```XML
<objects xmlns='http://www.springframework.net'
             xmlns:custom="http://www.grozeillle.com/custom">
  <custom:Setting timeout="100">
    <custom:EmbededSetting name="Default">
      <!-- autres settings -->
    </custom:EmbededSetting/>
  </custom:Setting>
</objects>
```

Mais ces fichiers de paramétrages restent difficiles à lire pour une personne non-informaticienne, qui n'a pas besoin de savoir comment le programme est construit. Dans ce cas, on externalise des valeurs dans des fichiers ".properties" très lisible puisque c'est une simple fichier texte avec une liste de couples "clef=valeur". On peut aussi externaliser ces couples dans une XML mais on perd l'intérêt d'avoir quelque chose de très facile à lire.

```XML
<objects xmlns='http://www.springframework.net'>
<!-- Cet objet contient une liste de "fournisseur" de paramétres-->
  <object type="Spring.Objects.Factory.Config.VariablePlaceholderConfigurer, Spring.Core">
    <property name="VariableSources">
      <list>
        <!-- Nous n'avons ici qu'un seul fournisseur,
            qui va chercher les paramétrages dans un fichier .properties -->
        <object type="Spring.Objects.Factory.Config.PropertyFileVariableSource, Spring.Core">
          <!- la liste de nos fichiers .properties -->
          <property name="Locations">
            <list>
              <value>config.properties</value>
            </list>
          </property>
        </object>
      </list>
    </property>
  </object>
</objects>
```

On peut ainsi utiliser des variables comme ceci:

```XML
<objects xmlns='http://www.springframework.net'>
    <!-- mon object de type "MyTutoClass" a besoin du chemin de Notepad.exe -->
    <object type="MyApp.MyTutoClass, MyApp">
        <property name="NotepadPath" value="${notepad.path}">
    </object>
</objects>
```

Mon fichier .properties ressemble simplement à ça:

```INI
;ceci est un commentaire
notepad.path=c:\windows\notepad.exe
```

Spring.net propose plusieurs méthodes de recherche de ces clef+valeur. On peut avoir comme source des fichiers ".properties", mais aussi la section "settings" dans l'App.config (comme vu plus haut), la base de Registre, etc. Voici la liste dans la [documentation officiel](http://www.springframework.net/doc-latest/reference/html/objects.html#objects-variablesource). Si elle ne vous suffit pas, vous pouvez toujours créer votre "provider" vous même.


Enfin, pour les plus "hardcore" d'entre-vous (ceux qui aime recoder l'univers), vous pouvez aussi créer votre propre XML avec votre propre format. Il est vrai qu'on souhaite parfois faire sa propre classe "Setting" car on veut hiérarchiser les différents paramètres. Admettons que l'on veuille vraiment avoir son propre format de fichier XML, ceci reste très simple en .Net:

```C#
// créer un "serializer" de Setting
XmlSerializer serializer = new XmlSerializer(typeof(Setting));
// création d'un flux sur mon fichier XML
TextWriter writer = new StreamWriter("Settings.xml");
// création de ma classe de Setting
Setting setting = new Setting();
// setting.Timeout = 5; etc, etc..
// enfin, sauvegarde de mon objet sous format XML dans le flux de mon fichier "Settings.xml"
serializer.Serialize(writer, setting);
```

On ne peut pas faire plus simple, non? Et vous savez quoi? Par défaut, ça marche sans rien faire d'autre. Mais si vous voulez customizer le format du XML, il suffira de décorer notre classe Setting à l'aide de quelques attributs `[XmlAttribute]`. Si vous voulez générer un schéma XSD de ce format XML, c'est à l'aide de `c:\Program Files\Microsoft SDKs\Windows\v6.0A\bin\xsd.exe`.

---
author: grozeille
comments: true
date: 2008-11-29 13:24:50+00:00
layout: post
slug: quel-langage-pour-lavenir-c4-ou-oxygene-delphi
title: 'Quel langage pour l''avenir : C#4 ou Oxygene (Delphi)'
wordpress_id: 106
categories:
- Blabla
- Developpement
tags:
- .Net
- c++
- delphi
- oxygene
---

Suite au post de Romain sur [l'avenir du langage C#](http://codingly.com/2008/11/15/le-futur-de-c/), je voulais non seulement répondre, mais en profiter pour parler brièvement d'un autre langage .Net : Oxygene.


### C#4 ?


Romain a trouvé une citation un peu abusive mais qui m'est pourtant tout de suite venu à l'esprit concernant C#4 :


<blockquote>The dynamic keyword is going be abused so much… C# is on its way to becoming PHP.</blockquote>


Pour la petite histoire, je viens de passer 2 jours à coder du Javascript... coder?? Débuguer surtout!
Je ne sais pas si suis allergique aux langages dynamiques, mais ça me frustre au plus au point de ne pas savoir quel sont les membres que possède un objet, et de devoir le vérifier au _Runtime_...
J'ai passé 2h car j'ai fait une faute de frappe sur le nom d'un membre, ce qui ne plante pas, mais comme cela créer dynamiquement un nouveau membre avec ce nouveau nom, j'ai passé beaucoup de temps à comprendre pourquoi sa valeur était "null".

C'est pour ça que les aspects "dynamiques" me font peur pour la maintenance des futures programmes C#4.
Ceci dit, le mot clé "var" existe déjà en C#3, et je n'ai pas vu quelqu'un en abuser (_d'ailleurs, est-ce que la nouvelle version de Resharper suggère toujours de remplacer les types par des var ??!!_).
Toujours pour diluer mes propos, il est vrai que dans la réalité on a besoin d'utiliser différents langages pour différents besoin, alors pourquoi ne pas tout réunir en un seul...
Mais j'aimerai éviter ça :

[![Pétage de cable](http://grozeille.files.wordpress.com/2008/11/photo-4.jpg?w=260)](http://grozeille.files.wordpress.com/2008/11/photo-4.jpg)

Parfois je me dit aussi que "_C# is on its way to becoming C++_". Je n'ai pas beaucoup d'expérience en C++, et de ce fait j'ai parfois du mal à comprendre certains codes.
Mais j'ai surtout l'impression que les possibilités du langage sont tellement nombreuses, qu'on a pas 2 codes source C++ "dans la même prose", ce qui devient vite difficile à lire. Pouvoir faire 1 chose de 10 manières différentes, n'est en mon sens pas un bon truc.

Mais en pratique, les nouvelles fonctionnalités de C# ne sont utilisées que par une "élite" qui a un besoin très précis. Dans mon travail actuel, les gens ne savent pas encore faire du Linq, et j'ai l'impression que je suis le seul a avoir VRAIMENT migrer sur C#3. Donc, avant que quelqu'un découvre les nouveautés de C#4 et en abuse....

Ah, si, il y en a 1... et c'est le genre de personne à faire une chose d'une certaine façon "juste parce que c'est possible", si vous voyez ce que  je veux dire... et là, ça devient vraiment dangereux, et on fini par avoir du code incompréhensible car il a détourné une fonctionnalité de son but initial.

Je dois être vieux jeux, mais je préfère parfois la méthode "classique et lisible" même si elle est plus verbeuse. Pourtant, je me laisse séduire, et je deviens vite fan des méthodes d'extension et des expressions lambda. C'est comme si mes 2 personnalités entraient en conflit quand je me dit :

    
    [code language='csharp']
    return toto??tata;
    // ou
    return toto!=null?toto:tata;
    // ou
    if(toto != null)
    return toto;
    else
    return tata;
    [/code]


Il est clair que je préfère la première solution, mais on m'a défait fait la remarque :


<blockquote>euh, tu peux l'écrire avec le "if", je trouve ça plus lisible.</blockquote>


Et oui, il faut aussi s'adapter au niveau de lecture de l'équipe.

Mais là, je ne parle que du langage C#, pas des possibilité de la VM ou du Framework. S'il est possible d'interagir entre .Net et Javascript, alors je suis aux anges, mais il existe sans doute d'autres moyens "peut être plus contraignant" que d'ajouter de la dynamicité dans le langage C#. (On génère bien des "stub" pour communiquer en COM !)

Mais au finale, je me laisse prendre au jeux, et finalement je suis fan des expressions lamdba, Linq, les méthodes d'extensions, juste parce que ça s'écrit plus rapidement et que je suis fainéant.


### Oxygene ?


Parce que je suis bavard, je voulais en profiter pour parler non pas de C#, mais de [Oxygene](http://en.wikipedia.org/wiki/Chrome_programming_language).

[![delphiprismscreenshot](http://grozeille.files.wordpress.com/2008/11/delphiprismscreenshot.png?w=300)](http://grozeille.files.wordpress.com/2008/11/delphiprismscreenshot.png)

Un peu d'histoire : le créateur de [Delphi](http://fr.wikipedia.org/wiki/Delphi_(langage)) a aussi été le créateur de C# : [Anders Hejlsberg
](http://en.wikipedia.org/wiki/Anders_Hejlsberg)Petit lien car ça ne fait pas de mal : Anders qui parle du [future de C#](http://channel9.msdn.com/pdc2008/TL16/) (je sais, tout le monde l'a déjà vu).[
](http://en.wikipedia.org/wiki/Anders_Hejlsberg)

J'ai commencer à coder en Delphi au Lycée _(je ne compte pas les années Basic sous AsmstradCPC6128 ;))_.
Delphi était magique à l'époque : langage [Pascal Objet](http://en.wikipedia.org/wiki/Object_Pascal), IDE avec un puissant Designer pour application Windows, framework riche...

Puis le monde a évolué : Anders Hejlsberg a quitté Borland pour aller chez Microsoft.
A l'époque, Microsoft a voulu faire leur propre "Java" :[ J++](http://en.wikipedia.org/wiki/Visual_J%2B%2B).
Anders a commencer par travailler la dessus, mais Microsoft est entré en conflit avec Sun concernant ce J++, et c'est comme ça que .Net naquis.
Anders inventa alors C# pour l'occasion, et J++ fut porté sous .Net sous le nom de J#.

Les années noirs pour Borland ont commencé, les entreprises se tournant vers Microsoft et .Net.
Mais je suis resté à coder en Delphi 7 dans mon ancienne société, alors que .Net en était déjà à sa V2. Période de ma vie (en tant que codeur) très frustrante: pas de "foreach", pas de "generics", programmation par interface difficile, etc.

Pour Borland, ce fut de pire en pire : ils ont fini par migrer Delphi en .Net, et ont alors inclue le SDK de Microsoft .Net dans leur IDE... comme si Delphi en tant que langage était mort, et que "Delphi 2008" ne servait surtout qu'à développer en C#. Sans compter les frameworks tel que VCL.Net en conflit avec ceux de .Net comme Winforms.

Je n'ai pas travaillé avec Delphi 2008, mais je l'ai un peu testé. Malgré de gros problème de performance, cet IDE était déjà 1000 fois mieux que VisualStudio : refactoring poussé, historique "à la svn" à chaque sauvegarde/innactivité d'un source, Designer plus sympa, etc.

Mais finalement, Borland a laissé son IDE à Codegear et la mort de Delphi semblait proche. C'est pour cela que mon ancienne société a choisi de passer de Delphi7 à VisualStudio/C#.

Puis, récemment en surfant, j'ai découvert Oxygene.

Et je me suis dit : "haha, la résurrection de Delphi?"
Ce langage est dérivé de Delphi (comme une nouvelle version en quelque sorte), possède toutes (?) les fonctionnalités du langage C#3 comme Linq, etc.
Mais il ajoute aussi son lot de nouveauté que j'adore :



	
  * éviter les tests de nullité inutile :



    
    [code language='csharp']
    if(truc.parent != null && truc.parent.parent != null)
    toto = truc.parent.parent;
    // devient
    toto = truc:parent:parent;
    [/code]





	
  * ne pas choisir entre un "for" et un "foreach" car on a besoin d'un compteur


Combien de fois ais-je du ajouter un compteur dans un foreach (et risqué d'oublier le ++) et au final me résigner à utiliser le bon vieux "for". En Oxygene, le foreach peut gérer l'index :

    
    [code language='csharp']
    for each u in Users index i do begin
    // et on se sert de i
    [/code]


Maintenant, Oxygene fait du buzz sur le net... enfin surtout "[Delphi Prism](http://www.remobjects.com/oxygene.aspx)".

Finalement, l'IDE de Codegear est abandonné, et Delphi Prism s'intègre à VisualStudio (utilisé comme une application Eclipse RCP).
On retrouve le langage Oxygene, mais aussi un certains nombre de framework pour pouvoir faire des applications multi-plateform à l'aide de Mono.
Et pour faire plaisir aux ex-Delphi-istes, le package inclue une [API d'interoperabilité](http://www.remobjects.com/hydra.aspx) entre .Net et les applications pure Delphi Win32.
Pour plus d'infos : [http://www.delphi.org/2008/10/delphi-prism/](http://www.delphi.org/2008/10/delphi-prism/)

Il ne me reste plus qu'à tester tout ça :) Est-ce que ça veut dire que je vais abandonné C# pour revenir flirter avec Delphi?

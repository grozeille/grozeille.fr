---
author: grozeille
comments: true
date: 2010-01-25 21:36:49+00:00
layout: post
excerpt_separator: <!--more-->
slug: alt-net-et-loriente-objet
title: ALT.Net et l'orienté objet
wordpress_id: 261
categories:
- ALT.Net
- Developpement
tags:
- .Net
- ALT.Net
- java
- langage
- POO
---

La dernière réunion ALT.Net a été présentée par [Frédéric Fadel](http://fr.linkedin.com/in/fredericfadel) sur le sujet: [L’orienté objet : erreur historique ou la voie à poursuivre ?](http://www.altnetfr.org/2010/01/07/alt-net-paris-21-loriente-objet-erreur-historique-ou-la-voie-a-poursuivre/)

Je remercie Freddy pour sa présentation et Octo pour leur accueil.

En résumé, nous avons évoqué les problèmes avec les langages objets, et ce qui nous fait perdre en productivité.
Pour cela, il faut définir exactement ce qu'est l'Objet: d’après Freddy : **Héritage**, **Composition**, **Polymorphisme**.

[![](http://grozeille.files.wordpress.com/2010/01/p1030608-1.jpg?w=300)](http://grozeille.files.wordpress.com/2010/01/p1030608-1.jpg)

D’après lui, l’héritage est un handicap, la composition est une bonne chose, le polymorphisme aussi.

<!--more-->

Mais voila, c'est mon blog, alors je parle de ce que je veux :)
Ceci dit, j'avoue que çette présentation m'a fait réfléchir. A vrai dire, ça m'a presque empêcher de dormir!

Après de longues réflexions, je ne pense pas que l'objet soit une erreur historique. Freddy souligne bien le fait que l'objet est complexe, et pas facile à maitriser. Vous en connaissez beaucoup qui ne font jamais une erreur d'architecture? Qui maitrise le MVC, l'AOP et l'ORM ? (à part moi? ^^)

Ma définition de l’objet est différente : pour moi, tout est objet, c’est l’unité atomique en programmation.
On peut tout faire avec des objets, les meilleurs choses comme les pires.
Je distingue  plusieurs catégories d’objets suivant leurs responsabilités:



### 1 - Object domain


L'Object Domain est une représentation d’un composant métier (au sens **DDD **du terme). Un objet possède un état et un comportement. Une _facture_ par exemple possède un état représenté par son "prix", et un comportement comme "appliquer une remise".



### 2 - Services


Le service est un Objet ayant pour responsabilité de fournir des traitements, c’est-a-dire qu’il n’a pas d’état mais seulement un "comportement". En DDD, ces services permettent de calculer des choses qui impliquent plusieurs graphes d'objet. Si une _facture_ sait calculer son propre prix, elle n'est pas capable de calculer le profit du mois courant, c'est donc la responsabilité d'un objet de plus haut niveau, c'est à dire le service.



### 3 - Repository


Un Repository est un service spécial qui a pour objectif de faire l’interface entre le programme et les sources de données, que ce soit des Base de données, fichiers, caches mémoire, WebService ou WMI. Comme le Repository fait référence à une source de données externe (non en mémoire) il n’est pas testable unitairement.
Le Repository fait office de référence des données, on peut dire alors qu’il possède l’instance "de référence" d’un objet.



### 4 - Factory


Si le Repository est responsable de charger ou modifier les données existantes, la Factory quand a elle est responsable de créer une nouvelle donnée. La Factory est un service, qui a donc connaissance des différents objets du SI pour en construire un nouveau. On peut imaginer que la Factory construise une facture avec un "ReferenceNumber" calculé intelligemment en fonction de la date du jour, et du prochain numéro de factures en fonction de celles déjà existantes: `#QUOTE_230110_0002`



### 5- Data Transfert Objects (DTO)


C’est le fameux **DataSet** de Freddy. Si l’objet du domaine ne possède plus de constructeur (Factory) ne possède plus de procédures/fonctions (Service&Repository), il ne lui reste que l’état, c'est-à-dire une ensemble de données.

On peut alors parler de "structure" ou de "type valeur". Il ne sert qu’à être "sérializé" à travers un réseau, ou entre 2 programmes, et passer de tier en tier, de l’interface à la source de données. Avoir une unique instance importe peu, ce n’est d'ailleurs pas possible en N-Tier, on l’identifie alors avec son ID.



### 6 - Message


C’est en quelque sorte la "**Command**" ou la "**Query**" de **CQRS**. C’est un objet qui représente une action à faire: une requête (query) pour récupérer un objet, ou une action (command) à effectuer dans le programme. L'utilisation d'un objet "message" permet de réduire le nombre d'arguments d’une méthode, ou ne donner que ce qui est nécessaire à la méthode: comme le dit Udi, rien ne sert de donner TOUT l’objet métier à la fonction `ComputeDiscount()`, son ID et le Pourcentage suffisent.



## Comment utiliser tout ceci


Pour donner un retour d'expérience, je vais expliquer comment j'utilise ces objets en général.

En réalité, j'utilise très très rarement des méthodes dans des objets. Mes objets du domaine peuvent alors se résumer à des DTO.
Je séparer le comportement dans des services.

J'utilise aussi très peu l'héritage. Je me sert très souvent de la composition, voir de l'AOP.

Je n’ai pas parlé des interfaces, mais c’est un concept important puisque comme dit Freddy:


<blockquote>"tout est boite noire, c’est le principe de composition".</blockquote>


L'interface au sens "POO" est donc l'intermédiaire entre l'utilisateur (le code appelant) et ce qu’il y a dans la boite noire (implémentation).
Ces interfaces ont aussi un rôle très important dans l'interopérabilité, ou les systèmes distribués: il est donc dommage que ces notions ne soit pas inhérente au langage, quelque soit la technologie de communication.



### Procédure ou Fonction?


En ce qui concerne le comportement, on peut distinguer la "procédure" et la "fonction" : La fonction au sens "fonctionnel" du terme, est sensé calculer un résultat sans effet de bord (sans altéré l’état de l’objet ou de ses paramètres). La procédure par contre, ne renvoi aucun résultat et ne sert qu’à altérer l’état de l’objet.
Les langages modernes ne font pourtant pas la distinction entre ces 2 notions, et c’est peut-être une erreur (on avait pourtant le "const" en C++).
Si Freddy suggère que l'objet est un échec, je pense que les "procédures" le sont. Depuis de début de ma formation informatique, on nous met en garde contre les effets de bord, et l'on trouve divers mécanismes pour les éviter, alors qu'on peut simplement "interdire" les procédures. Il faut en tout cas un concept "d'immutabilité" clair pour savoir ce que "la procédure/fonction" fait exactement.



### Référence ou Valeur?


On distingue l'identité d'un objet par sa référence, ou son instance en mémoire (c'est à dire son adresse mémoire). Mais ce n'est clairement pas représentatif de la réalité. Dans un contexte distribué comme l’a dit Freddy, ce n’est pas possible: la donné existe dans plusieurs mémoires (plusieurs programmes) et plusieurs machines. Il existe alors plusieurs instances d’une même données : dans l'interface du programme client, sur le serveur de WebService et dans la base de données.

Les références sont donc inutiles, puisque la donnée existe partout, mais on a du coup besoin d’identifier un objet à l'aide d’autre chose, et c'est souvent un "ID" qui sera la clé en BD. Il serait utile aussi de connaitre sa "version", afin de résoudre mieux résoudre les changements, tout comme dans un gestionnaire de code source.

Donc finalement, les objets du domaine ne sont que des DTOs, tout comme des "Datasets typés".
Mais parfois nous avons besoin de représenter une même donnée sous différente forme.
Exemple: J'ai besoin de récupérer une liste de "Factures" avec son total calculé, ou parfois j'ai besoin de la même "Facture" mais avec son détail: InvoiceListItemDto & InvoiceDetailDto.

Le problème est le suivant: j'ai une fonction qui calcule le totale avec taxe, qui prend en paramètre un InvoiceDetailDto alors que je manipule un InvoiceListItemDto.

Je me retrouve avec un type incompatible, et pourtant, ma fonction a besoin de champs existant aussi bien dans le premier que le deuxième type: un total hors taxe.

```C#
float ComputeWithTaxes(InvoiceDetailDto dto);
var invoice = new InvoiceListItemDto();
ComputeWithTaxes(invoice); // !!! ça marche pas
```

Faut-il alors de l'héritage pour que la fonction prenne en paramètre un type commun?
Ah NON! Si je commence comme ça, je vais avoir besoin de multiple héritage rapidement, pour de multiples fonctions. Et comme je code en C#, je n'ai pas de multiple héritage.

Alors ai-je besoin d'une interface commune? Mais dans ce cas, vais-je faire une interface pour chaque fonction?? Ors de question.

Une solution existe alors pour convertir un type "presque identique" à un autre: AutoMapper!!
Une solution proposé par Fredy, c'est de ne pas typer tout simplement. Ma fonction va alors "planter" si elle n'a pas les informations attendues, mais fonctionnera le reste du temps.
Mais une autre solution plus simple existe: je peux simplifier la fonction pour ne lui donner **QUE CE QUI EST NECESSAIRE**:

```JAVA
float ComputeWithTaxes(float totalWithoutTaxes);
```
OK, dans ce cas c'est simple. Mais si j'ai besoin de 10 paramètres à ma fonction?



### Paramètres ou Messages?


Comme je l'ai dit au début, un peut utiliser des objets, qui ont une duré de vie très courte puisqu'ils ne servent qu'a représenter une liste d'argument d'une méthode.
Cela simplifie l'appel de la méthode, et rend la lecture du code plus lisible.

Prenons par exemple l'interface suivante:

```JAVA
public class InvoiceService
{
  Invoice ProcessMessage(ApplyDiscountMessage message)
  {
    // do some stuff
  }

  object ProcessMessage(object unknownMessage)
  {
    // ignore it, unkown message type
  }
}```

Grâce au polymorphisme, nous avons un comportement dynamique qui traite le message si son type est connu.
Si tout les services sont capables de prendre une commande, ils peuvent se spécialiser pour traiter certains type de commandes et ignorer les autres.
Un appel à la méthode "ProcessMessage" ne provoquera alors jamais une erreur de compilation, mais peut être ignoré dans le pire des cas.

Et puisque mon programme peut posséder plusieurs services capables de traiter un même type de message, je peux alors le dispatcher à chacun d'eux.
Exemple :

```C#
Factory.GetServices().ProcessMessage(new ApplyDiscountMessage {id=1, discount=10.0}) ;
```



## Un nouveau langage!!


En reprenant donc tous ces concepts, je peux TOUT modéliser avec les objets tels qu’on les connaît aujourd’hui.
Mais pour être plus efficace pour la réalisation des différentes briques du SI et modéliser facilement le métier sans rentrer dans la technique, on a peut-être besoin de plusieurs DSL pour chaque aspect du SI, même si ces DSL reposent sur l'objet (tout comme le langage qui s'appuie sur l'assembleur).

Je vais donc essayer de reprendre les concepts cité plus haut, et en faire un NOUVEAU LANGAGE!!

Reprenons le plus important: **"Pas d'objet, des données!"**.
Soit alors la définition d'une donnée comme ceci:

```C#
data Person
{
  key int Id;

  version int Version;

  unique max(20) string SocialSecurityNumber;

  DateTime Birthday;

  string Firstname;

  string Lastname;
}
```

Il n'y a ici que de la donnée, pas de comportement. Donc inutile de rendre des choses privés, si aucunes méthodes ne peut s'en servir.
Comme je l'ai dis plus tôt, on a besoin d'un identifiant pour cette donnée. Pourquoi ne pas l'inclure au langage?
De même pour la version ou les contraintes sur les données.
Si vous souhaitez calculer l'age de la personne, il suffit alors de demander à un service de le faire:

```C#
contract PersonContract
{
  float ComputeAge(Person this);

  string SayHelloTo(Person this, Person otherPerson);

  string Talk(Person this, Person to, string message);

  Person HappyBirthDay(Person this);

  Person BuildNew();
}
```
Ceci est une "interface", ou dirais-je un "contrat". Comme le dit Freddy: pas besoin de "private/public" puisque toute implémentation est privé et toute interface est publique.
Voici donc l'implémentation:

```C#
// on parle beaucoup "d'injection de dépendance", c'est même maintenant une JSR en Java,
// ou un mot clé dans le langage NOOP. Un contrat peut donc dépendre d'un autre contrat
service PersonService : PersonContract<Person>
   depends MathContract,optional DateContract, PersonRepository
{
  float ComputeAge() =>
    this.Birthday-DateTime.Now;

  string SayHelloTo(Person otherPerson) =>
     "Hello {otherPerson.FirstName} {otherPerson.LastName.ToUpper()}";   

  string Talk(Person to, string message) =>
     var m = message??"Hello";
     "Hey {to.FirstName}, {m}!";

  Person HappyBirthDay(Person this) =>
     this.Birthday = this.Birthday.AddDays(1);
     this;

  Person BuildNew()=>
     var id = PersonRepository.GetNextId();
     new Person{ Id = id };
}
```

On peut alors imaginer une utilisation de ce service comme ceci:

```C#
// constructeur? pas besoin avec des types valeur...
Person moi;

// ... mais on peut imaginer une initialisation "à la C#3", ou dirais-je,
// comme un tableau puisque chaque structure est comme un tableau typé
Person freddy = { Firstname = "Freddy", Lastname = "" };

// ... ou demander à une Factory de le construire
Person other = Person.BuildNew();

// la données n'ont pas de méthode, mais rien n'empêche d'utiliser les services comme les méthodes d'extensions?
moi.SayHelloTo(Freddy);

// imaginons aussi que les paramètres sont nommé comme en C#4
// l'ordre n'a donc pas d'importance...
moi.Talk(message = "Salut", to = Freddy)

// ... et les paramètres ont des valeurs par défaut
moi.Talk(to = Freddy);
```



## Conclusion (enfin)...


Après ce petit essaie, il ne me reste plus qu'à maitriser [http://www.antlr.org/works/index.html](http://www.antlr.org/works/index.html) et réaliser mon propre langage ;)



Cette proposition de langage ne résout pas un dernier problèmes évoqué par Freddy concernant l'objet: le typage fort.
Je ne suis pas sûr que le Javascript soit le meilleur langage du monde :) ça me fait perdre trop de cheveux lors des "debugging-party".
Je ne suis pas fan d'écrire du code qui "peut être marche", je préfère éviter de longue journée de débuguage devant le client.


C'est parfois utile, c'est pourquoi C#4 offre maintenant le mot clé "dynamic". Mais dans certain cas on souhaite s'assurer que le programme est viable, et pour cela il existe la programmation par "contrat" comme le propose [Spec#](http://bit.ly/7LEZiE).



Bref, rien de bien nouveau donc. La plupart des propositions proviennent de langages déjà existant. On en revient toujours au même problème: est-ce l'outil qui est mal adapté? Ou est-ce qu'on l'utilise pas comme il le faut? Je ne suis donc pas sectaire, et apprendre de nouveau langage, objet, fonctionnel ou autre, ne me dérange absolument pas. C'est pour moi un métier passionnant que d'apprendre toutes ces choses et utiliser le langage adapté situation.

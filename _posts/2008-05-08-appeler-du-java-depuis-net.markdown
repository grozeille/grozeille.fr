---
author: grozeille
comments: true
date: 2008-05-08 18:34:15+00:00
layout: post
excerpt_separator: <!--more-->
slug: appeler-du-java-depuis-net
title: Appeler du Java depuis .Net
wordpress_id: 53
categories:
- Developpement
tags:
- .Net
- c++
- interop
- java
- jni
---

Deux mondes s'affrontent: Java et .Net. Chacun choisi son camp, ou choisi les deux... moi j'ai la double nationalité :) Mais quand les deux mondes doivent alors communiquer? Je fais l'interprète. Voila le topo:
J'ai une application .Net qui a besoin de manipuler des classes Java, et pour se faire je passe par [C++/CLI](http://en.wikipedia.org/wiki/C%2B%2B/CLI): comment avoir un pied dans du .Net et un autre dans du natif C++.

<!--more-->

L'avantage de C++/CLI ([Common Language Infrastructure](http://en.wikipedia.org/wiki/Common_Language_Infrastructure)) c'est qu'on peut mixer du code managé et non-managé. Je peux donc compiler un assembly .Net en C++, qui lui fait appelle à du pure code C++ natif. Ici en l'occurrence j'utilise `"jni.h"` pour communiquer avec la JVM à l'aide de `jvm.dll`.

Rentrons dans le vif du sujet: qu'est-ce que ça donne du coté de mon application C#:
```C#
// on démarre la JVM avec mes bons arguments
MathiasJniCpp.JVMWrapper.InitJvm(new String[] { "-Djava.class.path=Mathias.Jni.Java.jar" });

// on créer un objet .Net qui wrappe l'objet Java
// en C++/CLI, le destructeur des classes CLI sert de méthode "Dispose"
using (MathiasJniCpp.MyJavaWrapper javaObject = new MathiasJniCpp.MyJavaWrapper())
{
// faire mumuse avec...
javaObject.People = "Mathias";
Console.WriteLine(javaObject.SayHello());
}

// on libère la JVM
JVMWrapper.ReleaseJvm();
```

`MathiasJniCpp` c'est le namespace de mon assembly c++/cli, j'en reparlerai plus tard.
On voit que je manipule une classe JVMWrapper qui me permet de charger une JVM (et de la libérer). J'utilise aussi une classe .Net codé en C++/CLI. En fait, je l'utilise comme un classe C#, ou VB.net etc. C'est une classe "classique" .Net avec des méthodes et des propriétés.

Point intéressant à souligner: pourquoi utiliser `using`?
Pour rappelle, il y a des mots-clefs en C# très lié au Framework (comme `foreach`) et `using` en fait partie. Il prend les objets qui implémente `IDisposable` et fait appelle à la méthode `Dispose()` à la fin du bloque. Comme ça, je suis sûr de libérer la classe du coté JVM quand j'en ai plus besoin.

Je ne vais pas montrer tout le code, car trop long et [disponible ici](http://www.box.net/shared/ropzl4u80o).
Mais voici un aperçu de la classe C++:
```C++
#include "jni.h"
public ref class MyJavaWrapper
{
private:
  static jmethodID initMethodId;
  static jclass clazz;
  jobject obj;
public:
  /* initialisation des métadata Java/JNI, à voir plus tard */
  static void initJavaMetadata()
  { ... }

  /* une méthode de notre classe Java que l'on wrappe, expliqué aussi plus tard */
  String^ SayHello(String^ people)
  { ... }

  /* constructeur */
  MyJavaWrapper(void)
  {
    // histoire de récupérer toutes les métadatas nécessaires du coté Java
    MyJavaWrapper::initJavaMetadata();

    // construction d'une instance avec le constructeur par défaut
    this->obj = JVMWrapper::env->NewObject(MyJavaWrapper::clazz, MyJavaWrapper::initMethodId);
  }

  /* "destructeur" */
  virtual ~MyJavaWrapper(void)
  {
    JVMWrapper::env->DeleteLocalRef(this->obj);
  }
};
```
`ref class` veut dire "c'est une classe .Net". Mais... ma classe n'implémente pas `IDisposable`!! Et c'est quoi ce destructeur??
Et oui: le destructeur C++ pour un objet .Net est transformé en la méthode `Dispose()` et la classe devient alors forcement `IDisposable`. Pour gérer le `finalize` [allez voir ici](http://dotnet.developpez.com/faq/cppcli/?page=syntaxe#finalizer_vs_destructor).

Je manipule le membre `this->obj` qui est tout simplement un "pointeur" sur notre objet java. En fait, c'est un `jobject` qui est un type définie dans `"jni.h"`.
J'utilise la classe JVMWrapper qui me permet de communiquer avec la JVM, et je lui demande de créer un nouvel objet d'une certaine classe `jclass` avec un certain constructeur `jmethodID` et j'obtiens ainsi mon `jobject`.
_Étant donnée que la classe et la méthode ne change pas, j'ai rendu ces données `static`._

Voyons maintenant ce que fait `MyJavaWrapper::initJavaMetadata();`:
```C++
/* initialise les metadata du coté Java */
static void initJavaMetadata()
{
  // si les métadata ne sont pas déjà récupérées...
  if(MyJavaWrapper::clazz == NULL)
  {
    MyJavaWrapper::clazz = JVMWrapper::env->FindClass("mathias/jni/java/MyJavaClass");
    MyJavaWrapper::initMethodId = JVMWrapper::env->GetMethodID(MyJavaWrapper::clazz, "", "()V");
  }
}
```

C'est la dedans que j'obtiens une fois pour toute la représentation de la classe Java `mathias.jni.java.MyJavaClass` et la représentation de la méthode `<init>` avec en paramètre `()V`.
Pour comprend le lien avec la classe, il n'y a pas trop de problème: c'est le [fully qualified name](http://en.wikipedia.org/wiki/Fully_qualified_name) avec des '/' au lieu des '.'.
Mais en ce qui concerne la recherche d'une méthode, ça devient du charabia!!
En fait, `<init>` est une méthode un peu spéciale: c'est un constructeur.
Ensuite, on spécifie les arguments du constructeur que l'on cherche, et la on tombe sur une syntaxe barbare. Dans notre cas, on cherche le constructeur par défaut c'est à dire qui ne prend pas d'argument.
Mais pour mieux comprendre la syntaxe barbare, voyons d'autres exemples de méthodes:
```C++
JVMWrapper::env->GetMethodID(MyJavaWrapper::clazz, "setPeople", "(Ljava/lang/String;)V");
```
Traduction: je cherche la méthode `setPeople` qui prend un argument de type `java.lang.String` et qui retourne `void`.
Un autre exemple:
```C++
JVMWrapper::env->GetMethodID(MyJavaWrapper::clazz, "sayHello", "([Ljava/lang/String;Z;)I");
```
Traduction: je cherche la méthode `sayHello` qui prend un argument de type `java.lang.String[]` et un autre de type `boolean` et qui retourne un type `int`.

On retrouve cette syntaxe à beaucoup d'endroits, comme sous [Eclipse](http://grozeille.files.wordpress.com/2008/05/eclipsejni.png) par exemple. Pour plus d'explication voir la [documentation officielle](http://java.sun.com/j2se/1.4.2/docs/guide/jni/spec/types.html).

Si l'on veut maintenant appeler une méthode Java, on récupère sa représentation tout comme on le fait avec le constructeur, puis on l'invoque sur notre instance:
```C#
public ref class MyJavaWrapper
{
private:
  static jmethodID initMethodId;
  static jclass clazz;

  // notre représentation JNI de la méthode "sayHello"
  static jmethodID sayHelloMethodId;

  jobject obj;
public:
  /* initialisation des métadata Java/JNI */
  static void initJavaMetadata()
  {
    /* initialisation de la classe et du constructeur, comme vu précédemment
    [...]  */

    // on récupère la représentation de "sayHello"
    JVMWrapper::env->GetMethodID(MyJavaWrapper::clazz, "sayHello", "(Ljava/lang/String;)Ljava/lang/String");
  }

  /* sur l'appelle de cette méthode .Net, on fait appelle à la méthode Java */
  String^ SayHello(String^ people)
  {
    // j'utilise une classe spéciale pour convertir ma String^ .net en natif ou Java
    StringConverter peopleStringConverter(people);
    jstring jPeople = peopleStringConvert.toJava();

    // appelle de la méthode Java, j'ai le droit de caster en jstring car c'est un sous-type de jobject
    jstring jResult = (jstring)JVMWrapper::env->CallObjectMethod(this->obj, sayHelloMethodId, jPeople);

    // conversion du type Java en .Net
    StringConverter resultStringConvert(jResult);
    return resultStringConvert.toDotnet();
  }
};
```

Voila, maintenant vous savez:




  * obtenir la représentation d'une classe Java


  * obtenir la représentation d'une méthode d'une classe


  * créer une instance d'une classe Java


  * invoker des méthodes sur une instance



En conclusion:
l'API JNI c'est un peux comme utiliser la réflection. Ça a donc des conséquences en termes de performance. Pour information, créer 10000 objet en java prend _625ms_, en pure .net ça donne _46ms_ et en .Net->JNI->Java ça donne _2.687s_.
L'API JNI peut sembler barbare au début, mais on s'y fait :) et puis il y a [la doc](http://java.sun.com/j2se/1.4.2/docs/guide/jni/spec/functions.html#wp20949), alors [RTFM](http://en.wikipedia.org/wiki/RTFM) ;).

C++/CLI c'est de la bombe en termes d'interop. C'est le pont parfait entre le monde .Net et le natif.
L'inconvénient c'est que la syntaxe C++ est lourde. Et elle l'est d'autant plus en C++/CLI car il faut y ajouter les spécificités .Net, et il faut aussi distinguer une instance managée et non-managée, et tout ça passe par de nouveau symboles/mots-clefs.
Les conversions de types entre les deux mondes ne sont pas faites implicitement, et il faut souvent jongler pour avoir le bon type. J'ai par exemple eu des problèmes lors des conversions de String avec JNI: il faut convertir la `String^` .net en `char*` natif pour enfin construire une `jstring`. Les conversions ont été le plus pénible dans l'histoire.

Enfin, voici le projet complet: [Mathias.Jni.CSharp.zip](http://www.box.net/shared/ropzl4u80o)
Un petit rappel des liens utiles:




  * [http://dotnet.developpez.com/faq/cppcli/](http://dotnet.developpez.com/faq/cppcli/)


  * [http://java.sun.com/j2se/1.4.2/docs/guide/jni/spec/jniTOC.html](http://java.sun.com/j2se/1.4.2/docs/guide/jni/spec/jniTOC.html)

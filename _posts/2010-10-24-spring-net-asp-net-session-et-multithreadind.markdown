---
author: grozeille
comments: true
date: 2010-10-24 19:22:00+00:00
layout: post
slug: spring-net-asp-net-session-et-multithreadind
title: Spring.Net, ASP.Net, Session et multithreadind
wordpress_id: 452
categories:
- Developpement
tags:
- .Net
- Asp.net
- Spring.net
---

Pour commencer, je vous préviens, ce billet s’adresse à ceux qui savent développer en ASP.Net.
Je ne plaisante pas! J’ai vu un trop grand nombre de gens prétendre savoir faire des applications Web sans savoir m’expliquer le protocole HTTP!
Donc voici un petit test d’entré:




  * Comment fonctionne un HttpHandler?


  * Pourquoi ne pas utiliser les UpdatePanels?


  * A quoi sert un MembershipProvider et comment s’en servir?


Si ces questions vous paressent obscures et que vous êtes plutôt un développeur “glisser-déposer”, alors je vous propose de vous “glisser-déposer” sur un autre blog ;)

Pour les autres, j’ai un aveu à vous faire: je viens de découvrir qu’il n’est pas possible d’afficher 2 pages ASP.Net en simultané si elles accèdent à la Session.

<!-- more -->

J’ai cru que j’étais sous l’effet d’une drogue… mais non, c’était bien vrai.
J’ai alors voulu en avoir le cœur net, et j’ai fouillé de nombreux forums… c’est la que j’ai découvert que d’autres l’on découvert après 5 ans d’expériences en ASP.Net!!!

Certes, on ouvre rarement 2 pages Web d’un même site, mais il est plus fréquent d’avoir 2 appelles Ajax en simultané.
C’est mon cas, car j’aime Ajax, j’aime le Web, et j’utilise une technique “Comet” appelé “Long Pooling”. Cela consiste à faire un appelle Ajax potentiellement infinie, qui va se terminé seulement si le serveur à quelque chose à nous dire. Cela permet d’avoir un système de notification très simple à implémenter.

Pour vulgariser, au lieu d’avoir ça:


> Client: “Tu veux me dire quelque chose?”
> Server: “Non”
> Client: “Tu veux me dire quelque chose?”
> Server: “Non”
> Client: “Tu veux me dire quelque chose?”
> Server: “Mais lâche moi sale client!!!”


En long polling ça donne ça:


> Client: “Bon, tu me préviens si t’as un truc à me dire...”
> Server: “...”
> Server: “...”
> Server: “...”
> Server: “...”
> Server: “... ouai, j’ai un truc pour toi, un nouveau message”
> Client: “OK, je le traite, bon, tu me préviens si t’as un autre truc à me dire...”


Et sinon, en C# ça donne ça:

```C#
public string LongAjaxCall()
{
    string result = null

    while(result == null)
    {
        lock(this.notificationList)
        {
            if(notificationList.Count > 0)
            {
                result = new JavaScriptSerializer().Serialize(this.notificationList.ToArray());
                this.notificationList.Clear();
            }
        }
        if(result == null)
            Thread.Sleep(500);
    }
}
```

En général, le serveur n’a pas les mêmes choses à dire aux différents clients, c’est pourquoi on utilise la Session. Mais cette dernière est verrouillée par le long pooling, l’utilisateur ne sera alors pas en mesure d’ouvrir une nouvelle page si l’appelle Ajax ne se termine pas, ce qui est plutôt fâcheux.


## Et Spring.Net dans tout ça?


J’utilise massivement Spring.net, pas seulement pour l’IOC, mais pour bien d’autres choses que ce merveilleux framework offre.
Dans le cadre d’une application Web, il est possible d’avoir un “scope” pour les instances des objets:




  * **application**: un singleton pour toute l’application Web


  * **session**: l’instance n’existe que dans le cadre d’une session ASP.Net


  * **request**: l’instance n’existe pour pour la duré de la requête HTTP


J’utilise pas mal le scope “Session”, afin d’instancier des “contrôleurs” différents pour chaque utilisateurs. Je peux ainsi conserver un état à l’aide des membres de mes contrôleurs (ou conserver une connexion SQL, etc.).

Je vous propose alors de jeter un œil à mon exemple afin de comprendre mon problème: [http://bitbucket.org/grozeille/testaspsessionmultithread/src](http://bitbucket.org/grozeille/testaspsessionmultithread/src)
Cette solution contient un premier exemple “[TestASPSessionMultithread.Bad](http://bitbucket.org/grozeille/testaspsessionmultithread/src/tip/TestASPSessionMultithread.Bad/)” qui illustre mon problème.

L’exemple est simple:
Vous avez une première page “_Default.aspx_” qui permet d’ajouter une “_string_” à une liste à l’aide du button “_add_” qui effectuera un appelle Ajax.
Vous pouvez alors ensuite déclencher un “_long pooling_” à partir du boutton “_long polling_” qui va demander au serveur de renvoyer les nouveaux items.


[](http://grozeille.files.wordpress.com/2010/10/image.png)[![](http://grozeille.files.wordpress.com/2010/10/longpooling01.png?w=300)](http://grozeille.files.wordpress.com/2010/10/longpooling01.png)


Dans cet ordre, tout va bien. Par contre, si vous faite un “_long pooling_” en premier, le boutton “_add_” restera bloqué et il sera donc impossible d’ajouter un nouvel item.


[![](http://grozeille.files.wordpress.com/2010/10/longpooling02.png?w=300)](http://grozeille.files.wordpress.com/2010/10/longpooling02.png)


De même, vous pouvez tester aussi la page “_Other.aspx_” qui simule un lourd traitement qui prend 5 secondes. Quand vous essayer d’ouvrir la page “_Other_” et que vous tentez de recharger la page “_Default_” en parallèle, cette dernière va attendre la fin du chargement de la page “_Other_”.


[![](http://grozeille.files.wordpress.com/2010/10/longpooling03.png?w=300)](http://grozeille.files.wordpress.com/2010/10/longpooling03.png)


A noter aussi que j’affiche le _“creation time_” des différents contrôleurs. Puisque Spring.Net permet d’avoir du LazyLoad, on voit que le _OtherController _est créé après le _DefaultController_.

Si vous regardez le code en détail, vous pouvez voir que je gère les appelles Ajax à l’aide d’un _HttpHandler _custom.
Je pense que le code est suffisamment bien commenté pour le comprendre, et pour ceux qui ont la flemme de récupérer le source depuis BitBucket, voici l’extrait:

[code language="csharp"]
public class BadAjaxHttpHandler : IHttpHandler, IRequiresSessionState
{
    public void ProcessRequest(HttpContext context)
    {
        // get the name of the controller and the action from the URL
        var action = context.Request.Url.Segments[context.Request.Url.Segments.Length - 1];
        var controller = context.Request.Url.Segments[context.Request.Url.Segments.Length - 2]
            .Replace(".ajax", string.Empty)
            .Replace("/", string.Empty);

        // get the instance of the controller thanks to its name
        var instance = ContextRegistry.GetContext().GetObject(controller);

        // get the method of the controller thanks to reflection
        var method = instance.GetType().GetMethod(action, BindingFlags.Instance | BindingFlags.Public);
        var args = new List();
        foreach (var item in method.GetParameters())
        {
            args.Add(TypeDescriptor.GetConverter(item.ParameterType).ConvertFromString(context.Request.Params[item.Name]));
        }

        // invoke the method of the controller
        var result = method.Invoke(instance, args.ToArray());

        // return the JSON value of the method result
        context.Response.Write(new JavaScriptSerializer().Serialize(result));
        context.Response.StatusCode = 200;
        context.Response.End();
[/code]

On remarque que pour accéder à la session nous avons ici besoin d’implémenter l’interface “_IRequiresSessionState_”, mais la aussi, comme c’est en lecture/écriture, cela verrouille la session le temps de la requête HTTP.


## Comment résoudre le problème?


La solution est dans le projet “[02-TestASPSessionMultithread.Good.Unsecured](http://bitbucket.org/grozeille/testaspsessionmultithread/src/tip/TestASPSessionMultithread.Good.Unsecured/)”.

Pourquoi “Unsecured” ? On verra ça plus tard.

La solution est simple, il suffit d’accéder à la Session en “lecture seule”.
En effet, il peut être problématique d’ajouter une même clé depuis 2 thread concurrents, mais une fois que la clé est créée, c’est à vous de gérer la concurrence de la valeur.

Exemple:

[code language="csharp"]
Session[“list”] = new List(); // problème de concurrence, donc session verrouillée

((List)Session[“list”]).Add(“toto”); // ce cas est une lecture seule de la session, mais à vous de gérer la concurrence pour la collection
[/code]

Comme Spring.Net est en quelque sorte une “grosse collection d’instance”, et que Sprint.net utilise une seule clé “spring.object”, cela s’applique aussi :)

Par défaut, les pages sont en accès Write à la session. Pour changer cela, il faut ajouter une option dans l’ASPX:

[code language="html"]
<%@ Page EnableSessionState="ReadOnly"  %>
[/code]

Il a fallut un petit changement dans le HttpHandler Ajax aussi:

[code language="csharp"]
public class AjaxHttpHandler : IHttpHandler, IReadOnlySessionState
[/code]

Cette nouvelle interface “_IReadOnlySessionState_” parle d’elle même :)

Et voila! C’est tout! Ca marche, plus de problème de concurrence!
Enfin… non ce n’est pas tout, on a un petit problème, c’est que Sprint.net ne pourra plus jamais initialiser la session sans accès en écriture :(
Il faut donc trouver un “bootstrap” qui accède à la session en écriture juste le temps de créer le contexte Spring.Net.

L’astuce est donc de faire une redirection vers un HttpHandler particulier “_SpringSessionHttpHandler_” si la session est nouvelle. Il peut alors accèder à la session en écriture grâce à l’interface “IRequiresSessionState” pour initialiser le contexte et rediriger vers la page d’origine.

Ceci est fait lors du “_OnLoad_” car nos pages héritent de “_SessionPage_”.

[code language="csharp"]
public class SessionPage : Page
{
    protected override void OnLoad(EventArgs e)
    {
        // build the spring.net session
        if (Session.IsNewSession)
        Response.Redirect("SpringSessionHttpHandler?ReturnUrl=" + Server.UrlEncode(Request.Url.ToString()), true);

        base.OnLoad(e);
    }
}
[/code]

Le code du HttpHandler est très simple: il force la création du contexte Spring dans la session, puis redirige sur la page d’origine qui elle a un accès en lecture seule sur la session.

[code language="csharp"]
public class BadAjaxHttpHandler : IHttpHandler, IRequiresSessionState
    {
        public void ProcessRequest(HttpContext context)
        {
            // get the name of the controller and the action from the URL
            var action = context.Request.Url.Segments[context.Request.Url.Segments.Length - 1];
            var controller = context.Request.Url.Segments[context.Request.Url.Segments.Length - 2]
                .Replace(".ajax", string.Empty)
                .Replace("/", string.Empty);

            // get the instance of the controller thanks to its name
            var instance = ContextRegistry.GetContext().GetObject(controller);

            // get the method of the controller thanks to reflection
            var method = instance.GetType().GetMethod(action, BindingFlags.Instance | BindingFlags.Public);
            var args = new List<object>();
            foreach (var item in method.GetParameters())
            {
                args.Add(TypeDescriptor.GetConverter(item.ParameterType).ConvertFromString(context.Request.Params[item.Name]));
            }

            // invoke the method of the controller
            var result = method.Invoke(instance, args.ToArray());

            // return the JSON value of the method result
            context.Response.Write(new JavaScriptSerializer().Serialize(result));
            context.Response.StatusCode = 200;
            context.Response.End();
        }
[/code]


## Mais quel astuce géniale! ...mais pourquoi “Unsecured” ?


Vous pouvez remarquer que j’affiche l’ID de la session dans la page.
L’identifiant de session est stocké par défaut dans un cookie. J'ai tout de même changé le nom de ce dernier, car si je laisse la valeur par défaut, je risque d’avoir un conflit avec une autre application (erreur de débutant)

[code language="xml"]
<sessionState cookieName="TestSession"/>
[/code]

Normalement, le cookie est “sécurisé”, cad qu’il n’est pas accessible depuis du Javascript malicieux.
Mais bon, un cookie ça reste quand même pas super sécurisé.

Si vous voulez tester un vol de session, il vous suffit de copier/coller l’ID de la session dans un cookie d’un autre navigateur.

Comment faire alors pour sécuriser le tout? Vous avez pour cela différentes solutions:




  * implémenter votre propre gestion d’ID de session avec <sessionState customProvider="MonType">, et vérifier l’identité à l’aide de critère comme l’IP du client


  * coupler la session avec l’authentification


C’est cette dernière solution que je vais vous présenter, car c’est la plus simple.
L’authentification en ASP.Net se fait à l’aide du MembershipProvider, que vous pouvez implémenter vous même. Le framework .Net va alors gérer l’identité à l’aide d’un cookie aussi, mais ce dernier est beaucoup plus sécurisé et vous pouvez y faire confiance.
Je vais alors stocker dans la session la valeur du cookie d’authentification, et vérifier donc l’identité avant d’accéder à la session.

Vous pouvez vérifiez cela par vous même à l’aide du projet [03-TestASPSessionMultithread.Good.Secured](http://bitbucket.org/grozeille/testaspsessionmultithread/src/tip/TestASPSessionMultithread.Good.Secured/)
Si vous tentez de voler le cookie d’authentification pour l’utiliser sur un autre navigateur, vous serez alors déconnecté. Si vous tentez de voler le cookie de session, vous serez alors aussi déconnecté.

Les pages hérites alors de “_SecuredSessionPage_”, et vont alors vérifier le cookie de session dans le "_OnLoad_":

[code language="csharp"]
// if the user tried to steal the session of another user
if (Page.Request.Cookies[FormsAuthentication.FormsCookieName] == null ||
    !Equals(Page.Request.Cookies[FormsAuthentication.FormsCookieName].Value, Session[FormsAuthentication.FormsCookieName]))
{
    this.Logout();
}
[/code]

Je vous laisse ensuite découvrir l'implémentation de l'authentification, mais ce n'est pas le sujet de ce billet et il n'y a rien de plus classique.


## Conclusion


Si comme moi vous utiliser Spring.net avec ASP.net et que vous avez des problèmes de lenteur, essayer cette astuce :)

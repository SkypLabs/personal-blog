+++
title = "Impossible de démarrer Google Chrome sous Fedora 15"
date = 2011-10-15
template = "post.html"

[taxonomies]
categories = ["SysAdmin"]
tags = ["Google Chrome", "Fedora"]
+++
Mon ordinateur portable tournant sous **Fedora 15**, j'ai récemment eu quelques
soucis pour démarrer **Google Chrome** après avoir fait les dernières mises à
jour officielles du dépôt de Google. La dernière mise à jour en date étant la
suivante : `google-chrome-stable-15.0.874.106-107270.i386`.

Le problème provient d'un conflit de permissions lié à **SELinux**. Pour
corriger cela, il faut modifier le type du contexte de sécurité de l'application
**chrome-sandbox** :

```
chcon -t usr_t  /opt/google/chrome/chrome-sandbox
```

+++
title = "[FreeBSD] Créer une interface de loopback au démarrage"
date = 2012-07-12
template = "post.html"

aliases = [
  "/2012/07/12/freebsd-creer-une-interface-de-loopback-au-demarrage/",
  "/freebsd-create-loopback-interface",
]

[taxonomies]
categories = ["SysAdmin", "Network"]
tags = ["FreeBSD"]
+++
Sous FreeBSD, pour créer une interface virtuelle de type loopback au démarrage
du système (nommée `lo1` pour l'exemple), il faut ajouter le fichier
`/etc/start_if.lo1` et ce dernier devra contenir la commande suivante :

```
/sbin/ifconfig lo1 create
```

Pour la configuration de l'interface, cela se passe dans le fichier
`/etc/rc.conf`.

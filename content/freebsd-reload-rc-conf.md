+++
title = "[FreeBSD] Recharger le fichier /etc/rc.conf sans redémarrer votre machine"
date = 2011-12-31
template = "post.html"

aliases = [
  "/2011/12/31/freebsd-recharger-le-fichier-etcrc-conf-sans-redemarrer-votre-machine/",
]

[taxonomies]
categories = ["SysAdmin"]
tags = ["FreeBSD"]
+++
Voici une petite astuce permettant de gagner du temps :

```
shutdown now
```

Le fait d'utiliser la commande `shutdown` sans les arguments `-r` ou `-h` (ou
encore `-p`) permet de passer le système en mode **single user**. Après ceci,
quand le système vous le propose, appuyez sur la touche entrée pour récupérer un
shell. Puis, utilisez la commande `exit` (ou la combinaison `ctrl + D`) pour
revenir en mode **multi user** et ainsi recharger le fichier `/etc/rc.conf`.

Ayez cependant conscience que l'ensemble de vos services vont être relancés
pendant cette procédure.

Bonne année à tous :)

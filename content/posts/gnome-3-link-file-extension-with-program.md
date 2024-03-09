+++
title = "[GNOME 3] Associer l'ouverture d'un programme à une extension de fichier"
date = 2014-01-07
template = "post.html"

aliases = [
  "/2014/01/07/gnome-3-associer-louverture-dun-programme-a-une-extension-de-fichier/",
  "/gnome-3-link-file-extension-with-program",
]

[taxonomies]
categories = ["SysAdmin"]
tags = ["GNOME 3"]
+++
Sous GNOME 3, l'association d'une extension de fichier à un programme référencé
par un fichier de configuration dans `/usr/share/applications` se fait à travers
le fichier `/usr/share/applications/defaults.list` de la manière suivante :

```
application/x-<extension>=<app>;
```

Vous devez remplacer *extension* par le nom de l'extension concernée et *app*
par le nom du fichier de configuration du programme qui doit être utilisé.

Par exemple dans mon cas, pour associer **xournal** comme programme permettant
d'ouvrir les fichiers **xoj**, j'ai ajouté la ligne suivante dans le fichier
`/usr/share/applications/defaults.list` :

```
application/x-xoj=xournal.desktop;
```

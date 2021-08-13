+++
title = "[Fedora] Problème avec Steam et OpenGL sur un système en 64 bits"
date = 2013-04-21
template = "post.html"

[taxonomies]
categories = ["SysAdmin"]
tags = ["Steam", "OpenGL"]
+++
Si Steam vous affiche un message d'erreur lors de son lancement au sujet
d'OpenGL sous Fedora en 64 bits et que vous utilisez le driver propriétaire de
Nvidia, il faut seulement installer la bibliothèque Nvidia 32 bits en utilisant
la commande suivante :

```
yum install xorg-x11-drv-nvidia-libs.i686
```

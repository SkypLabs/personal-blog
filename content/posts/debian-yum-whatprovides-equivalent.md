+++
title = "[Debian] Équivalent de \"yum whatprovides\""
date = 2014-04-27
template = "post.html"

aliases = [
  "/2014/04/27/debian-equivalent-de-yum-whatprovides/",
  "/debian-yum-whatprovides-equivalent",
]

[taxonomies]
categories = ["SysAdmin"]
tags = ["RPM", "Yum"]
+++
Les outils **apt-get** et **aptitude** ne possèdent pas d'équivalent à l'option
`whatprovides` de Yum. Cependant, il existe un logiciel nommé **apt-file**
capable de remplir cette tâche :

```
aptitude install apt-file
apt-file update
apt-file search <file>
```

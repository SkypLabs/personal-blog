+++
title = "[Fedora] Reconstruire la base de données des paquets RPM"
date = 2013-04-21
template = "post.html"

aliases = [
  "/2013/04/21/fedora-reconstruire-la-base-de-donnees-des-paquets-rpm/",
]

[taxonomies]
categories = ["SysAdmin"]
tags = ["RPM"]
+++
```
rm -rf /var/lib/rpm/__db*
rpm --rebuilddb
```

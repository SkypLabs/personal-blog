+++
title = "[Fedora] Reconstruire la base de données des paquets RPM"
date = 2013-04-21
template = "post.html"

[taxonomies]
categories = ["SysAdmin"]
tags = ["RPM"]
+++
```raw
rm -rf /var/lib/rpm/__db*
rpm --rebuilddb
```

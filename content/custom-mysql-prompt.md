+++
title = "Modifier la présentation du prompt sous MySQL"
date = 2012-07-25
template = "post.html"

[taxonomies]
categories = ["SysAdmin"]
tags = ["MySQL"]
+++
Pour modifier la présentation du prompt sous MySQL, il faut éditer la variable
d'environnement `MYSQL_PS1` comme dans l'exemple ci-dessous :

```bash
export MYSQL_PS1="(\u@\h) [\d]> "
```

`\u`, `\h` et `\d` désignent respectivement l'utilisateur, l'hôte et la base de
données.

Pour conserver cette modification, le mieux est d'ajouter cette ligne dans le
fichier `~/.bashrc` de l'utilisateur courant (dans le cas du shell Bash) ou dans
le fichier `/etc/profile` pour cibler tous les utilisateurs.

Cependant, ce n'est pas la seule façon de procéder. Pour plus d'informations,
[cliquez ici][mysql-doc].

 [mysql-doc]: https://dev.mysql.com/doc/refman/5.7/en/mysql-commands.html "Documentation MySQL : MySQL commands"

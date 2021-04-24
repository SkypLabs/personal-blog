+++
title = "[FreeBSD] Mise à jour du port git-1.8.1.1"
date = 2013-01-27
template = "post.html"

[taxonomies]
categories = ["SysAdmin"]
tags = ["FreeBSD", "Git"]
+++
Si vous aussi vous avez eu quelques difficultés à mettre à jour git vers la
version 1.8.1.1 au moyen de son port sous FreeBSD, voici la démarche à suivre
pour solutionner votre problème :

1. On commence par supprimer le groupe `git_daemon` :

    ```raw
    pw group del git_daemon
    ```

2. On supprime la ligne correspondant à l'utilisateur `git_daemon` dans les
   fichiers `/etc/passwd` et `/etc/master.passwd`.

3. On met à jour la base de données des mots de passe :

    ```raw
    pwd_mkdb -p /etc/master.passwd
    ```

Après ceci vous ne devriez plus avoir de problème.

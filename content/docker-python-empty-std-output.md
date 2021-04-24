+++
title = "[Docker] Votre script Python laisse anormalement la sortie standard vide"
date = 2015-11-16
template = "post.html"

[taxonomies]
categories = ["SysAdmin", "Programming"]
tags = ["Docker", "Python"]
+++
Lors de l'exécution d'un programme écrit en Python dans un conteneur Docker, il
arrive régulièrement que la sortie standard reste anormalement vide :

```raw
$ docker logs my-app
$
```

La raison est généralement que par défaut, l'interpréteur Python utilise une
mémoire tampon pour les écritures vers `stdout`. Les écritures sont donc
différées et cela peut prendre un moment avant de voir apparaitre la moindre
ligne d'écriture (selon la verbosité de votre programme).

Une solution est d'utiliser l'option `-u` lors de l'appel à l'interpréteur
Python. Votre `Dockerfile` devra contenir une ligne ressemblant à ceci :

```dockerfile
CMD ["python3", "-u", "my-app.py"]
```

Et ainsi :

```raw
$ docker logs my-app
It works !
$
```

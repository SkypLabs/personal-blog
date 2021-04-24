+++
title = "[GNOME 3] Désactiver le bluetooth au démarrage"
date = 2013-09-22
template = "post.html"

[taxonomies]
categories = ["SysAdmin"]
tags = ["GNOME 3", "Bluetooth"]
+++
Pour modifier l'état de l'interface Bluetooth de votre ordinateur, nous allons
utiliser le programme **rfkill**. Assurez-vous qu'il soit bien installé sur
votre machine :

```raw
yum install rfkill
```

Voici les commandes de base de l'outil :

* Pour afficher l'état actuel de votre interface Bluetooth :

    ```raw
    rfkill list bluetooth
    ```

* Pour activer l'interface Bluetooth :

    ```raw
    rfkill unblock bluetooth
    ```

* Pour désactiver l'interface Bluetooth :

    ```raw
    rfkill block bluetooth
    ```

<!-- more -->

Ainsi, pour désactiver l'interface Bluetooth au démarrage, il faut exécuter la
commande ci-dessus au lancement de GNOME 3. Pour ce faire, faites `Alt + F2`
puis tapez `gnome-session-properties`. Dans l'onglet *Startup Programs*,
utilisez le bouton *Add* afin d'ajouter un programme à exécuter au démarrage.
Enfin, dans la boîte de dialogue qui vient de s'ouvrir, entrez les informations
suivantes :

* Name : Un nom arbitraire désignant la fonction du programme. Par exemple
  "Disable Bluetooth".
* Command : Le chemin absolu de la commande à exécuter afin que les paramètres
  additionnels. Ici `/usr/sbin/rfkill block bluetooth`.
* Comment : Une description optionnelle comme "Turn off Bluetooth by default".

Il ne vous reste plus qu'à valider et à redémarrer votre machine afin de tester
le bon fonctionnement de votre nouvelle configuration.

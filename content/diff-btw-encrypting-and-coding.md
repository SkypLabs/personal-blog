+++
title = "Quelle est la différence entre chiffrer et coder une information ?"
date = 2015-03-26
template = "post.html"

aliases = [
  "/2015/03/26/quelle-est-la-difference-entre-chiffrer-et-coder-une-information/",
]

[taxonomies]
categories = ["Cryptology", "Misc."]
tags = []
+++
Dans un [précédent article](@/crypter-does-not-exist-in-french.md), j'avais
expliqué pourquoi le mot "crypter" n'a aucun sens en français. Je vais continuer
sur ma lancée pour maintenant expliquer la différence entre chiffrer et coder un
message.

Lorsque l'on parle de coder un message, on sous-entend l'utilisation d'un code
de référence qui va permettre aux personnes le connaissant de transformer le
message de notre langue commune à une forme codée et vice versa. Un des exemples
les plus connus est le Morse. Toute personne connaissant le Morse est capable de
comprendre les messages codés avec ce dernier.

Contrairement aux codes comme le Morse, les algorithmes de chiffrement assurent
une confidentialité des messages, que le système cryptographique soit connu ou
non. En effet, dans le cas du chiffrement, seule la clé est confidentielle.
C'est ce qu'énonce le [principe de Kerckhoffs][principe-kerckhoffs], également
repris par Shannon avec sa maxime :

> L'adversaire connaît le système

Il est donc évident qu'utiliser un algorithme de chiffrement est bien plus
judicieux qu'utiliser un code pour rendre ses données confidentielles.

 [principe-kerckhoffs]: https://fr.wikipedia.org/wiki/Principe_de_Kerckhoffs "Principe de Kerckhoffs"

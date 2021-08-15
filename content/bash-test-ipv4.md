+++
title = "[Bash] Tester une adresse IPv4"
date = 2014-04-14
template = "post.html"

aliases = [
  "/2014/04/14/bash-tester-une-adresse-ipv4/",
]

[taxonomies]
categories = ["Programming"]
tags = ["Bash"]
+++
La fonction ci-dessous permet de tester une adresse IPv4 pour vérifier qu'elle
est bien formée :

{{ gist(url="https://gist.github.com/SkypLabs/8758fa2aa63201b028d0ac680b2a90c4",
file="is_ipv4.sh") }}

Et voici un exemple d'utilisation :

{{ gist(url="https://gist.github.com/SkypLabs/8758fa2aa63201b028d0ac680b2a90c4",
file="is_ipv4_example.sh") }}

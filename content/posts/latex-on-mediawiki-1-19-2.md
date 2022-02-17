+++
title = "LaTeX sur MediaWiki 1.19.2"
date = 2012-10-20
template = "post.html"

aliases = [
  "/2012/10/20/latex-sur-mediawiki-1-19-2/",
  "/latex-on-mediawiki-1-19-2",
]

[taxonomies]
categories = ["SysAdmin", "Web"]
tags = ["MediaWiki", "LaTeX"]
+++
Cela faisait plusieurs jours que j'essayais de faire fonctionner l'extension
**Math** de MediaWiki pour pouvoir afficher des équations mathématiques en
LaTeX. Mais lors de mes tests, j'obtenais toujours une erreur HTTP 500
(*Internal Server Error*) et le message suivant dans mes logs :

```
Call to undefined method TempFSFile::autocollect()
```

On peut donc en conclure que la dernière version de l'extension Math n'est pas
compatible avec MediaWiki 1.19.2. Pour résoudre cette situation, il est
nécessaire de revenir à une version antérieure :

```
cd extensions
git clone https://gerrit.wikimedia.org/r/p/mediawiki/extensions/Math.git
cd Math
git reset --hard 29a0a80e8fbb2d33507760075e4da9103439cbd9
```

Merci à **Cgeroux** pour sa contribution [(lien vers ses
explications)][latex-issue].

 [latex-issue]: https://www.mediawiki.org/wiki/Extension_talk:Math

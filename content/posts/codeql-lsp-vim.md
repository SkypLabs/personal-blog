+++
title = "[Vim] Set up CodeQL LSP"
date = 2022-07-10
template = "post.html"

[taxonomies]
categories = ["Programming"]
tags = ["CodeQL", "Vim"]
+++
[CodeQL CLI][codeql-cli] includes a language server which can be easily set up
in [coc.nvim][coc-nvim] by adding the content of this `coc-settings.json` file
to your own configuration file:

```json
{
  "languageserver":{
    "codeql": {
      "command": "codeql",
      "args": [
        "execute",
        "language-server",
        "--check-errors",
        "ON_CHANGE",
        "-q"
      ],
      "filetypes": [
        "codeql",
        "ql"
      ],
      "initializationOptions": {},
      "settings": {}
    }
}
```

Given that coc.nvim uses Vim filetype detection system and not file extensions,
you need to let Vim know about `*.ql` files being CodeQL files. One way to do
that is to add `codeql.vim` to `~/.vim/ftdetect`:

```vim
" Set '.ql' files as CodeQL files.
au BufRead,BufNewFile *.ql set filetype=codeql
```

 [coc-nvim]: https://github.com/neoclide/coc.nvim "coc.nvim GitHub repository"
 [codeql-cli]: https://codeql.github.com/docs/codeql-cli/ "CodeQL CLI Documentation"

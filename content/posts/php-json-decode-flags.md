+++
title = "[PHP] StackOverflow, or how to fail at parsing JSON"
date = 2022-03-09
template = "post.html"

[taxonomies]
categories = ["Programming"]
tags = ["PHP"]
+++
Not too long ago, I was writing a WordPress plug-in for one of my clients, a
simple proxy sitting between the website visitors and a remote third-party
platform not to expose the remote service's API key client-side in the
JavaScript. For this purpose, I had to parse JSON-serialised data, nothing fancy
so far.

PHP has a built-in function to carry out this task,
[`json_decode()`][php-json-decode]. The function has the following prototype:

```php
json_decode(
    string $json,
    ?bool $associative = null,
    int $depth = 512,
    int $flags = 0
): mixed
```

I hadn't touched to PHP in a big while, so I took a close look to the official
documentation to see how to use it properly. Something caught my attention:

> Returns the value encoded in json in appropriate PHP type. Values true, false
> and null are returned as true, false and null respectively. null is returned
> if the json cannot be decoded or if the encoded data is deeper than the
> nesting limit.

The documentation says that the function returns `null` when the parsing routine
has failed or when the input value to parse is actually `null`, which is [one of
the four primitive types in JSON][json-rfc]. Of course, having the same
behaviour in both scenarios is not acceptable if you want to write a reliable
software. Thankfully, the `JSON_THROW_ON_ERROR` flag was added in version 7.3 to
throw an exception upon parsing failure instead of returning the value `null`.

<!-- more -->

To use this feature, I initially thought that I could write something like
`json_decode($input, flags = JSON_THROW_ON_ERROR)` but it turns out [named
parameters are only available since version 8.0 of PHP][php-named-parameters]
which was not available in the production environment of my client.

 [json-rfc]: https://datatracker.ietf.org/doc/html/rfc8259#section-1
 [php-json-decode]: https://www.php.net/manual/en/function.json-decode.php
 [php-named-parameters]: https://php.watch/versions/8.0/named-parameters

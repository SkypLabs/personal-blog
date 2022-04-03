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
<?php

json_decode(
    string $json,
    ?bool $associative = null,
    int $depth = 512,
    int $flags = 0
): mixed

?>
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
software. Thankfully, PHP gives you tools to distinguish the two outcomes.

<!-- more -->

The fist option is to invoke [`json_last_error()`][php-json-last-error], a
function which "returns the last error (if any) occurred during the last JSON
encoding/decoding". Here is an example taken from [the official
documentation][php-json-last-error]:

```php

<?php
// A valid json string
$json[] = '{"Organization": "PHP Documentation Team"}';

// An invalid json string which will cause an syntax
// error, in this case we used ' instead of " for quotation
$json[] = "{'Organization': 'PHP Documentation Team'}";


foreach ($json as $string) {
    echo 'Decoding: ' . $string;
    json_decode($string);

    switch (json_last_error()) {
        case JSON_ERROR_NONE:
            echo ' - No errors';
        break;
        case JSON_ERROR_DEPTH:
            echo ' - Maximum stack depth exceeded';
        break;
        case JSON_ERROR_STATE_MISMATCH:
            echo ' - Underflow or the modes mismatch';
        break;
        case JSON_ERROR_CTRL_CHAR:
            echo ' - Unexpected control character found';
        break;
        case JSON_ERROR_SYNTAX:
            echo ' - Syntax error, malformed JSON';
        break;
        case JSON_ERROR_UTF8:
            echo ' - Malformed UTF-8 characters, possibly incorrectly encoded';
        break;
        default:
            echo ' - Unknown error';
        break;
    }

    echo PHP_EOL;
}
?>
```

The other option is to set the `JSON_THROW_ON_ERROR` flag when calling the
`json_decode()` function. This flag was added in PHP version 7.3 to throw an
exception upon parsing failure instead of returning the value `null`. This is
the path I decided to follow.

To use this feature, I initially thought that I could write something like
`json_decode($input, flags: JSON_THROW_ON_ERROR)` but it turns out [named
parameters are only available since version 8.0 of PHP][php-named-parameters]
which was not available in the production environment of my client. So it seemed
that I had to go the long way and set the values of all four parameters per the
function prototype. But then I thought: "I'm not a PHP expert so maybe I missed
something and there is actually a more elegant way to write it :thinking:". This
is how I ended up doing some internet searching to finally stumbled on the real
topic of this blog post: a [StackOverflow][stackoverflow] thread having as title
["Multiple Flags for json_encode()"][so-flags-json-encode].

 [json-rfc]: https://datatracker.ietf.org/doc/html/rfc8259#section-1
 [php-json-decode]: https://www.php.net/manual/en/function.json-decode.php
 [php-json-last-error]: https://www.php.net/manual/en/function.json-last-error.php
 [php-named-parameters]: https://php.watch/versions/8.0/named-parameters
 [stackoverflow]: https://stackoverflow.com/
 [so-flags-json-encode]: https://stackoverflow.com/questions/32311103/multiple-flags-for-json-encode

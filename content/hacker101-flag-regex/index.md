+++
title = "Hacker 101 - Capture the Flags with a Regex"
date = 2020-07-07
template = "post.html"

aliases = [
  "/2020/07/07/hacker101-flag-regex/",
]

[taxonomies]
categories = ["Security"]
tags = ["CTF", "ZAP", "Web"]
+++
Enjoying [HackerOne's CTF][h1-ctf]?

If you want to make sure not to inadvertently miss any single flag while
skimming through web pages, you can ask [ZAP][zap] to catch them for you with
this regex: `\^FLAG\^[\w\d]{64}\$FLAG\$`

![ZAP settings to capture Hacker 101 flags
automatically](hacker101_zap_flag_regex_settings.jpg)

A "Flag" tag will appear next the requests containing a flag in their response:

![HTTP request captured with ZAP containing a Hacker 101
flag](hacker101_zap_flag_regex_captured.jpg)

This technique is particularly useful when a flag appears in a non-obvious
location such as an HTML comment.

 [h1-ctf]: https://ctf.hacker101.com
 [zap]: https://zaproxy.org

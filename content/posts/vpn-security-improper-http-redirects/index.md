+++
title = "VPN, Security and Improper HTTP Redirects"
date = 2023-01-28
template = "post.html"

[taxonomies]
categories = ["Essay", "Security", "Web"]
tags = ["Firefox", "TLS", "VPN"]
+++
As you probably have already noticed, the number of VPN providers has grown
massively in the recent years, and you can now stumble on ads for VPN
subscriptions on every corner of the Internet. Of course, not all of these
providers are equal in terms of quality of service, security or privacy. At the
contrary, some of them falsely claim to have a zero-log policy or to even
protect you from malicious actors.

Having said that, using a public VPN service is not necessarily a bad idea if
you choose it correctly. It's a matter of trust after all. Who do you trust the
most for keeping your traffic private, your ISP, or a carefully selected VPN
provider? (I said carefully here because you have a larger number of VPN
providers on the market than ISPs available where you live).

If you trust your VPN provider, you get in theory a higher degree of online
privacy by proxying your connections through it (even if, as of today, nothing
can fully replace [Tor][tor]). But what about security? From a theoretical
standpoint once again, TLS is well enough to guarantee the security of your
online activity. And thanks to projects like [Let's Encrypt][lets-encrypt], most
websites are accessible via HTTPS these days.

<!-- more -->

So, using a VPN doesn't give you a better security? Well, in practice, it's not
that simple, and for one simple reason: there are lots of misconfigured web
servers out there! And it is actually the reason I wanted to write this blog
post. To be more precise, it is [this Twitter
thread](https://twitter.com/SchmiegSophie/status/1489986563677196288) which made
me realise that even experienced information security people can miss this
point:

> "Please stop with your misinformation campaign. VPNs are completely
> unnecessary to protect someone in this scenario, https works just fine."
> [@SchmiegSophie](https://twitter.com/SchmiegSophie)

Sophie is right here, HTTPS works fine, but only when properly configured. As a
matter of fact, I use an online accounting web application called
[Bullet][bullethq] for the needs of [my company][skyplabs]. When I try to log
into my Bullet account, here is what happens:

![Firefox HTTPS-only mode alert page stating that "Secure Site Not Available" on
Bullet's login page.](./bullet-improper-http-redirect.png)

As you can see, I am redirected to an HTTP page, leaking the session cookie
because it is not marked as [`Secure`][mdn-cookies-secure]. I let the company
know about this security issue months ago but to this date, they still haven't
taken any actions to fix it, hence the public disclosure here.

This category of issues is unfortunately quite common. Just the other day, the
same thing happened to me once again on the Help Desk tool of a cloud provider
specialised in Healthcare Data Solutions (HDS). It goes without saying that
impersonating an account used to request actions on production systems is
something not desired... If I were to be connected to a public Wi-Fi while
triggering one of those improper HTTP redirects, a malicious actor on the same
network could have stolen my session token, and indeed, tunnelling my network
traffic using a VPN is a way to prevent it.

Another less costly way to prevent your browser from leaking personal data,
including session cookies, is to turn on the HTTPS-only mode of your web browser
as I did with [Firefox][firefox-https-only]. The result is the one of the above
screenshot: Firefox warns you when plaintext data is about to be sent.

To conclude, the decision to use or not a VPN is yours, and my intention was
solely to help you weight the pros and cons on that matter. If you think a VPN
can fit your needs, I recommend [Mullvad VPN][mullvad] (this is my personal
opinion, not a sponsor) for the following main reasons: EU-based company,
[diskless infrastructure][mullvad-diskless], [post-quantum
cryptography][mullvad-post-quantum], open-source software without trackers (and
written in Rust!), [supporting open-source projects such as Qubes
OS][mullvad-donate-qubesos], and [transparent security audit
reports][mullvad-security-audit].

 [bullethq]: https://www.bullethq.com/ "Bullet HQ"
 [firefox-https-only]: https://support.mozilla.org/en-US/kb/https-only-prefs "Firefox HTTPS-only mode"
 [lets-encrypt]: https://letsencrypt.org/ "Let's Encrypt"
 [mdn-cookies-secure]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#restrict_access_to_cookies "MDN - Restrict access to cookies"
 [mullvad]: https://mullvad.net/ "Mullvad VPN"
 [mullvad-diskless]: https://www.mullvad.net/en/blog/2022/8/1/expanding-diskless-infrastructure-to-more-locations-system-transparency-stboot/ "Mullvad VPN's diskless infrastructure"
 [mullvad-donate-qubesos]: https://www.mullvad.net/en/blog/2022/6/15/mullvad-is-now-continuously-donating-to-qubes-os/ "Mullvad VPN continously donating to Qubes OS"
 [mullvad-post-quantum]: https://www.mullvad.net/en/blog/2022/11/8/post-quantum-safe-vpn-tunnels-available-on-all-wireguard-servers/ "Mullvad VPN's post-quantum cryptography"
 [mullvad-security-audit]: https://www.mullvad.net/en/blog/2022/10/21/security-audit-report-for-our-app-available/ "Mullvad VPN's latest security audit of their apps"
 [skyplabs]: https://skyplabs.com "SkypLabs"
 [tor]: https://www.torproject.org/ "The Tor project"

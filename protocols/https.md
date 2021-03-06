# HTTPs

## HTTPS Protocol

HTTPS \(HTTP Secure\) is a secure communication protocol obtained by layering the HTTP protocol on top of the SSL/TSL protocol.

Protocol name in Jolie port definition: `https`.

## HTTPS Parameters

Since HTTPS is the HTTP protocol wrapped in an SSL encrypted message, HTTPS parameters are the same defined for [HTTP](https://github.com/jolielang/docs/tree/de0bcc5b82206ed6be6cb78fa10f6068bbe5881c/documentation/protocols/http.html) and [SSL](https://github.com/jolielang/docs/tree/de0bcc5b82206ed6be6cb78fa10f6068bbe5881c/documentation/protocols/ssl.html).

## HTTPS with HTTP Compression

Unfortunately there exist some known HTTPS attacks with enabled HTTP compression like [BREACH](http://en.wikipedia.org/wiki/BREACH). Hence you might want to set the `compression` parameter to `false` when you are handling sensitive data.


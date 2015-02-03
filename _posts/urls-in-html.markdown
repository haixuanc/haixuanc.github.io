---
layout: post
title:  "URLs in HTML"
date:   2015-01-29 20:00:00
categories:
- HTTP, HTML
---

## Absolute vs Relative URLs

``` html
// Relative URL
<img src="/images/suprise.png">
// Absolute URL
<img src="http://my-site.com/images/suprise.png">
```

If you want to reference a **local** resource on your server, always use relative URL over absolute URL:
1. relative URLs will be correctly resolved to absolute URLs;
2. absolute URLs are like hardcoding which makes it cumbersome if you were to migrate your server to a different domain (e.g. change of URL/protocol/port).

## Resolutions of Relative URL

Suppose your server lives in the `/var/www/my-site` directory of the host machine.

### Local Resource

#### Type 1
``` html
/images/surprise.png
```
resolves to
``` html
/var/www/my-site/images/surprise.png
```

#### Type 2
```html
images/surprise.png
```
resolves to
``` html
/var/www/my-site/path-to/page-that/I-am-currently-browsing/images/surprise.png
```

### Scheme-less URLs

``` html
//external-site.com/images/surprisepng
```
resolves to
``` html
http/https://external-site.com/images/surprisepng
```
depending on the scheme used by the server who is serving the containing webpage.

Scheme-less URLs can avoid the attempts of sending request over HTTP while the containing webpage is being served over HTTPS.

## References

[Absolute vs relative URLs, StackOverflow](http://stackoverflow.com/questions/2005079/absolute-vs-relative-urls)

---
layout: post
title:  "ETags"
date:   2015-01-7 20:00
categories:
- HTTP
---

## Overview

The **ETag** or **entity tag** is a HTTP header. It is one of the several mechanisms that HTTP provides for web cache validation, and which allows a client to make conditional requests. With it a web server does not need to send a full response if the content has not changed.

## Definition

* An ETag is an opaque identifier assigned by a web server to a specific version of a resource found at a URL. if the resource content at that URL ever changes, a new and different ETag is assigned. Used in this manner ETags can be compared to determine if two version of a resource are the same. Comparing ETags only makes sense with respect to one URL - ETags for the same resource obtained from different URLs may or may not be equal.
* ETags are cached by the browser, and returned with subsequent requests for the same resource.

## ETag vs Expires

ETag header is meant to be used by **server**. When a server reads the ETag header of a request from a client, the server can use it to determine if the resource content has changed. If changed, the server can send back the new resource (**HTTP 200**). If not changed, the server can tell the client to use its local copy (**HTTP 304**).

**Expires** header is meant to be used by **client** (including proxies and caches). **Expires** header of a response is firstly set by server, which tells when the resource will expire. Client can use it to determine whether it should send another request if caching is used.

Etag and Expires can be used together to provide an efficient caching mechanism.

## ETags with load-balanced server

If you are using a load-balanced server setup with multiple machines running Apache, you should probably turn off ETag generation. Etag generation algorithm is based on **inode** and **timestamp** which are likely to be different across different machines. You can configure Apache to not use inodes as part of Etag generation, but then you also need to make sure the timestamps on the files are exactly the same.

## References

1. [HTTP Etags, Wikipedia](http://en.wikipedia.org/wiki/HTTP_ETag)
2. [ETag vs Header Expires, Stackoverflow](http://stackoverflow.com/questions/499966/etag-vs-header-expires)


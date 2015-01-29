---
layout: post
title:  "HTTP Forms"
date:   2015-01-29 20:00:00
categories:
- HTTP, HTML
---

## A Basic Form

```html
<form action="/somewhere_on_my_server" method="GET">...</form>
```

A form without `action` attribute will cause browser to send requests to the current page containing the form.

## Methods

While HTTP provides a rich set of methods to perform requests, HTML forms only support `GET` and `POST` requests.

### GET Method

The `GET` method is used by the browser to ask the server to send back a given resource:
1. browser encodes form data into **query string** and appends it to the `action` URL;
2. the request body is **empty**.

Don't use `GET` method to send any sensitive information e.g. username and password, because these form data will be encoded as part of the URL which is visible to the network.

### POST Method
 
The `POST` method is used by the browser to ask the server for a response that takes into account the data provided in the request body:
1. browser saves form data in request body;
2. browser sets `Content-Type` and `Content-Length` properties of the request. Server will use them to decode the request body to get back the original form data. 

### Sending Files

HTTP is a **text** protocol, while files are usually considered **binary data** e.g. images and videos. To properly send files, you need to set the `enctype` attribute of a form: 

``` html
<form action="/somewhere" method="post" enctype="multipart-form-data">
	<input type="file" name="some-file">
	...
</form>
```

#### Enctype Attribute

By default, a form sets its `enctype` attribute to `application/x-www-form-urlencoded` which means: *"This is form data that has been encoded into URL form."*

Setting `enctype` attribute to `multipart-form-data` tells browser that the data will be split into multiple parts, one for each file plus one for the text inputs of the form.
 
## References

[Sending and retrieving form data, MDN](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Forms/Sending_and_retrieving_form_data)

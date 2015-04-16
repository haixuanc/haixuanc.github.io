---
layout: post
comments: true
title:  "Post/Redirect/Get Pattern"
date:   2015-01-17 20:00:00
categories:
- HTTP
---

When user refreshes a webpage the browser will attempt to resend the last HTTP request. The browser may display a obscure warning that asks for confirmation before submitting that request again. If user chooses yes and the last one is a `POST` request caused by a form submission, a duplicated action will be triggered on the server.

To solve this problem, the server can always respond a successful `POST` request with a `REDIRECT` response. When the browser receives the `REDIRECT` response it will issue another `GET` request. So the last request sent is `GET` which won't cause any problem if user refreshes the webpage and the browser resends a `GET` request for the same URL.

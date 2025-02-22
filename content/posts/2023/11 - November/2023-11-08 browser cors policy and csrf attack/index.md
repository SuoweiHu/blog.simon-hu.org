---
title: "Browser CORS policy"
date: 2023-11-08
tags: ["Network"]
tags: ["#Other"]
---

## Intuition

**To begin with we need to answer a simple question, why do we need to block traffic from one site to another site, and have everything controlled in this CORS policy ?**

> Imagine there's two site, site A is a legitimate banking website that provides online finance services, site B is a phishing website that tries to spoof the website A. As a developer you might be aware of API's, and the legitimate banking website is using exactly that to transfer money from account to account, for instance: "`https://bank-site-a.com/api?from=account1&to=account2`". If without any security policy, the phishing site B can copy this exact link and place it on some easily found buttons or links, and once a user (with logged in bank account) clicks on these buttons or links, the transaction will be triggered without the user's permission.

> Such attack forces authenticated users to submit a request to a Web application against which they are currently authenticated, is called **Cross-Site Request Forgery (CSRF)**.

![2023.11.08 - 173520](2023.11.08%20-%20173520.jpg)


**And the CORS (Cross-Origin Resource Sharing) policy is here to prevent this ! It will allow controlled access to resources from different origins/domain names in web browsers, ensuring security and protecting against cross-site scripting attacks.**

---

## Example

### CORS Request Type ?

The CORS request will be preflighted (preflight request sent) in the following cases:
```
- Non-simple request methods:    If the request method is other than GET, POST, or HEAD, a preflight request is sent.
- Custom request headers:        If the request includes custom headers (apart from a few allowed headers like `Accept`, `Accept-Language`, `Content-Language`, `Content-Type`, etc.), a preflight request is sent.
- Content-Type header:           If the ﻿Content-Type header value is outside the allowed values for simple requests, a preflight request is sent.
```
For **all other cases**, the request is considered a simple request, and no preflight request is needed

### CORS Simple Request

Suppose a user visits `http://www.example.com` and the page attempts a cross-origin request to fetch data from `http://service.example.com`. A CORS-compatible browser will attempt to make a cross-origin request to service.example.com as follows.
1. The browser ends request with Origin header to `service.example.com`:
   ```
   Origin: http://www.example.com
   ```
2. The server at `service.example.com` sends one of these three responses:
    ```
    A) wild-card:     Access-Control-Allow-Origin: *
    B) with-origin:   Access-Control-Allow-Origin: http://www.example.com
    C) disallow:      Access-Control-Allow-Origin: none
    ```

### CORS Preflight Request

When performing certain types of cross-domain Ajax requests, modern browsers that support CORS will initiate an extra "**preflight**" request to determine whether they have permission to perform the action. Cross-origin requests are preflighted this way because they may have implications to user data.
```
OPTIONS /
Host:                          service.example.com
Origin:                        http://www.example.com
Access-Control-Request-Method: PUT
```

If service.example.com is willing to accept the action, it may respond with the following headers:
```
Access-Control-Allow-Origin:   http://www.example.com
Access-Control-Allow-Methods:  PUT
```
The browser will then make the actual request. If `service.example.com` does not accept cross-site requests from this origin then it will respond with error to the OPTIONS request and the browser will not make the actual request.


---

## Resolving Cross-Origin Issue

From time to time we will have to face the condition where we need to access some portion of the site from another site (for instance: reading font-face or script, fetching data using ajax), and in that scenario, we will need to bypass the Cross-Origin constraint by CORS policy. And we can resolve this via two methods: making the two sites under the same domain (using reverse proxy like apache or nginx), or add the parent site (origin) into the access-allow-origin header of the child site (target).

### Method-1: Reverse Proxy

The first method involves using a **reverse proxy router**, mapping two sites of the different domain to a different URI of the same domain. For instance we can map "`www.proxy.com/site-1`" to "`www.example.com`", "`www.proxy.com/site-2`" to "`www.services.com`", and replace the original URL (in the "`www.example.com`") from "`www.services.com`" to "w`ww.proxy.com/site-2"`. Then from the point-of-view of the browser, they are now **under the same domain** hence will not trigger the CORS policy.

![2023.11.08 - 173649](2023.11.08%20-%20173649.jpg)


### Method-2: Add Origin Header

The second method involves making **modification at the service** (side of server), in order for the browser to permit CORS access, the receiver will need to have origin's origin in the "access-allow-origin" header; For instance, "`www.example.com`" initiates the request with header "`origin:www.example.com`" to server "`www.service.com`", we will need to put header "`access-allow-origin:www.example.com`" for every relating request response from "`www.service.com`".



![2023.11.08 - 174442](2023.11.08%20-%20174442.png)



---

> Reference-1: [Wikipedia - Cross-origin resource sharing](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing)
> Reference-2: [Bilibili - 底搞懂CORS（跨域资源共享 ](https://www.bilibili.com/video/BV13z4y1F717)

---
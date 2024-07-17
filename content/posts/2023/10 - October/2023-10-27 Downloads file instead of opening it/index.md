---
title: "Websites downloads the PHP-File instead of opening the website"
date: 2023-10-31
tags: ["Drupal Bug Fix"]
---

This tutorial provides step-by-step instructions to address the strange problem where, upon accessing a website, the index.php file begins to **download** instead of **opening** as intended. Users may encounter a dialog box prompting them to download the file, unsure of how to proceed when faced with options to open, close, or cancel. This article aims to guide you in resolving this issue effectively.

## 	Solution 1: Rebooting your web development environment

Sometimes it will be a easy fix like **rebooting** your development environment / software, for my instance I am using MAMP, and by stopping the server and opening it again, solved 99% of my issues



## Solution 2: Get a fresh instance of the .htaccess file

Sometimes this issue is caused by the `.htacecss` file. To resolve this, you can download a fresh instance of the drupal from its [official website](https://www.drupal.org/download), and use its `.htaccess`  file to override the existing one. 

After you do that you might want to: 

1.   restart your MAMP server 
2.   change your website's name (such that their URL differs from the previous one) to prevent caching issue
3.   check your website in different browsers (for instance chrome + firefox + arc + brave + safari)




## Solution 3: Move MIME type "application/x-httpd-php" to highest priority

In file `MimeTypes.php`, move the `application/x-httpd-php` to the very bottom of the page, this will ensure your php handler is put on the highest priority.

The purpose of the MIME type "application/x-httpd-php" is to indicate that a file being served by a web server is a PHP script. MIME types are used to identify the nature and format of a file so that the browser or other client software can handle it appropriately. In the case of "application/x-httpd-php," it tells the browser that the file should be processed by the server as a PHP script rather than being displayed directly to the user. This MIME type is crucial in ensuring that the PHP script is executed correctly on the server side before the resulting HTML or other output is sent to the browser for rendering.

This is proposed by “franck22” at drupal community post: https://www.drupal.org/forum/support/post-installation/2004-05-14/indexphp-starts-to-download-instead-of-opening


```diff
- ---------------------------before changes
- ...
-   private const MAP = [
-        ....
-        ....
-        'application/x-httpd-php' => ['php'],
-        ....
-        ....
-   ]
- ...
-
+ ---------------------------after changes
+ ...
+   private const MAP = [
+        ....
+        ....
+        ....
+        ....
+        'application/x-httpd-php' => ['php'],
+   ]
+ ...
```

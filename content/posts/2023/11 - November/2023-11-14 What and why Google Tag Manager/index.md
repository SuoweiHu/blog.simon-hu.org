---
title: "What/Why Google Tag Manager (GTM)"
date: "2023-11-14"
tags: ["#Other"]
---



## Intuition

To begin with, I looked for the definition of "tag" in the Google Tag Manager's context, according to their [official documentation](https://support.google.com/tagmanager/answer/3281060), they refer tags as "segments of code provided by analytics, marketing, and support vendors to help you integrate their product into your website or mobile apps", so bascially you can think of tag like a chunk of script for third party plug-in (like for example: HotJar (a digital expereience insight and behavior analytics tool))

![image-20231114142828720](image-20231114142828720.png)

So why would you want to include Google Tag Manager (GTM) to help you control these "tag(s)", isn't it easier to just have these "tag(s)" writting into the `.html` file ? (or `.twig` template in the Drupal world); This is of course, because there's benifits from using Google Tag Manager:
- **Consolidation**: the Google Tag Manager allows a centered single place to control to tags, and have different rule-based triggers that allows fire of different tags on different scenarios (for instance different tags on mobile and desktop)
- **Speed**: unlike having all tags in the html documentation, the Goggle Tag Manager will loads multiple tags asynchronously, hence improve page load times
- **Workflow **: it is earlier to add/modify tags once setup, you wont have to repeat the process of "loggin into server → change code → clear cache → wait for client side cache to expire". Further more it allows collaboration between multiple teams, for instance two teams can work on "google analytics tags" and another working on "google ads tags" without conflicts.

![image-20231114142923126](image-20231114142923126.png)

For more details, you can refer to official documentation: [Tag Manager Overview](https://support.google.com/tagmanager/answer/6102821?hl=en)



## Basic Setup

Let's say there's this scenario where one wanna setup  `<script type="application/ld+json">` in a normal HTML file; (The purpose of `﻿<script type="application/ld+json">` is to embed structured data in JSON format within an HTML page. This data is used to provide additional context and information about the content on the page, helping search engines and other applications better understand and interpret the content. It is commonly used for implementing schema.org markup to enhance search engine optimization and improve the visibility of web pages in search results.)

**First**, create a GTM account.
**Second**, you will need to following the guide, and add the `<script>` code provided by GTM: ([ScreenShot](image-20231114143023149.png))

- Add the following to the `<head>`of the page (as high of the code as possible)
  ```html
  <!-- Google Tag Manager -->
  <script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':
  new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],
  j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src=
  'https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);
  })(window,document,'script','dataLayer','GTM-W92NBFNR');</script>
  <!-- End Google Tag Manager -->
  ```

- Add the following imeediately after the opening `<body>` tag



  ```html
  <!-- Google Tag Manager (noscript) -->
  <noscript><iframe src="https://www.googletagmanager.com/ns.html?id=GTM-W92NBFNR"
  height="0" width="0" style="display:none;visibility:hidden"></iframe></noscript>
  <!-- End Google Tag Manager (noscript) -->
  ```

-   Test the website using the GTM's built in tool

**Third**, proceed to the left bar, choose "tag" and then "create a tag", here we will put `<script type="application/ld+json">` and trigger it on every page (trigger basically means the condition it will get rendered)

![2023.11.14 - 143234](2023.11.14%20-%20143234.png)

**Lastly**, see it take effect...

![2023.11.14 - 144832](2023.11.14%20-%20144832.jpg)

You may also test it via https://validator.schema.org/

![2023.11.14 - 151904](2023.11.14%20-%20151904.jpg)




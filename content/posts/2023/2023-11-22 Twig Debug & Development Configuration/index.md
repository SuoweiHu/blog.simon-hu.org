---
title: "Twig - Debug/Development Environment - Setting Configuration"
date: "2023-11-22"
categories: ["twig"]
---

## Enable Twig Debug (Show source file)

In order to have the output such as:
```html
<!-- THEME DEBUG -->
<!-- THEME HOOK: 'paragraph' -->
<!-- FILE NAME SUGGESTIONS:
   * paragraph--accordion-single--default.html.twig
   x paragraph--accordion-single.html.twig
   * paragraph--default.html.twig
   * paragraph.html.twig
-->
<!-- BEGIN OUTPUT from 'themes/custom/XXXX/templates/paragraph/paragraph--accordion-single.html.twig' -->
```
printing in the terminal (this is good to help identifying the **source of twig template file** current node is rendering from).

You will need to put the following in the `services.yml` (if not exits, then copy `default.services.yml` to `services.yml`)
```yml
parameters:
  twig.config:
    debug: true
```

## Enable Auto-Reload Configuration

Twig templates are compiled to PHP classes on disk for improved performance. However, this means that by default, your templates are not automatically updated when you make changes. It is not advisable to enable this feature in a production environment. (To manually rebuild the templates run `drush cr`).

To save time during development, you can enable automatic reloading by put the following in `services.yml`:
```yml
parameters:
    twig.config:
        auto_reload: true
```
(by default, auto reloading will turned on with twig.config.debug: true)
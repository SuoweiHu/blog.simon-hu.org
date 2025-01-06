---
title: "Fixing module not getting recognized (after D9-10 upgrade)"
summary: "Quick fix to the issue of module not getting recognized after upgrading from drupal-9 to drupal-10"
tags: ["Drupal", "Patch"]
date: 2023-11-01
---

(This one is very similar to where I fix the issue of theme not getting recognized, so if you have checked that one out, the procedure is the same, you will just have to uninstall the manually installed module, and use composer to install module instead)

During the course of the upgrade, it is found that after the upgrade drupal 10 consistently fails to recognize bootstrap theme, resulting in a site with plain html and css, this post will help you resolve this issue.

**Step-1: Install using composer**

To begin with you will need to install the module using composer, this will place your module inside the `$drupal-root/module/contrib` folder, for instance run `composer require 'drupal/XXXX:^3.29'` will download the drupal bootstrap 3.29 module and place it in folder `$drupal-root/module/contrib/XXXX`.

**Step-2: Remove original module**

Then you will need to remove the original folder located at the `$drupal-root/module` for this instance, the original bootstrap base module is located at `$drupal-root/module/XXXX`, you will need to remove it.

**Step-3: Clear Cache**

Lastly, we will need to let drupal correctly identify the location of the new composer installed module, simply clear the cache using the admin panel or run `drush cr` in terminal.


---
title: "Fixing bootstrap theme not getting recognized (after D9-10 upgrade)"
summary: "Quick fix to the issue of theme not getting recognized after upgrading from drupal-9 to drupal-10"
tags: ["Drupal", "Patch"]
date: 2023-10-31
---

During the course of the upgrade, it is found that after the upgrade drupal 10 consistently fails to recognize bootstrap theme, resulting in a site with plain html and css, this post will help you resolve this issue.

**Step-1: Install using composer**

To begin with you will need to install the theme using composer, this will place your theme inside the `$drupal-root/theme/contrib` folder, for instance run `composer require 'drupal/bootstrap:^3.29'` will download the drupal bootstrap 3.29 theme and place it in folder `$drupal-root/theme/contrib/bootstrap`.

**Step-2: Remove original theme**

Then you will need to remove the original folder located at the `$drupal-root/theme` for this instance, the original bootstrap base theme is located at `$drupal-root/theme/bootstrap`, you will need to remove it.

**Step-3: Clear Cache**

Lastly, we will need to let drupal correctly identify the location of the new composer installed theme, simply clear the cache using the admin panel or run `drush cr` in terminal.


---
title: "[Bug Fix] Composer Unpin Drupal Core From Certain Version"
date: "2024-07-24"
tags: ["Drupal", "Patch"]
---


## \#Unpinning from a specific version of core

If you are running a pinned version of Drupal core, and want to update your site to another version, you have two choices.

You can run the composer require command above to specify a new, pinned version of core.
You can unpin your core version, and update to the latest version of Drupal.
To unpin your version of Drupal, run this command:
```
composer require drupal/core-recommended drupal/core-composer-scaffold drupal/core-project-message --update-with-all-dependencies

```




## Reference

- https://www.drupal.org/docs/updating-drupal/updating-drupal-core-via-composer#s-unpinning-from-a-specific-version-of-core
- https://www.drupal.org/forum/support/upgrading-drupal/2024-06-04/how-to-un-pin-my-version-of-drupalcore
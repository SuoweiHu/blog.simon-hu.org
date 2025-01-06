---
title: "Deprecation of \"path/filename\" api (after D9-10 upgrade)"
summary: "Fixing custom modules' code that are dependent of function drupal_get_path() and drupal_get_filename() which is deprecating in newest drupal 10, hence making it compatible for the upgrade (only for temporal purpose). "
tags: ["Drupal", "Patch"]
date: 2023-10-31
---

**Handle for deprecated function `drupal_get_path()`**

```diff
# Node
- drupal_get_path('module', 'node')
+ \Drupal::service('extension.list.module')->getPath('node')

# Node (Alternative)
- drupal_get_path('module', 'node')
+ \Drupal::service('extension.path.resolver')->getPath('module', 'node')

# Theme
- drupal_get_path('theme', 'seven')
+ \Drupal::service('extension.list.theme')->getPath('seven')

# Standard
- drupal_get_path('profile', 'standard')
+ \Drupal::service('extension.list.profile')->getPath('standard')
```


**Handle for deprecated function `drupal_get_filename()`**

```diff
# Node
- drupal_get_filename('module', 'node')
+ \Drupal::service('extension.list.module')->getPathname('node')

# Node (alternative)
- drupal_get_filename('module', 'node')
+ \Drupal::service('extension.path.resolver')->getPathname('module', 'node')

# Theme
- drupal_get_filename('theme', 'seven')
+ \Drupal::service('extension.list.theme')->getPathname('seven')

# Standard
- drupal_get_filename('profile', 'standard')
+ \Drupal::service('extension.list.profile')->getPathname('standard')
```

---

**Reference Material:**

-   https://www.drupal.org/node/2940438
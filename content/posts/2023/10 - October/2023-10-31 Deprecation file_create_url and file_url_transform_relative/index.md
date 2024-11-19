---
title: "Deprecation of \"url\" api"
summary: "Fixing custom modules' code that are dependent of function file_create_url() and file_url_transform_relative() which is deprecating in newest drupal 10, hence making it compatible for the upgrade (only for temporal purpose). "
tags: ["Drupal"]
tags: ["D9 - D10 Upgrade"]
date: 2023-10-31
---


**Handle for deprecated function `“file_create_url()` and `“file_url_transform_relative()`**

```diff
- file_create_url($uri)
+ \Drupal::service('file_url_generator')->generateAbsoluteString($uri)

- file_url_transform_relative($file_url)
+ \Drupal::service('file_url_generator')->transformRelative($file_url)

- file_url_transform_relative(file_create_url($uri)
+ \Drupal::service('file_url_generator')->generateString($uri)

- Drupal\Core\Url::fromUri(file_create_url($uri))
+ \Drupal::service('file_url_generator')->generate($uri)
```



---

**Reference Material:**

-   https://www.drupal.org/node/2940031
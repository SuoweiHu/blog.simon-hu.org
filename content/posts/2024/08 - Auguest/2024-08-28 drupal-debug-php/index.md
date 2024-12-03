---
title: "Drupal Debug PHP File"
date: "2024-08-28"
tags: ["Drupal", "Debug"]
---


## Method-1: PHP (print_r / var_dump / var_export)
You may use a combination of the `print_r()`, `var_dump()`, `var_export()`, and always end with `die()` to break the logic flow, such that the function hault on your debug code and print out:
``` php
  print_r    ("HELLO WIRLD from PRINT_R");
  dump       ("HELLO WORLD from DUMP");
  var_export ("HELLO WORLD from VAR_EXPORT");
  var_dump   ("HELLO WORLD from VAR_DUMP");
  die();
```

For instance you can have the following code to debug print in `custom_theme_name.theme` file:
```php
//
function custom_theme_name_preprocess_html(&$variables) {
    // Get the current path and node id
    $current_path = \Drupal::service('path.current')->getPath();
    $internal_path = \Drupal::service('path_alias.manager')->getAliasByPath($current_path);
    $website_base_url= \Drupal::request()->getSchemeAndHttpHost();
    $node = \Drupal::routeMatch()->getParameter('node');
    if ($node instanceof \Drupal\node\NodeInterface) {$nid = $node->id();}

    // Debug printing the variables retrived above
    print_r($nid);                   // [DEBUG]: NODE ID
    print_r($current_path);          // [DEBUG]: PATH
    print_r($website_base_url);      // [DEBUG]: WEBSITE BASE URL
    dump($var_array);                // [DEBUG]: HEAD ATTRIBUTE
    die();                           // [DEBUG]: KILL PHP WHEN DONE

    // ===================
    // YOUR CODE CONTINUED
    // ▼▼▼▼▼▼▼▼▼▼▼▼▼▼▼▼▼▼▼
}
```

## Method-2: Drupal (via watchdog module / logger service)

Please refer to reference, not recommended as the debug log will eventually be a part of database of website.


## Method-3: XDebug (Debug using IDE)

Please refer to reference, very tricky to setup, but can become useful when you are facing complicated scenarios.



## Reference
- https://www.specbee.com/blogs/php-debugging-how-debug-your-php-code-drupal-debugging-techniques-included
- https://api.drupal.org/api/drupal/core%21includes%21common.inc/function/debug/8.9.x
---
title: "Drupal Settings.php Snippets for Debug"
date: "2024-11-20"
tags: ["Drupal", "Debug"]
---



## Usage (TLDR;)

You can simply copy  `<CTRL-C>` + `<CTRL-V>`  the following into your `public_html/site/default/settings.php`, and toggle on/off those that are relevant to you based on your need:
```php
$config['system.logging']['error_level'] = 'verbose';                        // [A] (For Drupal 8+) Turn on verbose debug message reporting
//$conf['error_level'] = 2;                                                  // [A] (For Drupal 7)  Turn on verbose debug message reporting (Equivalant to navigate to Administration→ Configuration→ Development → logging and errors and select "All messages".)
																			 // [A] -------------------------------------------
error_reporting(E_ALL);													     // [A] Enable PHP errors (For local Drupal development, you can also enable error reporting, display errors and display startup error to help you further debugging and fixing major runtime errors
ini_set('display_errors', TRUE);                                             // [A] Enable PHP errors (For local Drupal development, you can also enable error reporting, display errors and display startup error to help you further debugging and fixing major runtime errors
ini_set('display_startup_errors', TRUE);                                     // [A] Enable PHP errors (For local Drupal development, you can also enable error reporting, display errors and display startup error to help you further debugging and fixing major runtime errors

$settings['twig_debug'] = TRUE;                                              // [B] Twig Debug       - Turn on  twig debug mode
$settings['twig_auto_reload'] = TRUE;                                        // [B] Twig Debug       - Turn on  twig template auto reload
$settings['twig_cache'] = FALSE;                                             // [B] Twig Debug       - Turn off twig cache 
																			 // [B] ------------------------------------------
$settings[‘cache’][‘bins’][‘render’] = ‘cache.backend.null’;                 // [B] Disable Caching  - Disable render caching.
$settings[‘cache’][‘bins’][‘page’] = ‘cache.backend.null’;                   // [B] Disable Caching  - Disable page cache.
$settings[‘cache’][‘bins’][‘dynamic_page_cache’] = ‘cache.backend.null’;     // [B] Disable Caching  - Disable dynamic page cache.
$settings[‘cache’][‘default’] = ‘cache.backend.null’;                        // [B] Disable Caching  - Disable backend cache.
																				
$config['system.performance']['css']['preprocess'] = FALSE;                  // [C] Turn off agrregated css      (see: https://www.drupal.org/docs/develop/development-tools/disabling-and-debugging-caching)
$config['system.performance']['js']['preprocess'] = FALSE;                   // [C] Turn off agrregated js       (see: https://www.drupal.org/docs/develop/development-tools/disabling-and

$settings['update_free_access'] = FALSE;                                     // [D] Enable access to /update.php
$settings['rebuild_access'] = TRUE;                                          // [D] Enable access to /rebuild.php                    (This setting can be enabled to allow Drupal's php and database cached storage to be cleared via the rebuild.php page. Access to this page can also be gained by generating a query string from rebuild_token_calculator.sh and using these parameters in a request to rebuild.php.

$settings['skip_permissions_hardening'] = TRUE;                              // [E] Skip file system permissions hardening.          (The system module will periodically check the permissions of your site's site directory to ensure that it is not writable by the website user. For sites that are managed with a version control system, this can cause problems when files in that directory such as settings.php are updated, because the user pulling in the changes won't have permissions to modify files in the directory.
$settings['extension_discovery_scan_tests'] = TRUE;                          // [E] Allow test modules and themes to be installed.   (Drupal ignores test modules and themes by default for performance reasons. During development it can be useful to install test extensions for debugging purpose.                 
$settings['trusted_host_patterns'] = array();                                // [E] Turn off trusted host
```

(for instance `verbose debug` required then turn comment all lines except for `$config['system.logging']['error_level'] = 'verbose';`)



## Line-by-line Explaination 

### Debug Logging 

Sometimes, you can face an unexpected error in a Drupal website, for example during installation, development or updating:

```
The website encountered an unexpected error. Please try again later.
```

You can enable backtracing of the error, and display of more information in the message area, via the GUI or by adding a single line in a settings file. You can do this via the drupal GUI backend via navigate to `Administration > Configuration > Development Logging and errors > Error messages` to display and select the level of **Error messages to display** (config variable names added for reference):

-   None - `hide`
-   Errors and warnings - `some`
-   All messages - `all`
-   All messages, with backtrace information - `verbose`

Or alternatively you can add the following line to the `settings.php` to enable this feature. For local Drupal development, you can also enable error reporting, display errors and display startup error to help you further debugging and fixing major runtime errors. 

```php
$config['system.logging']['error_level'] = 'verbose';                        // [A] (For Drupal 8+) Turn on verbose debug message reporting
//$conf['error_level'] = 2;                                                  // [A] (For Drupal 7)  Turn on verbose debug message reporting (Equivalant to navigate to Administration→ Configuration→ Development → logging and errors and select "All messages".)
                                                                             // [A] ---------------------------------------
error_reporting(E_ALL);													     // [A] Enable PHP errors (For local Drupal development, you can also enable error reporting, display errors and display startup error to help you further debugging and fixing major runtime errors
ini_set('display_errors', TRUE);                                             // [A] Enable PHP errors (For local Drupal development, you can also enable error reporting, display errors and display startup error to help you further debugging and fixing major runtime errors
ini_set('display_startup_errors', TRUE);                                     // [A] Enable PHP errors (For local Drupal development, you can also enable error reporting, display errors and display startup error to help you further debugging and fixing major runtime errors
```



### Development Settings (Twig + Caching)

Disabling caching (render cache, dynamic page cache, Twig cache) during development is useful for seeing changes without clearing the cache. Within Drupal 10.1.0 and later, there is a new "Development settings" page at `/admin/config/development/settings` that contains Twig development settings, as well as the ability to disable various caches. (see screenshot: [link](2024-11-20T103955.png))

The settings available are

-   **Twig development mode**: This checkbox exposes two Twig development checkboxes and checks them by default.
    -   **Twig debug mode** - This enables Twig debug, which provides the `dump()` function, outputs template suggestions to HTML comments, and will also enables Twig auto-reload, which tells Twig to reload any templates that have been modified by the developer.
    -   **Disable Twig cache** - This completely disables the Twig cache.
-   **Do not cache markup** - This disables the render cache, dynamic page cache, and page cache.

You can also do that via adding the following in your `settings.php` without logging into the drupal backend:

```php
$settings['twig_debug'] = TRUE;                                              // [B] Twig Debug  - Turn on  twig debug mode
$settings['twig_auto_reload'] = TRUE;                                        // [B] Twig Debug  - Turn on  twig template auto reload
$settings['twig_cache'] = FALSE;                                             // [B] Twig Debug  - Turn off twig cache 
																		     // [B] ------------------------------------------
$settings[‘cache’][‘bins’][‘render’] = ‘cache.backend.null’;                 // [B] Disable Caching  - Disable render caching.
$settings[‘cache’][‘bins’][‘page’] = ‘cache.backend.null’;                   // [B] Disable Caching  - Disable page cache.
$settings[‘cache’][‘bins’][‘dynamic_page_cache’] = ‘cache.backend.null’;     // [B] Disable Caching  - Disable dynamic page cache.
$settings[‘cache’][‘default’] = ‘cache.backend.null’;                        // [B] Disable Caching  - Disable backend cache.
```



### Aggregated CSS & JavaScript 

In Drupal, "Aggregate CSS and JavaScript" refers to a performance optimization feature that **combines multiple CSS and JavaScript files into single files** (and perform minification to reduce the file-size via removing unused code and pruning whitespaces), respectively. This process is part of Drupal's caching and performance management system and is designed to reduce the number of HTTP requests made by a browser when loading a page, thereby improving page load times. 

You can turn this feature off during development to see the raw form of CSS and JavaScript scipts gettings used via going to `Configuration > Development > Performance` and turn off options under `Bandwidth optimization `(see screenshot: [link](2024-11-20T103704.png)), putting the following line in `setttings.php`: 

```php
$config['system.performance']['css']['preprocess'] = FALSE; // [C] Turn off agrregated css                          (see: https://www.drupal.org/docs/develop/development-tools/disabling-and-debugging-caching)
$config['system.performance']['js']['preprocess'] = FALSE;  // [C] Turn off agrregated js   
```





## Reference 

-   https://www.drupal.org/docs/develop/development-tools/disabling-and-debugging-caching
-   https://www.drupal.org/docs/develop/development-tools/enable-verbose-error-logging-for-better-backtracing-and-debugging

-   https://drupal.stackexchange.com/questions/310970/enable-error-logging-from-settings-php

-   https://www.drupal.org/docs/7/creating-custom-modules/show-all-errors-while-developing

    

    

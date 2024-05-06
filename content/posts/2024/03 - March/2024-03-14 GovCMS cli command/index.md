---
title: "GovCMS Drupal CLI Command (Drush Command) - Backup"
date: "2024-03-14"
categories: ["Drupal", "GovCMS"]
---


Logging in without username / password
```
ahoy drush uinf --uid=1        # Getting the first user created in the db
ahoy drush uublk [user-name*]  # Unblock that user’s name (overwrite name)
ahoy login                     # The generic drush login thing 
```


Enabling / Disable two-factor-authenticator module
```
drush config-set tfa.settings enabled 0
drush config-set tfa.settings enabled 1
```


Importing database to WHM / VPS server
```
mysql –username=[USERNAME] –password [DBNAME] < [FILE_REALPATH]
# (Then enter password for user USERNAME)
```


Composer Package Manager
```
composer require “[PKG_NAME]   : [VER_NAME]”  # Composer install (version 1)
composer require “[PKG_NAME]” “[VER_NAME]”    # Composer install (version 2)
composer info drupal/captcha                  # List package version & dependencies
composer clear-cache                          # Clear composer cache 
composer update PKG_NAME --dry-run            # Run through the test pkg installation,
                                              # dry run will not install eventually
```

Turning on PHP debugging (settings.php)
```
$settings['skip_permissions_hardening'] = TRUE;
$config['system.logging']['error_level'] = 'verbose';
// $settings['container_yamls'][] = DRUPAL_ROOT . '/sites/default/services.yml';
```

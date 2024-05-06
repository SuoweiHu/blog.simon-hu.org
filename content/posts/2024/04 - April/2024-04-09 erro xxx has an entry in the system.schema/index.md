---
title: "Drupal Error: Module ... has an entry in the system.schema key/value storage"
date: "2024-04-08"
categories: ["Drupal"]
---

### Error Found
After performing `composer update`, and during the execution of `/update.php` to update database, the following was observed:
![2024-04-09T091115](2024-04-09T091115.jpg)


### Error Resolution
To repair these sorts of errors, you must remove the orphaned entries from the system.schema key/value storage system. There is **no UI** for doing this. At this point, the simplest solution is to use **drush to evaluate some PHP code** to invoke a system service to manipulate the system.schema table. For example, to clean up these two errors:
```
Module  media_entity         has an entry in the system.schema key/value storage, but is missing from your site.
Module  media_entity_image   has an entry in the system.schema key/value storage, but is missing from your site.
```
You will need to perform the following drush command
```
drush php-eval "\Drupal::keyValue('system.schema')->delete('media_entity');"
drush php-eval "\Drupal::keyValue('system.schema')->delete('media_entity_image');"
```


### Reference
- [[Drupal Community] Update.php warns administrators if there are orphaned entries in the system.schema key/value storage](https://www.drupal.org/node/3137656)
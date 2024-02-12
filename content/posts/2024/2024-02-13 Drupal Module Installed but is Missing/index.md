---
title: "Drupal Module Installed but "
date: "2024-02-13"
categories: ["Drupal"]
---

## Error Encountered

```
The following module is marked as installed in the core.extension configuration, but it is missing:
* xxyyzz_module_name
```

## Solutions


**Solution 1: Remove from `core.extension`**


If you have access to the command-line-interface and drush command, you can do it via:
```
    $ ahoy drush cdel core.extension module.MYMODULE
```
(OR) If you have acccess to the configuration synchronization, you can also do that via exporting the configuration, manually changing the `core.extension`, then importing the modified configruation again.


**Solution 2: Database**

- Drupal 7:    `drush sql-query "DELETE from system where type = 'module' AND name = 'MYMODULE';"`
- Drupal 8:    `drush sql-query "DELETE FROM key_value WHERE collection='system.schema' AND name='MYMODULE';"`
- Drupal 9/10: `drush sql-query "DELETE FROM key_value WHERE collection='system.schema' AND name='MYMODULE';"`

(This one failed on my attempt in govcms)


**Solution 3: Generate Module, Install, then Uninstall**

By generating a module with the same machine name and then uninstalling it, you can quickly resolve this issue.
```
    $ drupal generate:module
    $ drush pm-uninstall
```
Then you can delete the newly generated module from the file system and continue with your day.

(This approach I have not attempted)


## Reference
- Drupal Community: [How to fix "The following module is missing from the file system..." warning messages](https://www.drupal.org/node/2487215)
- Drupal Answer: [How to solve the "The following module is missing from the file system" error?](https://drupal.stackexchange.com/questions/245731/how-to-solve-the-the-following-module-is-missing-from-the-file-system-error)
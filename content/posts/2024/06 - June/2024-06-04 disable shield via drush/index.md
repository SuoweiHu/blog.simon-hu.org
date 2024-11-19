---
title: "Disable Shield via Drush"
date: "2024-06-04"
tags: ["Drupal"]
---





In Drupal, the "**Shield**" module is used to protect your site with a simple HTTP authentication prompt, which is typically needed during development to prevent unauthorized access to the site.



### Disable Shield via Drush

To disable the Shield module using Drush (Drupal's command-line shell), you can use the following command:

**For Drupal 8 and later:**

From Drupal 8 onwards, modules are no longer disabled—they are uninstalled if you need to remove them. If you simply want to disable the Shield authentication (and not uninstall the module), you might need to change its configuration instead. However, if uninstalling is your aim:

```bash
drush pm-uninstall shield
```

This command will completely uninstall the Shield module.

If you're looking to just disable the HTTP authentication without uninstalling the module (e.g., switching it off in a settings file or interface), you often **can’t directly do** this through Drush as it involves a configuration change rather than a module state change. You would have to change the configuration by updating the appropriate settings via the Drupal admin UI, or by editing the module’s configuration files directly.

**For Drupal 7:**

In Drupal 7, you can disable a module (without uninstalling it) using the following Drush command:

```bash
drush dis shield -y
```

This command will disable the Shield module. The ﻿-y option answers "yes" to all prompts, streamlining the process.


-------------------
### General Notes

Ensure that Drush is correctly installed and that you are running the command from within your Drupal root directory or use the ﻿`-r` or `﻿--root` option to specify the Drupal root directory if you’re outside of it. After using Drush to change module states, it's often a good idea to clear the site cache. You can do this with Drush by running:

```bash
drush cr        #for Drupal 8+
drush cc all    #for Drupal 7
```


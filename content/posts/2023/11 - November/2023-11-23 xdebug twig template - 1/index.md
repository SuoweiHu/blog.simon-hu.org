---
title: "Drupal X-Debug Twig Template 1: Turning on X-Debug"
date: "2023-11-23"
tags: ["Drupal"]
---

> Note:
> This post focuses on developing a Drupal website on a MacOS machine using MAMP & MAMP Pro hosting software, Apache HTTP Server, and MySQL Backend. The goal is to debug the PHP file to access the variables available in a Twig template.

## Turning on X-Debug for PHP (Pro MAMP)

**If you are developing using a Pro MAMP:** simply turn the the "Xdebug (Debugger)" setting under the "Language > PHP" tab (on the sidebar):

![2023.11.23 - 162521](2023.11.23%20-%20162521.jpg)



Then click "Save", and start/restart MAMP, and proceed to [phpinfo page for mamp](http://localhost:8888/MAMP/phpinfo.php), and scroll down; At the roughly middle of the phpinfo page, you should be seeing something like this ([link to image of full xdebug](2023.11.23%20-%20161837.jpg)):

![2023.11.23 - 162229](2023.11.23%20-%20162229.jpg)




## Turning on X-Debug for PHP (Non-Pro MAMP)

**If you are developing using a non-pro MAMP software:** first turn the MAMP off, then configure the `php.ini` file located at the directories (noting that when you change to a different php version, you will have to repeat the step, adding the lines in to the corresponding php.ini for the selected version):

- `/Applications/MAMP/conf/php[version]/php.ini`
- `/Applications/MAMP/bin/php/php[version]/conf/php.ini`

At the bottom of the file, you will see something like:
```ini
[xdebug]
; zend_extension="/Applications/MAMP/bin/php/.../lib/php/extensions/no-debug-non-zts-20220829/xdebug.so"
xdebug.mode=debug
xdebug.start_with_request=yes
;
; Unlike Xdebug 2, where there was an enabling setting for each feature, with
; Xdebug 3 you put Xdebug into a specific mode, which can be configured with the
; xdebug.mode setting.
;
; This setting, in combination with xdebug.start_with_request is the new way to
; enable functionality, and to configure when Xdebug's feature activates.
;
; Please also note: Xdebug's default debugging port has changed from 9000 to 9003.
; xdebug.client_port=9003
```

In order to turn on the xdebug extension for php, simply uncomment the line for `zend_extension`:

```ini
[xdebug]
zend_extension="/Applications/MAMP/bin/php/.../lib/php/extensions/no-debug-non-zts-20220829/xdebug.so"
xdebug.mode=debug
xdebug.start_with_request=yes
;
; Unlike Xdebug 2, where there was an enabling setting for each feature, with
; Xdebug 3 you put Xdebug into a specific mode, which can be configured with the
; xdebug.mode setting.
;
; This setting, in combination with xdebug.start_with_request is the new way to
; enable functionality, and to configure when Xdebug's feature activates.
;
; Please also note: Xdebug's default debugging port has changed from 9000 to 9003.
; xdebug.client_port=9003
```

Or, if you wish to make further customization to the xdebug, here's an example configuration to quickly copy from:

```ini
[xdebug]
zend_extension           = "/Applications/MAMP/bin/php/.../lib/php/extensions/no-debug-non-zts-20220829/xdebug.so"
xdebug.remote_autostart  = 1
xdebug.remote_enable     = 1
xdebug.remote_host       = localhost
xdebug.remote_port       = 9000
xdebug.remote_handler    =d bgp
```

Then start/restart MAMP, and proceed to [phpinfo page for mamp](http://localhost:8888/MAMP/phpinfo.php), and scroll down; At the roughly middle of the phpinfo page, you should be seeing something like this ([link to image of full xdebug](2023.11.23%20-%20161837.jpg)):

![2023.11.23 - 162229](2023.11.23%20-%20162229.jpg)

In case this is not working, try confirming you are changing the right configuration file (also via phpinfo)

![2023.11.23 - 162328](2023.11.23%20-%20162328.jpg)


## Reference
- [https://dillieodigital.wordpress.com/2015/03/10/quick-tip-enabling-xdebug-in-mamp-for-osx/](https://dillieodigital.wordpress.com/2015/03/10/quick-tip-enabling-xdebug-in-mamp-for-osx/)
- [https://joshbuchea.com/mac-enable-xdebug-in-mamp/](https://joshbuchea.com/mac-enable-xdebug-in-mamp/)
- [https://craftquest.io/courses/debugging-with-xdebug/36070](https://craftquest.io/courses/debugging-with-xdebug/36070)
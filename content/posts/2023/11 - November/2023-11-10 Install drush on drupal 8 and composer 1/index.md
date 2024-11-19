---
title: "Install drush on drupal 8 site (using downgraded composer ver.1)"
date: 2023-11-10
tags: [Drupal 8, Drush, Composer 1]
tags: ["Drupal"]
---


## Intuition

I was recently working on a client site, and I got to the issue where the site will show "Page unavailable" upon login. And upon the suspicion of a mis-placed module or uncleared cache, I wanted to install drush to perform some drush commands.

I ran `composer require drush/drush` which will install the most recent compatible drush on my current working directory, but then I got this error:
```
...
The "composer/installers"           plugin was skipped because it requires a Plugin API version ("^1.0")    that does not match your Composer installation ("2.6.0"). You may need to run composer update with the "--no-plugins" option.
The "drupal/core-composer-scaffold" plugin was skipped because it requires a Plugin API version ("^1.0.0")  that does not match your Composer installation ("2.6.0"). You may need to run composer update with the "--no-plugins" option.
The "drupal/core-project-message"   plugin was skipped because it requires a Plugin API version ("^1.1")    that does not match your Composer installation ("2.6.0"). You may need to run composer update with the "--no-plugins" option.
The "drupal/core-vendor-hardening"  plugin was skipped because it requires a Plugin API version ("^1.1")    that does not match your Composer installation ("2.6.0"). You may need to run composer update with the "--no-plugins" option.
...
```
After some research, I found this issue could be potentially related to a version mis-match of the composer and the drupal 8 (reference: [link](https://www.drupal.org/project/search_api_solr/issues/3213306)), the composer in the project could be of version 1.XX, and the local instance is using version 2.XX ...


## Failed Attempt

I quickly went online and found this solution: [link](https://serverpilot.io/docs/how-to-downgrade-to-composer-version-1/), that uses the following command to upgrade/downgrade composer:
```shell
# Down-grade to composer 1
sudo composer self-update --1; sudo apt-mark hold sp-composer;
# Up-grade   to composer 2
sudo apt-mark unhold sp-composer; sudo composer self-update --2
```
But this one only updates the composer version globally, and it does not solve the issue of installing drush on the current working directory. (I am using MAMP as my web server, and as a result, I will need to update the version of the composer located at `/Applications/MAMP/bin/php/composer`)


## Working Solution

In order to upgrade the "correct" composer, I did the following:

1. **First**, getting one composer 1.10 version phar file from this site: [link](https://getcomposer.org/download/). Place it on some location you can found, here I am putting it at my MAMP directory`/Applications/MAMP/bin/php/composer.phar`.

   (Note: in order to run this file, you will either need to use box command to compile it (`box compile composer.php`), or use php as the interpreter to run it (`php composer.php`), Since here we are only using it temporarily, we will use the shortcut of php: `php /Applications/MAMP/bin/php/composer.phar --version )
2. **Second**, I will need to find the correct compatible version of drush via the [official website](https://www.drush.org/12.x/install/), for my instance `drush/drush:10`
3. **Third**, running the require command to install: `php /Applications/MAMP/bin/php/composer.phar require drush/drush:10`
4. **Lastly**, (OPTIONAL) If the memory is not sufficient during the `composer install/update` you might see something ilke this: `Fatal error: Allowed memory size of 1610612736 bytes exhausted` .

   In order to change the memory limit you will need to add a parameter `-d memory_limit=-1 `, the command comes together looks like:  `php -d memory_limit=-1 /Applications/MAMP/bin/php/composer.phar require drush/drush:10`

As a result you should see the downloaded instance of composer installing drush successfully:

![2023.11.10 - 113349](2023.11.10%20-%20113349.png)

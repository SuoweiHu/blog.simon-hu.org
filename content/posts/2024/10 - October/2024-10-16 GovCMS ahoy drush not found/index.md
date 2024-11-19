---
title: "Reoslution for [\"/usr/local/bin/drush\": not found\"]"
date: "2024-10-16"
tags: ["Ahoy", "GovCMS"]
---



## Error Repeated

For some of the GovCMS client, I ran into this problem while trying to install the client website on my local computer: after running `pygmy up`  to crank up the amazie container, `composer install` to install the package, I got the following error while running `ahoy build` (same for `ahoy up`):

```
> ahoy build
[+] Building 1.0s (29/37)                                                                                                     docker:desktop-linux
 => [php internal] load build definition from Dockerfile.php                                                                                  0.0s
 => => transferring dockerfile: 244B
 ...
 ...
 ...
 => CACHED [test stage-1  8/12] RUN composer --working-dir=audit-site update --ignore-platform-reqs --no-interaction --no-suggest             0.0s
 => CACHED [test stage-1  9/12] WORKDIR /app                                                                                                  0.0s
 => ERROR [test stage-1 10/12] COPY --from=cli /usr/local/bin/drush /usr/local/bin/                                                           0.0s
 => CANCELED [nginx stage-1 1/2] FROM docker.io/govcms/nginx-drupal:10.x-latest@sha256:aae5325c977a943969a02ea0b1a6340e3cac6f58fcbd032911e76  0.2s
 => => resolve docker.io/govcms/nginx-drupal:10.x-latest@sha256:aae5325c977a943969a02ea0b1a6340e3cac6f58fcbd032911e76f3bd80d3677              0.0s
 => => sha256:ee1752d59231d421688bce9acc6f031f70dababa0e22f963a9ab9f8de0acdbfb 8.42kB / 8.42kB                                                0.0s
 => => sha256:4e8b32b7ceed2273f0a46cfa7750ab6d83eb8c59186ec29a4103a9747a43e50d 32.19kB / 32.19kB                                              0.0s
 => => sha256:aae5325c977a943969a02ea0b1a6340e3cac6f58fcbd032911e76f3bd80d3677 1.61kB / 1.61kB                                                0.0s
 => CANCELED [php stage-1 1/2] FROM docker.io/govcms/php:10.x-latest@sha256:1a6fe5b2d8eea699f0726a5fee5e6d02ad4775ab752a1dc340f8fda62967eea6  0.1s
 => => resolve docker.io/govcms/php:10.x-latest@sha256:1a6fe5b2d8eea699f0726a5fee5e6d02ad4775ab752a1dc340f8fda62967eea6                       0.0s
 => => sha256:86d49b3929177bc771c7c46842bbe2dead6fc633aba216231353326b5c525884 24.94kB / 24.94kB                                              0.0s
 => => sha256:59fd0b12489ee3c2a16122c0a1b0ee06882ca6d355aefbd20bd904b49b377e06 6.55kB / 6.55kB                                                0.0s
 => => sha256:1a6fe5b2d8eea699f0726a5fee5e6d02ad4775ab752a1dc340f8fda62967eea6 1.61kB / 1.61kB                                                0.0s
------
 > [test stage-1 10/12] COPY --from=cli /usr/local/bin/drush /usr/local/bin/:
------
failed to solve: failed to compute cache key: failed to calculate checksum of ref 0402bcea-675b-4e70-bf0f-dfa57911b0c1::ph76omges2o2rc5qsj75n5txc: "/usr/local/bin/drush": not found
```

See screenshot of this at: [this link](2024-10-16T103750.png).





## Error Resolved

Thanks to my intelligent teammate (saved me 3 days of head scratching literally), this happens because some lines are commented in the docker related file, namely the `Dockerfile.cli` file:

```
...

# Ensure drush-launcher instead of Drush 8 in /home/.composer
# @todo Make drush launcher available upstream, @see https://github.com/amazeeio/lagoon/pull/1183
# RUN wget -O /usr/local/bin/drush "https://github.com/drush-ops/drush-launcher/releases/download/0.6.0/drush.phar" \
#   && chmod +x /usr/local/bin/drush \
#   && rm -Rf /home/.composer/vendor/bin

...
```

Simply uncomment those (line 38 - line 40):

```
...

# Ensure drush-launcher instead of Drush 8 in /home/.composer
# @todo Make drush launcher available upstream, @see https://github.com/amazeeio/lagoon/pull/1183
RUN wget -O /usr/local/bin/drush "https://github.com/drush-ops/drush-launcher/releases/download/0.6.0/drush.phar" \
  && chmod +x /usr/local/bin/drush \
  && rm -Rf /home/.composer/vendor/bin

...
```

Let's use ChatGPT to explain line by line what these are doing:

*   The purpose of this snippet is to install the Drush Launcher in a Docker container environment. The Drush Launcher allows you to run Drush commands without having Drush installed globally. Instead, it looks for a site-local Drush in your project directory, making it easier to manage different Drush versions across different projects. By placing the Drush Launcher in `/usr/local/bin`, it ensures that the drush command is available in the system's PATH, making it accessible from any location within the container.
    1.   Install Drush Launcher: `RUN wget -O /usr/local/bin/drush "https://git...6.0/drush.phar"`
    2.   Make Drush Executable: `chmod +x /usr/local/bin/drush`
    3.   Clean Up: `rm -Rf /home/.composer/vendor/bin` (used to remove any existing Drush binaries or other executables that might interfere with the newly installed Drush Launcher)

Trying to re-run `ahoy build` yields no error anymore now: [see screenshot](2024-10-16T104649.png)








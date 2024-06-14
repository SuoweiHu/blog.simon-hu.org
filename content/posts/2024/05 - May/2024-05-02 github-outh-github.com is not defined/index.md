---
title: "[GovCMS SaaS] ahoy error: github-outh.github.com is not defined"
date: "2024-05-02"
categories: ["GovCMS"]
---




---

## Issue Reproduced

I run into this issue while performing `ahoy build` command for a client site, which will initiate the GovCMS environment, including running the `composer install` command <u>inside the docker container</u> to the install the required modules from the drupal modules repositories. And that have triggered the error: `In ConfigCommand.php Line 322: github-oauth.github.com is not defined `and `process "/bin/sh -c composer config -global github-oauth.github.com $GOVCMS_GITHUB_TOKEN" did not complete successfully: exit code: 1`.

You can find the exact error in the following screenshot:

![2024-05-02T111134](2024-05-02T111134.jpg)



---

## Resolution of Error

The error occurs inside the docker container, where it cannot find the variable `$GOVCMS_GITHUB_TOKEN`, as a result it cannot pull some of the packages via the composer command. To resolve this, we can use a `docker-compose.override.yml` file to overide and add the `$GOVCMS_GITHUB_TOKEN` variable for the docker container.

For my instance I will need to create this file at the root directory as the follows:

![2024-05-02T171646](2024-05-02T171646.jpg)

and have the following lines of configuration to set the environmental variables:

```
services:
  cli:
    build:
      args:
        GITHUB_Key: ghp_XXXXXXXXXXXXXXXXXXXXXXXXXXXX
        GOVCMS_GITHUB_TOKEN: ghp_XXXXXXXXXXXXXXXXXXXXXXXXXXXX
```




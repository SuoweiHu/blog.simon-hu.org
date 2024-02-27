---
title: "Resolve error: 'anti-virus scanner could not check the file'"
date: "2024-02-28"
categories: ["Drupal"]
---



## Issue Found
```
Drupal Core: 8.7.8
Lightning: 4.0.5
PHP: 7.2

Steps to reproduce.
- Enable ClamAV and leave "host" field blank.
- Go to Content > Add Media > Image.
- Upload an image.
- An error should be returned reading: "The anti-virus scanner could not check the file, so the file cannot be uploaded. Contact the site administrator if this problem persists." This is the expected result since we did not configure the clamav host.
```

![image-20240228095014860](image-20240228095014860.png)



## Resolution Approah

Go to "/admin/config/httpav" and:
- (either) toggle "`llow unchecked (If the HTTP request fails, assume success.)`" on
- (or) toggle "`Enabled (If files should be checked)`" off

![image-20240228095029938](image-20240228095029938.png)


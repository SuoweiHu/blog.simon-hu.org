---
title: "Drupal Error: Update No available releases found"
date: "2024-01-07"
categories: ["Drupal"]
---


## Error

I found this error when inspecting one of my client's website, of "update manager" fails to check the pending update module/core (in my case, drupal core is 10.2.0 of which have an available version update 10.2.1) but it is not shown on the "update manager" panel.

![image-20240108103022253](image-20240108103022253.png)

## Resolution

While checking updates Drupal creates some rows inside the `key_value` table which should be deleted after checking is complete but looks like they doesn't for some reason. So deleting the related rows manually solved my problem ([reference](https://drupal.stackexchange.com/questions/232520/cannot-update-no-available-releases-found)):

```
DELETE FROM key_value WHERE collection = 'update_fetch_task';
```

You can run this SQL query via drush

```
drush sql-query "DELETE FROM key_value WHERE collection='update_fetch_task'"
```


## Resource

- [Drupal Answers - Cannot update: "No available releases found"](https://drupal.stackexchange.com/questions/232520/cannot-update-no-available-releases-found)


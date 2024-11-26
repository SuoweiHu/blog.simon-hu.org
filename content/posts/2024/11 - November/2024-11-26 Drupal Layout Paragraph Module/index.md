---
title: "Drupal Layout Paragraph Module"
date: 2024-11-26
tag: ["Drupal", "Drupal Modules"]
---





## Step to install the Layout Paragraph Module

Step-0: below is how the paragraph component by default looks like in the drupal admin backend: 

![2024-11-26T162050](2024-11-26T162050.png)



Step-1: Install and enable the "`drupal/layout_paragraph`" module, and configure view of the content/paragraph to use "Layout Paragraph": 

![2024-11-26T161557](2024-11-26T161557.png)

![2024-11-26T161505](2024-11-26T161505.png)



Step-2: add the `paragraph--name--xxyyzz.html.twig` to the administration theme (we are using `claro` as admin theme in this case), you would need to keep the `{% block paragraph %}`, `{% block content %}`, and `<div {{ attributes.addClass(classes) }} ... >` in order for the paragraph layout to work:

![2024-11-26T161334](2024-11-26T161334.png)![2024-11-26T161928](2024-11-26T161928.png)

![2024-11-26T162216](2024-11-26T162216.png)

## Reference

https://www.drupal.org/project/layout_paragraphs
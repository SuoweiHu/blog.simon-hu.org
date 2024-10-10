---
title: "Drupal Tailwind CSS / Tailwind UI"
date: "2024-10-10"
categories: ["Drupal", "Tailwind"]
---





## Introduction

This post will provide a quick guidance on: 

-   how-to for installing the "Tailwind CSS" on to your custom drupal theme/sub-theme, 
-   how to create a reusable component styled based on "Tailwind UI" using paragraph module

Resources referenced in this post includes: 

-   Tailwind CSS - Official Installation Guide: https://tailwindcss.com/docs/installation
-   Tailwind UI - Official Installation Guide: https://tailwindui.com/documentation
-   Theme Drupal - Adding assets: [https://www.drupal.org/.../asset](https://www.drupal.org/docs/develop/theming-drupal/adding-assets-css-js-to-a-drupal-theme-via-librariesyml)







## Step-1: Initialization of Sub-Theme 

To begin with, you can refer to [this post](https://www.drupal.org/docs/develop/theming-drupal/creating-sub-themes) on how to create a sub-theme based on any contributed theme, for my instance I am creating my sub-theme of machine name `tailwind-civic` based on the [CivicTheme](https://www.drupal.org/project/civictheme), which has its special provided script to generate sub-theme (see [screenshot](2024-10-10T113214.png)): 

```
> cd "themes/contrib/civictheme"
  # cd to the base theme's directory to begin with
  
> php civictheme_create_subtheme.php tailwind_civic "Civic Theme (Tailwind)" "Custom theme using Tailwind CSS with Civic Theme as base" "../../themes/custom/tailwind-civic"
  # altered based on template -> php civictheme_create_subtheme.php <theme_machine_name> "Human theme name" "Human theme description" /path/to/theme_machine_name)

   ------------------------------------------------------------------------------------------------------------------
  | Civic Theme (Tailwind) (tailwind_civic) sub-theme was created successfully in ".../themes/custom/tailwind-civic".
  | 
  | ----------
  | NEXT STEPS
  | ----------
  | 
  | Ensure that front-end assets can be built:
  |   cd ".../themes/custom/tailwind-civic"
  |   npm install
  |   npm run build
  |   npm run storybook
  | 
   ------------------------------------------------------------------------------------------------------------------

> cd ".../themes/custom/tailwind-civic"              
  # cd to the sub-them's directly 

> npm install && npm run build && npm run storybook  
  # install dependencies (not all theme requires this step)

```

At the end you will have a sub-theme under your `theme/custom` folder with a hierachy alike the following: 

```
tailwind_civic
    |-tailwind_civic.info.yml       # defining a theme's metadata and configuration
    |-tailwind_civic.libraries.yml  # defining asset libraries, which include CSS, JavaScript, and other front-end resources
    |-tailwind_civic.theme          # defining theme-specific logic and functions that alter or enhance the theme's behavior
    |-css
       |-style.css
       |-style.css.map
    |-js
       |-script.js
    |-templates
       |-maintenance-page.html.twig
       |-node.html.twig
       |-html.html.twig
    |-images
       |-buttons.png
       |-banner.png
       |-avatar.png
    |-logo.svg
    |-config
       |-install - tailwind_civic.settings.yml
       |-schema  - tailwind_civic.schema.yml
```

Then simply enable your sub-theme (as well as the base theme if you haven't done so) in the drupal backend, or via the `drush` command : 

```
> drush theme:enable civictheme -y
> drush config-set system.theme default civictheme
> # Eanble Base Theme

> drush theme:enable tailwind_civic -y
> drush config-set system.theme default tailwind_civic
> # Enable sub-theme

> drush cr
> # Clear the cache
```

Once properly installed you should see your theme's style taking effect. (I would recommend you double-check by adding some debug css in the `style.css` file, for instance `*{border: 5px dotted #F9B455 !important;}` refresh the page and see if they take effect)





## Step-2: Installation of Tailwind CSS

Tailwind CSS along with its dependencies are managed by node package manager 





## Step-3: Building Re-usable Component (with Tailwind UI + Paragraph Module)

Please try it first....








---
title: "GovCMS PaaS (Platform as a Service) Update"
date: "2024-10-16"
categories: ["GovCMS", "Drupal"]
---

## Introduction

As mentioned in a earlier post "GovCMS SaaS vs PaaS", in SaaS website, the client is responsible for all the patching including security updates (unlike SaaS environments which does it all automatically). This post will guide you through on how to perform these update yourself. 

To begin with we'll need to differntiate the compositional part of the GovCMS PaaS website that will need update: 

*    `govCMS/govCMS` : the main repository for the Drupal-based GovCMS distribution, which provides a content management system tailored for Australian government websites. It includes core functionality and modules necessary for compliance and accessibility standards. ([GitHub](https://github.com/govCMS/GovCMS), [Packagist](https://packagist.org/packages/govcms/govcms))
*   `govCMS/scaffold-tooling`: comprises a collection of standard configurations, scripts, and packages designed to support the GovCMS scaffold. It includes tools for continuous integration and testing, enhancing development and deployment processes. ([Github](https://github.com/govCMS/scaffold-tooling), [Packagist](https://packagist.org/packages/govcms/scaffold-tooling))
*   `custom/patch` : some PaaS website also have custom module (contributed module) installed, or patches serve as temporary fixes or modifications to the website's existing codebase. They are utilized to rectify bugs that may emerge during regular operation, ensuring the site maintains optimal performance and user experience. 

The associated composer / patch files are the follwing: 

*   `$root_folder / composer.json`: record the version of core/scaffold  ([e.g. File](composer.json))
*   `$root_folder / composer.lock`: this is important as we need to override the old `.lock` file on the server ([e.g. File](composer.lock))
*   `$root_folder / custom / composer / composer.json`: record version of custom module that is installed ([e.g. File](custom-composer.json))
*   `$root_folder / custom / composer / patch.lock`: record any patches that is in-use ([e.g. File](custom-patches.json))

(\* Notice that the path for the custom module / patch can be altered in the main `composer.json` file: `"repositories": [ { "type": "path", "url": "custom/composer" },`)










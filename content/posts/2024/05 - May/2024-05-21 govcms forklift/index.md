---
title: "GovCMS Forklift"
date: "2024-05-21"
tags: ["GovCMS"]
---



> !!!!
>
> **This Post is simply a `copy`-`paste` from the GocCMS knowledge archive**
> https://www.govcms.support/support/solutions/articles/51000095221-forklift-basics
>
> (If there is any infringement, please contact me, and I'll delete the post.)
>
> !!!!







## What is a forklift & what is not?

### What is a forklift ?

A forklift is the process of copying a database and/or files (CMS media assets) from a **source environment/site** into an existing **target environment/site**. This includes:

-   Moving a site built locally from a developer onto the GovCMS platform
-   Moving a site from one project to another
-   Moving a database/files in the same project from a lower environment to Master

#### What is not a forklift ?

In some instances forklifts are not needed or not warranted. This includes:

-   Developing on the Master branch of a project
-   Creating a new feature branch in the same project
-   A site that isn't based on Drupal
-   For SaaS sites, sites not built with the GovCMS distribution





## What is the source/target?

#### Source Environment (or Site)

When scheduling a forklift with us, you will be asked to specify the *source environment*. There are two types of source environments:

-   **External source**: If a GovCMS site has originally been developed outside the GovCMS Hosting Platform (for example a local development environment, or any 3rd party hosting provider), its database and files live on a server external to the GovCMS Hosting Platform. That server is called *the "source"* (environment) in the context of a forklift.
-   **GovCMS secondary environment**: once your site has been successfully transferred to the GovCMS Hosting Platform, besides the single live/production site, you may also build up to 4 additional *"secondary environments"* (these can, for example, be used in order to test new features your developers or developer partner are building). There may be cases where the entire database and/or files need to be sourced from such a secondary environment.

#### Target Environment

The second piece of information we need in order to schedule a forklift for you is the *target environment*. Although the target environment in most cases is the live/production environment, there may be cases where the database and/or files need to be forklifted into a secondary environment first (for testing).





## How to schedule & estimated time ?

### How do I schedule in a forklift with GovCMS?

To schedule a forklift:

-   Raise a GovCMS Service Desk ticket.

-   Indicate your preferred date but be aware that scheduling is subject to availability.

-   We **CANNOT recommend** forklift scheduled on Fridays or a day before a public holiday.

    This is to ensure we have the GovCMS Service Desk resources available should we encounter an issue during the forklift that requires an extended amount of time to resolve.

### How long may a forklift take?

A forklift usually takes no more than 2 hours.  We also recommend you allow up to 48 hours for the forklift to complete, should any problem need to be mitigated.





## Fork Form & Approval Required ?

### Form Form

The service desk will send you a forklift form after receiving a forklift request from you through a service desk ticket. The form specifies the following information required for the GovCMS Service Desk to complete a forklift:

-   What is the source of the forklift assets?
-   What is the source project (if applicable)?
-   What is the source environment (if applicable)?
-   What is the target project?
-   What is the target environment?
-   What needs to be copied? (the database, media assets, or both)
-   How do you want to handle existing files in the target environment? (remove/replace, or leave in place)
-   What is the preferred date for the forklift? (avoid Fridays or any day before a public holiday, unless absolutely necessary)
-   Any additional details or comments (eg timing requirements)?

### Approval for development agencies/vendors

Before GovCMS books a forklift, we need approval from an authorised member of the Government Agency/Department responsible for the target project/site.



To avoid delays, development agencies/vendors must seek this approval ahead of time. The approval must come in the form of a comment added to the ticket where the forklift is requested. It needs to come from the project owner within the Government Agency.
















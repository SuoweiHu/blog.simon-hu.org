---
title: "Drupal \"Entity Reference\" field vs \"Entity Reference Revision\" field vs \"Dynamic Entity Reference\""
date: "2024-04-23"
categories: ["Drupal"]
draft: false
publishDate: "2024-04-22"
---



## Comparison

**Overview**

-   According to the project page for [Entity Reference Revision](https://www.drupal.org/project/entity_reference_revisions) module:

    >   **Entity Reference Revisions** adds an **Entity Reference** field type with **revision support**, allowing specific entity revisions to be references. This is useful for modules like Paragraphs and Inline Entity Form

-   According to the project page for [Dynamic Entity Reference](https://www.drupal.org/project/dynamic_entity_reference) module: 

    >   Dynamic Entity Reference provides a field type/widget/formatter combination for Drupal 8 that allows an entity-reference field to reference more than one entity type.

-   According to one of the [blog post](https://gorannikolovski.com/blog/migrate-existing-entity-reference-field-entity-reference-revisions-field#:~:text=Entity%20Reference%20and%20Entity%20Reference,reference%20a%20specific%20entity%20revision.):

    >    **Entity Reference** and **Entity Reference Revisions** fields are very similar, both enables more flexiblae reuse of data across the website, but the latter offers more flexibility when it comes to **<u>reverting to a previous revision</u>** in the case when you have a nested entity. In other words, this field type allows you to reference a specific entity revision.

**Use Case**

-   **Entity Reference**

    if more commonly used for reference type such as:

    -   Taxonomy Term
    -   Media (file/image)

    see [example](2024-04-23T090655.jpg)

-   **Entity Reference Revision**

    is more commonly used for reference type such as:

    -   Paragraph Type (found at: [link](https://www.drupal.org/project/paragraphs))

    see [example](2024-04-23T090655.jpg)

-   **Dynamic Entity Reference**

    if more commonly used when you need to have more than one entity type in a single entity reference field (for instance if you want both "content", "file", "user", see [example](Screen%20Shot%202014-06-11%20at%208.00.21%20am.png))









---


## Reference
- Drupal Project Module:
    - [Entity Reference](https://www.drupal.org/project/entityreference)
    - [Entity Reference Revisions](https://www.drupal.org/project/entity_reference_revisions)
    - [Dynamic Entity Reference](https://www.drupal.org/project/dynamic_entity_reference)
- [Migrate existing Entity Reference field to Entity Reference Revisions field](https://gorannikolovski.com/blog/migrate-existing-entity-reference-field-entity-reference-revisions-field#:~:text=Entity%20Reference%20and%20Entity%20Reference,reference%20a%20specific%20entity%20revision.)
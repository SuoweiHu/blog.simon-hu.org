---
title: "Twig - Generate Unique ID for Component"
date: "2023-11-22"
categories: ["twig"]
---

## Intuition

Some time you would like to have `id` in the twig template component to enable say: precise query/selector targeting with css, or setting attributes to enable certain behavior for javascript frameworks such as bootstrap:


For example: the example from [Bootstrap Accordion](https://getbootstrap.com/docs/5.0/components/accordion/)
```html
<!-- Notice the #collapseOne below  -->
<div class="accordion" id="accordionExample">
    <div class="accordion-item">
        <h2 class="accordion-header" id="headingOne">
        <button class="accordion-button" type="button" data-bs-toggle="collapse" data-bs-target="#collapseOne" aria-expanded="true" aria-controls="collapseOne">
            Accordion Item #1
        </button>
        </h2>
        <div id="collapseOne" class="accordion-collapse collapse show" aria-labelledby="headingOne" data-bs-parent="#accordionExample">
        <div class="accordion-body">
            <strong>This is the first item's accordion body.</strong>
        </div>
        </div>
    </div>
  </div>
  ```

  ## Method-1: random

  Simply set the unique id using  `{% set unique-id = random() %}`, then use it as the attribute for id or data selector, such as below:
  ```html
    {% set unique-id = random() %}
     ...
        <button ... data-bs-target="#{{unique-id}}"  aria-controls="{{unique-id}}">Accordion Item #1</button>
        <div id="{{unique-id}}"...">
     ...
  ```

  Reference:
  - [StackExchange - Give included twig component unique ID](https://craftcms.stackexchange.com/questions/29628/give-included-twig-component-unique-id)


## Method-2:clean_unique_id

A new `clean_unique_id` Twig filter has been added to Drupal 10.1 and later. This can be used for getting a unique ID. The filter ensures that even if the template rendered multiple times, the ID remains unique for each usage.

Example:
```html
    ...
        <div {{ attributes.setAttribute('id', 'my-id'|clean_unique_id) }}></div>
    ...
```

Reference:
- [Filters - Modifying Variables In Twig Templates](https://www.drupal.org/docs/develop/theming-drupal/twig-in-drupal/filters-modifying-variables-in-twig-templates#clean_unique_id)


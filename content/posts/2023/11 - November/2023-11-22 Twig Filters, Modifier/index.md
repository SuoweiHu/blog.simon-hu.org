---
title: "Twig - Twig Filters/Modifier (Universal & Drupal Specific) "
date: "2023-11-22"
tags: ["twig"]
---


## Twig filter: universal filters
```
* striptags:    removing html syntax tag from from the string
                {{ content.variable.0.value | striptags }}             //REMOVE ALL TAGS
                {{ content.variable.0.value | striptags('<br><p>') }}  //REMOVE <br> and <p> TAGS
other filter:   abs batch capitalize column convert_encoding country_name currency_name currency_symbol data_uri date date_modify default escape filter first format format_currency format_date format_datetime format_number format_time html_to_markdown inline_css inky_to_html join json_encode keys language_name last length locale_name lower map markdown_to_html merge nl2br number_format raw reduce replace reverse round slice slug sort spaceless split striptags timezone_name title trim u upper url_encode
```
[Link to Post/Documentation](https://twig.symfony.com/doc/3.x/filters/index.html)


---

## Twig filters: drupal specific filters
```
* raw           : This filter should be avoided whenever possible, particularly if you're outputting data that could be user-entered.
* clean_class   : This filter prepares a string for use as a valid HTML class name. (for instance "txt/raw" to "txt-raw")
* render        : This filter is a wrapper for the render() function. It takes a render array and outputs rendered HTML markup. This can be useful if you want to apply an additional filter (such as stripping tags), or if you want to make a conditional based on the rendered output (for example, if you have a non-empty render array that returns an empty string). It also can be used on strings and certain objects, mainly those implementing the toString() method.
trans           : This filter (alternatively, t) will run the variable through the Drupal t() function, which will return a translated string. This filter should be used for any interface strings manually placed in the template that will appear for users.
placeholder     : This filter escapes content to HTML and formats it using drupal_placeholder(), which makes it display as emphasized text.
format_date     : This filter prepares a timestamp for use as a formatted date string
safe_join       : The safe_join filter joins several strings together with a supplied separator
without         : The without filter creates a copy of the renderable array and removes child elements by key specified through arguments passed to the filter. The copy can be printed without these elements. The original renderable array is still available and can be used to print child elements in their entirety in the twig template.
add_suggestion  : The add_suggestion filter allows adding a theme suggestion to a render array rendered with #theme.
clean_unique_id : A new clean_unique_id Twig filter has been added to Drupal 10.1 and later. This can be used for getting a unique ID.
```
[Link to Post/Documentation](https://www.drupal.org/docs/develop/theming-drupal/twig-in-drupal/filters-modifying-variables-in-twig-templates#clean_unique_id)


---

## Twig filters: add(), set(), recursive_merge()
```
set() filter             : `{{ form|set( 'element.#attributes.placeholder', 'Label' ) }}`
add() filter             : `{{ form|add( 'element.#attributes.class', 'new-class' ) }}`
recursive_merge() filter : `{{ form|recursive_merge( {'element': {'#attributes': {'placeholder': 'Label'}}} ) }}`
```
[Link to Post/Documentation](https://www.drupal.org/docs/contributed-modules/components/twig-filters-add-set-recursive_merge)


---
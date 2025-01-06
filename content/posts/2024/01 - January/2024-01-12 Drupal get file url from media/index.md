---
date: "2024-01-12"
title: "Drupal get URL from media entity in twig"
tags: ["Drupal"]
---

# PENDING

https://www.drupal.org/project/media_entity_image/issues/2856093
```twig
{# The field name in the content is "field_image2" #}
{% for key, image in content.field_image2  %}
    {% set media = image.entity %}
    {# The field name in the referenced entity is "field_image_file #}
    {% set file = media.field_image_file.entity | merge({'#image_style': 'thumbnail'}) %}
    {% set uri = file_url(file.uri.value)  %}
    <img src="{{ uri }}" alt="{{ media.name.value }}" />
{% endfor %}
```
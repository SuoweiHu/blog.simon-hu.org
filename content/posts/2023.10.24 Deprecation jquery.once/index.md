---
title: "Deprecation of \"jquery.once\" api"
summary: "Fixing custom modules' code that are dependent of jquery.once which is changing its api in newest drupal 10, hence making it compatible for the upgrade. "
categories: ["Drupal"]
tags: ["D9 - D10 Upgrade"]
date: 2023-10-24T11:30:03+11:00
---

You can follow the following template + example to update your modules to make it drupal 10 compatible:

---

Template:
`your-module-name.libraries.yml`

```diff
drupal.form:
  js:
    js/your-library-file.js: {}
  dependencies:
    - some-origina/dependency
+   - core/drupal
+   - core/jquery
+   - core/once
```
`your-library-file.js`
```diff
- (function ($, window, Drupal, drupalSettings) {
+ (function ($, window, Drupal, drupalSettings, once) {

...

Drupal.behaviors.myfeature = {
    attach(context) {
-     const elements  =  once('myfeature', '[data-myfeature]', context);
+     const $elements =  $(once('myfeature', '[data-myfeature]', context));
      ....
-     elements.forEach(processingCallback);
+     $elements.each(processingCallback);
    }
  };
  function processingCallback(index, value) {}
...


- })(jQuery, this, Drupal, drupalSettings);
+ })(jQuery, this, Drupal, drupalSettings, once);
```
----
Example
`bootstrap.libraries.yml`
```diff
drupal.form:
  js:
    js/misc/form.js: {}
  dependencies:
    - bootstrap/theme
+   - core/drupal
+   - core/jquery
+   - core/once
```
`form.js`
```diff
- (function ($, window, Drupal, drupalSettings) {
+ (function ($, window, Drupal, drupalSettings, once) {

  Drupal.behaviors.bootstrapForm = {
    attach: function (context) {
      if (drupalSettings.bootstrap && drupalSettings.bootstrap.forms_has_error_value_toggle) {

-       var $context = $(context);
-       $context.find('.form-item.has-error:not(.form-type-password.has-feedback)').once('error').each(function () {
-       const $elements =  $(once('myfeature', '[data-myfeature]', context));
-         var $formItem = $(this);
-         var $input = $formItem.find(':input');
-         $input.on('keyup focus blur', function () {
-           if (this.defaultValue !== void 0) {
-             $formItem[this.defaultValue !== this.value ? 'removeClass' : 'addClass']('has-error');
-             $input[this.defaultValue !== this.value ? 'removeClass' : 'addClass']('error');
-           }
-         });
-       });

+        const $elements =  $(once('.form-item.has-error:not(.form-type-password.has-feedback)', 'error', context));
+        $elements.each(function () {
+            const $elements =  $(once('myfeature', '[data-myfeature]', context));
+            var $formItem = $(this);
+            var $input = $formItem.find(':input');
+            $input.on('keyup focus blur', function () {
+                if (this.defaultValue !== void 0) {
+                    $formItem[this.defaultValue !== this.value ? 'removeClass' : 'addClass']('has-error');
+                    $input[this.defaultValue !== this.value ? 'removeClass' : 'addClass']('error');
+                  }
+            });
+        });

      }
    }
  };


- })(jQuery, this, Drupal, drupalSettings);
+ })(jQuery, this, Drupal, drupalSettings, once);
```



----
Reference:
- https://www.drupal.org/node/3158256
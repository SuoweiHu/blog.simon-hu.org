---
title: "CSS Media Query"
date: "2024-02-07"
categories: ["CSS"]
---


## Media Query Usage Syntax


**When used inside a CSS file ?**

A media query is composed of a media type and can include one or more media features that evaluate to true or false. (The mediatype is optional, if omitted, it will be set to all. However, if you use not or only, you must also specify a mediatype.) Whenever a media query is evaluated to be true, the corresponding style rules inside it will be applied.

```css
@media not|only mediatype and (media_feature_1) and (media_feature2) {
  CSS-Code-Line1;
  CSS-Code-Line2;
  CSS-Code-Line3;
  CSS-Code-Line4;
}
```

**When used outside a CSS file ?**

An alternative way of using the meidia query on the html file, below are some examples:
```html
<link rel="stylesheet" media="print" href="print.css">
<link rel="stylesheet" media="screen" href="screen.css">
<link rel="stylesheet" media="screen and (min-width: 480px)" href="example1.css">
<link rel="stylesheet" media="screen and (min-width: 701px) and (max-width: 900px)" href="example2.css">
```

## Syntax Detail


**Operand**

Meaning of the `not`, `only`, and `and` keywords:

| Value  | Description                                                                                                                                        |
| ----   | ----                                                                                                                                               |
| `not`  | This keyword inverts the meaning of an entire media query.                                                                                         |
| `only` | This keyword prevents older browsers that do not support media queries from applying the specified styles. It has no effect on modern browsers.    |
| `and`  | This keyword combines a media type and one or more media features.                                                                                 |

**Media Type**
| Value       | Description                                           |
| ----        | ----                                                  |
| `all`       | Used for all media type devices                       |
| `print`     | Used for print preview mode                           |
| `screen`    | Used for computer screens, tablets, smart-phones etc. |



**Media Feature**

| Value       | Description                                         |
| ----        | ----                                                |
|`orientation`| Orientation of the viewport. Landscape or portrait  |
|`max-height` | Maximum height of the viewport                      |
|`min-height` | Minimum height of the viewport                      |
|`height`     | Height of the viewport (including scrollbar)        |
|`max-width`  | Maximum width of the viewport                       |
|`min-width`  | Minimum width of the viewport                       |
|`width`      | Width of the viewport (including scrollbar)         |




## Reference

- [W3School - Link1](https://www.w3schools.com/css/css3_mediaqueries.asp)
- [W3School - Link2](https://www.w3schools.com/cssref/css3_pr_mediaquery.php)
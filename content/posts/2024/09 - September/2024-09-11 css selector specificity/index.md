---
title: "CSS Selector’s Specificity - [in progress]"
date: "2024-09-11"
categories: ["CSS"]
---

## Why does it matter ?

When writing new styles for a functioning website, it is common for individuals to override CSS styles above the existing ones. For example, if one aims to emphasize the `<h2>` heading on the FAQ card below, it is likely necessary to override its style settings to increase the `font-weight` and `font-size` values.

![2024-09-11T084510](2024-09-11T084510.jpg)

When a specific HTML element, such as an `<h2>`, already possesses predefined styles, it becomes necessary to craft new CSS rules that are sufficiently robust to supersede the current styling in effect. An example of this scenario is the CSS rule `.slide_content .slide_caption a h2` (`Rule-A`)which is being applied to the upper FAQ card (this can be observed within the style panel situated on the right side of DevTools in Chrome)

![2024-09-11T084707](2024-09-11T084707.jpg)

Upon adding a rule utilizing `.slide__content h2` as the selector (`Rule-B`), I adjusted the style to include a font-size of 20px and font-weight of bold. However, it appears that this new rule is not superseding the original one. Subsequently, when implementing an alternative rule with a more potent selector `.slide__content .slide__caption a img + h2` while maintaining the same style attributes (`Rule-C`), it effectively overrides the initial selector. 

![2024-09-11T085916](2024-09-11T085916-6009425.jpg)

Why is the case that:

-   Styles in `Rule-B` <u>cannot</u> override styles in `Rule-A`
-   Styles in `Rule-C` <u>can</u> override styles in `Rule-A`

This is because: 

-   Specificity of selector in `Rule-B` is smaller than that of `Rule-A`
    -   `Rule-B`'s selector `.slide_content h2                 ` have specificity of `(0,0,1,1)`
    -   `Rule-A`'s selector `.slide_content .slide_caption a h2` have specificity of `(0,0,2,2)`
-   Specificity of selector in `Rule-C` is greater than that of `Rule-A`
    -   `Rule-C`'s selector `.slide_content .slide_caption a img + h2` have specificity of `(0,0,2,3)`
    -   `Rule-A`'s selector `.slide_content .slide_caption a h2      ` have specificity of `(0,0,2,2)`

I hope this example has made clear the importance of understanding the concept of "<u>**selector specificity**</u>", learning the working mechnism behind the selector specificity will help you write css rules that is both predictable and consistent, and be more efficient in debugging. 










## Reference
- [Selector 4 - 17.Calculating a selector’s specificity](https://drafts.csswg.org/selectors-4/#specificity-rules)
- [Stack Overflow - Which CSS pseudo-classes don't have specificity?](https://stackoverflow.com/questions/59362436/which-css-pseudo-classes-dont-have-specificity)
- [Mdn Web Docs - Specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity)
- [CSS TRICKS - Specifics on CSS Specificity](https://css-tricks.com/specifics-on-css-specificity/)
- [W3School - CSS Specificity](https://www.w3schools.com/css/css_specificity.asp)
---
title: "CSS Vendor Prefix (-webkit-, ms-, or moz-)"
date: "2024-02-18"
---


## What is vendor prefix ?

According to [web.simmons.edu](http://web.simmons.edu/) , vendor prefix are:

>    The process of introducing new CSS properties and HTML elements can be a long and convoluted process. Sometimes changes are proposed by "<u>standards committees</u> "(like the W3C) and other times "<u>browser vendors</u>" create their own properties.
>   Browser vendors needed a way to add support for new features that were not yet standardized, but without messing up later changes or creating incompatibles. To solve this issue Vendor Prefixes were created. A vendor prefixes is a <u>special prefix added to a CSS property</u>. Each rendering engine has it's own prefix which will only apply the property to that particular browser.


Example of vendor prefix:

| Browser           | Vendor Prefix |
| ----------------- | ------------- |
| Internet Explorer | `-ms-`        |
| Chrome            | `-webkit-`    |
| Safari            | `-webkit-`    |
| Firefox           | `-moz-`       |
| iOS               | `-webkit-`    |
| Andriod           | `-webkit-`    |
| No Vendor         | `-o-`         |



## Intuition behind vendor prefix ?

The reason we want to use such browser vendor specific css properties is because browser may support the same feature using different methods, of which might make the end-result look slightly different. Taking the porperty  `font-smoothing`  for example

-   **Webkit browser** implement options : `none`, `antialiased` and `subpixel-antialiased`
-   **Firefox browser** implement options: `auto`, `inherit`, `unset`, `grayscale`.

And even if the W3C committee proposed some standardized properties, the browser may or may not adapt the standard, and if they choose to do so, the standardization will take time and as a result different browser may adopt them on different times.

As a result, if you would like to have a finer control of the properties behavior for certain browser, say only firefox or only safari, you can do so via vendor properties. (Since in CSS, a browser simply ignores properties it does not understand, consequently the vendor properties that not belong to the current viewer's browser will get ignored)



## How should I use vendor prefix ?

To begin with, the majority of the CSS properties are supported across all mordern browser, to check that, you can use [caniuse.com](https://caniuse.com/). Taking the following check of "margin-inline" for example: we find all up-to-update modern browser (except for IE) supports this property (green).

![](./DASD8.jpg)

Secondly, if you happen to find the (standard) property not supported by all websites, but browser supported (not unprefixed), then you may use the vendor prefixed version of the property for each of the browser. (e.g. `-webkit-font-smoothing`, `-moz-font-smoothing`, `-ms-font-smoothing` , `-o-font-smoothing`... )

![](./ADU89A.jpg)

Note, you should always <u>put the standardized property last</u>. The benifit of this is that: any browser that understands it will use the last definition, overwriting any previous one.

```
// Imagine if a property -moz-xyz which is originally vendor specific to firefox browser
// The idea of `-moz-xyz` property somehow get popular and standardized into the W3C CSS property standard
// Having the `xyz` at the end of the vendor prefixed property will mean the standardized `xyz` always get used if it exists

-moz-xyz:     xxxxxyyyyyzzzz;
-webkit-xyz:  xxxxxyyyyyzzzz;
-ms-xyz:      xxxxxyyyyyzzzz;
xyz:          xxxxxyyyyyzzzz;

```

Last but not least, if you are feeling confortable exploding your CSS file, trading the browser support from performanc , you can do that via using AutoPrefixing tool such as [https://postcss.org/](https://postcss.org/).



## Why we should try not to use it ?

According to this [article](https://www.quora.com/Do-developers-still-include-vendor-prefixes-in-CSS-Besides-tools-like-Autoprefixer-what-other-tools-can-be-used/answer/Frank-M-Taylor-1?share=3bfecc91&srid=tVE5), vendor prefix are:

> The point of the vendor prefix is to indicate to the developer, “hey, this isn’t approved by the W3C, or it’s otherwise subject to change”. It’s prefixed so we can learn about it and play with it, before it becomes finalized. It’s a browser’s way of giving us a “preview” of new features.



## Reference

- [Do developers still include vendor prefixes in CSS? ](https://www.quora.com/Do-developers-still-include-vendor-prefixes-in-CSS-Besides-tools-like-Autoprefixer-what-other-tools-can-be-used/answer/Frank-M-Taylor-1?share=3bfecc91&srid=tVE5)
- [CSS Vendor Prefixes - web.simmons.edu](http://web.simmons.edu/~grovesd/comm244/notes/week6/css3-compatibility#:~:text=A%20vendor%20prefixes%20is%20a,property%20to%20that%20particular%20browser.&text=Much%20less%20necessary%2C%20but%20still%20used.)
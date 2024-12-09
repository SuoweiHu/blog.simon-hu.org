---
title: "Keyboard Tab Focus for Accessibility (tabindex)"
date: "2024-12-09"
categories: ["Accessibility"]
---



### Introduction to Concept

According to [MDN-tabindex](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex), `tabindex` is a global DOM element attribute used to indicate if the element is **keyboard focusable (via tab)** or not:

-   By setting `tabindex="-1"`,  element is not reachable via sequential keyboard navigation.
-   By setting `tabindex="0" `, the element should be focusable in sequential keyboard navigation.

*(\*p.s. You may also set other positive values such as `tabindex="2/3/4/5/..."`, to indicate the order/sequance for the focus, but generally this **<u>should be AVOIDED</u>**, due to its potential of causing difficulty for people solely relying on keyboard for navigation and those who are using other assistive technology to navigate around the page)*

![tab-tab-key](tab-tab-key.gif)


### HTML Component Focusable by Default

Some of the HTML element by default have a `tabindex=0` , these elements are:

-   `<a>` / `<area>`  : focusable only if you have the `href` attribute set, if you leave it empty it cannot be focused
-   `<input>` / `<textarea>`  : focusable when you do not have `hidden`
-   `<input>` / `<object>` / `<select>` / `<iframe>`

*(\*p.s. one exception is the `<dialog>` element, the tabindex attribute must not be used for `<dialog>` element)*



### Transform Any Component to Focusable

You may add `tabindex=0` as an attribute to any HTML component to make then focusable, for instance the below example uses jQuery to transform a `<div>` into focusable component that:

```html
<div class="hello-button-div">⌘</div>
...
<script>
    $("div.hello-button-div").onclick(()=>{
        console.log("Hello World !!!!!!!!!!!!!!!!!");
    });
    $("div.hello-button-div").each(function(){
        if ($(this).attr       ('tabindex') != '0') {
            $(this).removeAttr ('tabindex');
            $(this).attr       ('tabindex', '0');
        }
    });
...
```

You may also wanna add some styling to that button:

```html
<div class="hello-button-div">⌘</div>
...
<script>
    $("div.hello-button-div").onclick(()=>{
        console.log("Hello World !!!!!!!!!!!!!!!!!");
    });
    $("div.hello-button-div").each(function(){
        if ($(this).attr       ('tabindex') != '0') {
            $(this).removeAttr ('tabindex');
            $(this).attr       ('tabindex', '0');
        }
    });
...
<style>
    div.hello-button-div:hover,
    div.hello-button-div:focus,
    div.hello-button-div:focus-within{
        outline: 3px solid red !important;
    }
...
```

And ideally some ARIA information since `<div>` by default does not contain/provide much information for accessibility tool such as screen reader, especially here we do not even have any information within the `<div>` it self (its content is  `⌘`):

```html
<div
    role="button"
    aria-label="Hello World Button"
    aria-hidden="false"
	class="hello-button-div"
>⌘</div>
...
<script>
    $("div.hello-button-div").onclick(()=>{
        console.log("Hello World !!!!!!!!!!!!!!!!!");
    });
    $("div.hello-button-div").each(function(){
        if ($(this).attr       ('tabindex') != '0') {
            $(this).removeAttr ('tabindex');
            $(this).attr       ('tabindex', '0');
        }
    });
...
<style>
    div.hello-button-div:hover,
    div.hello-button-div:focus,
    div.hello-button-div:focus-within{
        outline: 3px solid red !important;
    }
...
```

You can find a full list of such ARIA roles and ARIA properties/attributes via: the following:

-   [MDN - ARIA Roles](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles)
-   [MDN - ARIA Properties](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Attributes)
---
title: "CSS Reset"
date: "2024-03-05"
categories: "CSS/SCSS"
---





## CSS Reset

Initially, upon exploring the web developer community using the search query "CSS Reset," you will encounter two distinct categories of articles:

- **Hard CSS Reset**:
    - The first type does a **complete reset** so that the whole website is **free from the default styling algorithm** of the client browser, as a result all components are styled the same way.
- **Soft CSS Reset**:
    - The second type aims to **normalise the styles across browsers**, this is to mitigate the issue caused by different browser applying different default rules. Such reset tries ti achieve a consistent default stylesheet throughout browser.



---



## CSS Reset Examples



### Hard CSS Reset: Eric Meyer's reset

```css
/* http://meyerweb.com/eric/tools/css/reset/  v2.0 | 20110126 License: none (public domain) */
a,abbr,acronym,address,applet,article,aside,audio,b,big,blockquote,body,canvas,caption,center,cite,code,dd,del,details,dfn,div,dl,dt,em,embed,fieldset,figcaption,figure,footer,form,h1,h2,h3,h4,h5,h6,header,hgroup,html,i,iframe,img,ins,kbd,label,legend,li,mark,menu,nav,object,ol,output,p,pre,q,ruby,s,samp,section,small,span,strike,strong,sub,summary,sup,table,tbody,td,tfoot,th,thead,time,tr,tt,u,ul,var,video{margin:0;padding:0;border:0;font-size:100%;font:inherit;vertical-align:baseline}article,aside,details,figcaption,figure,footer,header,hgroup,menu,nav,section{display:block}body{line-height:1}ol,ul{list-style:none}blockquote,q{quotes:none}blockquote:after,blockquote:before,q:after,q:before{content:'';content:none}table{border-collapse:collapse;border-spacing:0}
```

Comparison:

-   Before reset: http://web.simmons.edu/~grovesd/comm244/notes/week3/html-test-page.html
-   After reset: http://web.simmons.edu/~grovesd/comm244/notes/week4/reset-example.html

Source:

-   https://github.com/necolas/normalize.css/blob/master/normalize.css
-   https://meyerweb.com/eric/tools/css/reset/index.html



### Soft CSS Reset: Normalise.css

```css
/*! normalize.css v8.0.1 | MIT License | github.com/necolas/normalize.css */
button,hr,input{overflow:visible}progress,sub,sup{vertical-align:baseline}[type=checkbox],[type=radio],legend{box-sizing:border-box;padding:0}html{line-height:1.15;-webkit-text-size-adjust:100%}body{margin:0}details,main{display:block}h1{font-size:2em;margin:.67em 0}hr{box-sizing:content-box;height:0}code,kbd,pre,samp{font-family:monospace,monospace;font-size:1em}a{background-color:transparent}abbr[title]{border-bottom:none;text-decoration:underline;text-decoration:underline dotted}b,strong{font-weight:bolder}small{font-size:80%}sub,sup{font-size:75%;line-height:0;position:relative}sub{bottom:-.25em}sup{top:-.5em}img{border-style:none}button,input,optgroup,select,textarea{font-family:inherit;font-size:100%;line-height:1.15;margin:0}button,select{text-transform:none}[type=button],[type=reset],[type=submit],button{-webkit-appearance:button}[type=button]::-moz-focus-inner,[type=reset]::-moz-focus-inner,[type=submit]::-moz-focus-inner,button::-moz-focus-inner{border-style:none;padding:0}[type=button]:-moz-focusring,[type=reset]:-moz-focusring,[type=submit]:-moz-focusring,button:-moz-focusring{outline:ButtonText dotted 1px}fieldset{padding:.35em .75em .625em}legend{color:inherit;display:table;max-width:100%;white-space:normal}textarea{overflow:auto}[type=number]::-webkit-inner-spin-button,[type=number]::-webkit-outer-spin-button{height:auto}[type=search]{-webkit-appearance:textfield;outline-offset:-2px}[type=search]::-webkit-search-decoration{-webkit-appearance:none}::-webkit-file-upload-button{-webkit-appearance:button;font:inherit}summary{display:list-item}[hidden],template{display:none}
```

Source:

-   https://github.com/necolas/normalize.css
-   https://github.com/necolas/normalize.css/blob/master/normalize.css



### Soft CSS Reset:  Josh Comeau's Reset

```css
/* Josh's Custom CSS Reset | https://www.joshwcomeau.com/css/custom-css-reset/ */
*,::after,::before{box-sizing:border-box}*{margin:0}body{line-height:1.5;-webkit-font-smoothing:antialiased}canvas,img,picture,svg,video{display:block;max-width:100%}button,input,select,textarea{font:inherit}h1,h2,h3,h4,h5,h6,p{overflow-wrap:break-word}#__next,#root{isolation:isolate}
```

Source:

-   https://www.joshwcomeau.com/css/custom-css-reset/#one-box-sizing-model-2







---

## Reference

-   https://github.com/necolas/normalize.css/blob/master/normalize.css
-   https://meyerweb.com/eric/tools/css/reset/index.html
-   https://www.joshwcomeau.com/css/custom-css-reset/#one-box-sizing-model-2
-   https://github.com/necolas/normalize.css/blob/master/normalize.css



















## Reference

-   http://web.simmons.edu/~grovesd/comm244/notes/week4/css-reset
-   https://www.joshwcomeau.com/css/custom-css-reset/#one-box-sizing-model-2

-   https://github.com/necolas/normalize.css
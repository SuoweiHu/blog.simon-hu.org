---
title: "HTML/CSS Data Attribute"
date: 2024-09-24
categories: ["HTML", "CSS"]
---



## Intuition

It is very commmon for frontend developer like me to encounter screnario where they need to display the same component in very different style, and toggle them via javascript. Before knowing the concept of data-attirbute, often times I will perform the style change via toggling the class-name, for instance: 

```html
<!-- HTML -->
<div id="demo">HELLO WORLD</div>

<!-- CSS --> 
<style>
    div#demo:not(.active) { border-color: red;   }
    div#demo.active       { border-color: green; }
</style>

<!-- JavaScript -->
<script>
	document.querySelector('div#demo').onclick = () => {
		document.querySelector('div#demo').classList.toggle('active');
	}
</script>
```

This work well for the simple "toggling" screnario,  in such screnario, it is sufficient to use the class-name to control the styling of the component (via triggering different css rule-set). 

However, when the requirement gets more complicated, class-name's lack of ability to provide semantic information can be a huge drawback. Consider the screnario where I am writting in a template language, data stored in the website's backend will only be rendered as proper HTML through the template upon the client's visit, in order to pass style related parameters like color and width to the front-end, one might have to use css varaible: 

```html
<!-- HTML (Twig) Template --> 
<div 
     id="demo" 
     style="
            --var-background-color :{{context.bg-color.0.value}}; 
            --var-foreground-color :{{context.fg-color.0.value}}; 
            --var-width            :{{context.width.0[#context].value}}; 
            --var-height           :{{context.height.0[#context].value}}; 
           "
>HELLO WORLD</div>
	
<!-- CSS (using var) --> 
<style>
    div#demo                     { border-color: red;    }
    div#demo.active-desktop      { border-color: green;  }
    div#demo.active-mobile       { border-color: yellow; }
    div#demo{ 
        background-color: var(--var-background-color); 
        color:            var(--var-foreground-color);
        height:           var(--var-height);
        width:            var(--var-width);
    }
</style>

<!-- JavaScript -->
<script>
	document.querySelector('div#demo').onclick = () => {
        if(checkIsMobile == "mobile"){
            document.querySelector('div#demo').classList.remove('active-desktop');
            document.querySelector('div#demo').classList.toggle('active-mobile' );
        } else {
            document.querySelector('div#demo').classList.remove('active-mobile' );
            document.querySelector('div#demo').classList.toggle('active-desktop');
        }
	}
</script>
```

In the above example, although we have accounplished the goal of "piping styling information" from the backend to the style sheet, it methodology of storing everything in the style attribute definitely doesn't look elegant. Having using two class-name to control three different styling seems to start get complicated; And one can easily make a mistake when scrambling every variable in the style attribute, and can be potentially confusing if you choose to use shorter variable name.

Finally let's solve this scenario with the "new weapon" data attribute: 

```html
<!-- HTML (Twig) Template --> 
<div 
     id="demo" 
     data-active     ="none"
     data-background ="{{context.bg-color.0.value}}"
     data-foreground ="{{context.fg-color.0.value}}"
     data-width      ="{{context.width.0[#context].value}}"
     data-height     ="{{context.height.0[#context].value}}"
>HELLO WORLD</div>

<!-- CSS (using var) --> 
<style>
    div#demo[data-active="none"]      { border-color: red;    }
    div#demo[data-active="desktop"]   { border-color: green;  }
    div#demo[data-active="mobile"]    { border-color: yellow; }
    div#demo{ 
        background-color: attr(data-background);
        color:            attr(data-foreground);
        height:           attr(data-height);
        width:            attr(data-width);
    }
</style>

<!-- JavaScript -->
<script>
	document.querySelector('div#demo').onclick = () => {
        if (document.querySelector('div#demo').dataset.active != "none"){
            document.querySelector('div#demo').dataset.active = "none";
        } else {
            if(checkIsMobile == "mobile" ){ document.querySelector('div#demo').dataset.active = "mobile"; } 
            else {                          document.querySelector('div#demo').dataset.active = "desktop";}
        }
	}
</script>

```

As the above example showcased, with the help of data attribute, the sepration of content/data can be easily done without having the drawbacks. Moreover, data attributes also integrate better with JavaScript; And sometimes get used by the framworks (Vue, React, etc) to achieve unique functionalities, such as binding data, handling events, or integrating with third-party plugins.



## Accessing/Update Data Attribute via JavaScript (dataset property)

Like any other attribute you can access/update the attribute via the generic `getAttribute()`/`setAttribute()` method: 

```html
<!-- HTML -->
<div id="demo" data-name="Simon" ... >

<!-- JavaScript -->
<script>
	const _element_      = document.getElementByID("demo");
    const _element_name_ = _element_.getAttribute("data-name");           // Access Data Attribute
                           _element_.setAttribute("data-name", "Mark");   // Update Data Attribute
						   _element_.removeAttribute("data-name");        // Delete Data Attribute
</script>
```

However, JavaScript have its unique API of access any `data-*` attribute on element, via the read only `dataset` property: 

```html
<!-- HTML -->
<div id="demo" data-dateOfBirth="2000-01-01" ... >

<!-- JavaScript -->
<script>
    const _element_                = document.getElementByID("demo");
    const _element_dateOfBirth_    = _element_.dataset.dateOfBirth;    // Access Data Attribute 
    _element_.dataset.dateOfBirth  = "1960-10-03";                     // Update Data Attribute
    delete _element_.dataset.dateOfBirth;                              // Delete Data Attribute
</script>
```



## Accessing Data Attribute via CSS (attr function)

You can access the value of any attributes via `attr()` function in CSS style sheet, for instance: 

```html
<!-- HTML -->
<blockquote cite="https://mozilla.org/en-US/about/">
	Mozilla makes browsers, apps, code and tools that put people before profit.
</blockquote>
<blockquote cite="https://web.dev/about/">
	Google believes in an open, accessible, private, and secure web.
</blockquote>

<!-- CSS --> 
<style>
    blockquote::after {
      display: block;
      content: ' (source: ' attr(cite) ') ';
      color: hotpink;
    }
</style>
```

(Final outcome: [example-1.html](example-1.html))

Similarly you can do that for the data attribute: 

```html
<!-- HTML -->
<h1>Secret agents</h1>
<ul>
  <li data-id="10784">Jason Walters, 003: Found dead in "A View to a Kill".</li>
  <li data-id="97865">Alex Trevelyan, 006: Agent turned terrorist leader; James' nemesis in "Goldeneye".</li>
  <li data-id="45732">James Bond, 007: The main man; shaken but not stirred.</li>
</ul>


<!-- CSS --> 
<style>
    li:after {
      content: 'Data ID: ' attr(data-id);
      position: absolute;
      top: -22px;
      left: 10px;
      background: black;
      color: white;
      padding: 2px;
      border: 1px solid #eee;
      opacity: 0;
      transition: 0.5s opacity;
    }
    li:hover:after {
      opacity: 1;
    }
</style>
    
```

(Final outcome: [example-2.html](example-2.html), hover over the securet to see the effect of `::after`)



## Reference 

-   [Mdn web docs - data-*](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/data-*)
-   [Mdn web docs - attr()](https://developer.mozilla.org/en-US/docs/Web/CSS/attr)
-   [Mdn web docs - HTMLElement: dataset property](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/dataset)
-   [CSS-Tricks - HTML Data Attributes Guide](https://css-tricks.com/a-complete-guide-to-data-attributes/)
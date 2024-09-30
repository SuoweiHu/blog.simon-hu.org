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
        const ele = document.querySelector('div#demo');
        if(ele.dataset.active != "none"){
            ele.dataset.active = none;
        } else {
            if(checkIsMobile == "mobile" ){ document.querySelector('div#demo').dataset.active = "mobile"; } 
            else {                          document.querySelector('div#demo').dataset.active = "desktop";}
        }
	}
</script>

```













Sometimes I  

to display the same component in a sligntly differnet style, 

control the specific action of that 

twig template ????
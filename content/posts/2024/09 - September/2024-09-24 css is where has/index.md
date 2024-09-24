---
title: "CSS Functional Pseudo-Classes: :is and :where "
date: 2024-09-24
categories: ["CSS"]
---





>   ##  **TLDR**
>
>   -   Always use `:is` , never use `:where`
>   -   The only exception is that if you are writting your own "CSS Reset" file, then you may use `:where`.





## Similarities

Both `:is` and `:where` peseudo selector matches element based on a list of selectors, they allow you to group selectors together and apply styles to any element that matches any of the selectors in the list. For instance imagine we have multiple `<input>` child component wrapped in two different `<form>` parent comopnent, and we want to select them all based on their the form's classname and input's type attribute. 

```html
<!-- HTML ====================================================== -->
<div class="content-container">
    <div class="form-container">
        <form class="form-primary" action="/submit-form" method="post">
            <!-- Text Input -->
            <label for="name">Name:</label>
            <input type="text" id="name" name="name" required>
            <!-- Email Input -->
            <label for="email">Email:</label>
            <input type="email" id="email" name="email" required>
            <!-- Password Input -->
            <label for="password">Password:</label>
            <input type="password" id="password" name="password" required>
            <!-- Date Input -->
            <label for="dob">Date of Birth:</label>
            <input type="date" id="dob" name="dob">
            <!-- Submit Button -->
            <button type="submit">Submit</button>
        </form>
         <form class="form-secondary" action="/submit-form" method="post">
            <!-- Text Input -->
            <label for="name">Name:</label>
            <input type="text" id="name" name="name" required>
            <!-- Email Input -->
            <label for="email">Email:</label>
            <input type="email" id="email" name="email" required>
            <!-- Password Input -->
            <label for="password">Password:</label>
            <input type="password" id="password" name="password" required>
            <!-- Date Input -->
            <label for="dob">Date of Birth:</label>
            <input type="date" id="dob" name="dob">
            <!-- Submit Button -->
            <button type="submit">Submit</button>
        </form>
    </div>
</div>


<!-- CSS without is/where ====================================== --> 
<style>
	div.content-container > div.form-container > form.form-primary   > input[for="name"],
    div.content-container > div.form-container > form.form-primary   > input[for="email"],
    div.content-container > div.form-container > form.form-primary   > input[for="password"],
    div.content-container > div.form-container > form.form-primary   > input[for="date"],
    div.content-container > div.form-container > form.form-secondary > input[for="name"],
    div.content-container > div.form-container > form.form-secondary > input[for="email"],
    div.content-container > div.form-container > form.form-secondary > input[for="password"],
    div.content-container > div.form-container > form.form-secondary > input[for="date"] {
    	box-shadow: rgba(100, 100, 111, 0.2) 0px 7px 29px 0px;
		boder-radius: 10px;
    	border: 5px dotted #F9B455 !important;
    }
</style>

<!-- CSS with "is" ============================================== --> 
<style>
	div.content-container > div.form-container > form:is(.form-primary,.form-secondary) > input:is([for="name"], [for="email"], [for="password"], [for="date"]) {
    	box-shadow: rgba(100, 100, 111, 0.2) 0px 7px 29px 0px;
		boder-radius: 10px;
    	border: 5px dotted #F9B455 !important;
    }
</style>

<!-- CSS with "where" ============================================ --> 
<style>
	div.content-container > div.form-container > form:where(.form-primary,.form-secondary) > input:where([for="name"], [for="email"], [for="password"], [for="date"]) {
    	box-shadow: rgba(100, 100, 111, 0.2) 0px 7px 29px 0px;
		boder-radius: 10px;
    	border: 5px dotted #F9B455 !important;
    }
</style>
```



## Difference

The difference between the two functional Pseudo-Classes is the specificity: 

-   `:is` will add the same specificity as its inner most specific selector (within the bracket) to the overall selector 
-   `:where` contribute no specificity (irrelevant of the selector within the bracket) to the overall selector, which can be useful when you want to apply styles to a group of elements without increasing the specificity.

For instance: 

```
#node-search div.content > ul > li:is(#item-873, li.item-hidden, li:last-of-type){


Specificity:                                (0,2,1,3)    sum of below 
→ #node-search:                                          → (0,1,0,0)
→ div.content:                                           → (0,0,1,1)
→ ul:                                                    → (0,0,0,1)
→ li:                                                    → (0,0,0,1)
→ :is(#item-873, li.item-hidden, li:last-of-type)        → (0,1,0,0)    max of below 
  ⤷ #item-873                                                            ⤷ (0,1,0,0)
  ⤷ li.item-hidden                                                       ⤷ (0,0,1,1)
  ⤷ li:last-of-type                                                      ⤷ (0,0,0,2)
```

```
#node-search div.content > ul > li:where(#item-873, li.item-hidden, li:last-of-type){


Specificity:                                (0,1,1,3)    sum of below 
→ #node-search:                                          → (0,1,0,0)
→ div.content:                                           → (0,0,1,1)
→ ul:                                                    → (0,0,0,1)
→ li:                                                    → (0,0,0,1)
→ :where(#item-873, li.item-hidden, li:last-of-type)     → (0,0,0,0)    always zero
```

And as a result they will appear different usecases, which is explained well in [this post](https://www.sitepoint.com/css-is-where-has-pseudo-class-selectors/).













## Reference
- [How the CSS :is, :where and :has Pseudo-class Selectors Work](https://www.sitepoint.com/css-is-where-has-pseudo-class-selectors/)
- [mdn web docs :where](https://developer.mozilla.org/en-US/docs/Web/CSS/:where)
- [mdn web docs :is](https://developer.mozilla.org/en-US/docs/Web/CSS/:is)
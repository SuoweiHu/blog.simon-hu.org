---
title: "CSS Grid Layout"
date: "2024-12-22"
categories: ["CSS"]
---

>   **Disclaimer**: This post is primarily written as a personal reference note and is not intended as professional or formal content. Much of the material has been directly copied from various sources for my own learning purposes. The language used is casual and unpolished. This is essentially my digital notebook - use at your own discretion. All credit goes to the original sources referenced below.

## Intuition

The concept of CSS Grid gained prominence during discussions about its sub-grid functionality, which enables precise alignment of elements within multiple uniform components. Upon investigating the principles of grid layout and comparing it to Flexbox, [Codedamn's article](https://codedamn.com/news/frontend/difference-between-flexbox-and-css-grid) highlights several advantages of implementing Grid over Flexbox:

-   **Dimensionality**: Two-dimensional, both rows and columns *(vs One-dimensional)*
-   **Layout Basis**: Structure-driven *(vs Content-driven)*
-   **Alignment**: Aligns items along both axes *(Aligns items along a single axis)*
-   **Complexity**: Better for complex layouts *(Simpler for straightforward layouts)*
-   **Responsiveness:** Supports dynamic grid resizing *(Adapts content flexibly to space)*
-   **Overlapping Items**: Allows overlapping elements *(Requires hacks for overlapping)*

Until now, I have mostly been a flex-only person in my day-to-day job. I think it might be time for me to finally take a bit on this hard bone, so I can potentially make it part of my daily coding.

---

## Terminologies 

Below is a image that contains the majority of the terminologies above for illustration purpose (illustration from [webkit.org](https://webkit.org/blog/7434/css-grid-layout-a-new-layout-module-for-the-web/), explainations from [mdn web docs](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_grid_layout/Basic_concepts_of_grid_layout) and [css-tricks](https://css-tricks.com/snippets/css/complete-guide-grid/)): 

![CSS Grid Layout: A New Layout Module for the Web | WebKit](grid-concepts.svg)

### Grid Container & Grid Items (parent/child)

-   **MDN**: We create a *grid container* by declaring `display: grid` or `display: inline-grid` on an element. As soon as we do this, all *direct children* of that element become grid items.
-   **CSS-TRICK**: The element on which `display: grid` is applied. It’s the direct parent of all the grid items. In this example `container` is the grid container.The children (i.e. *direct* descendants) of the grid container. Here the `item` elements are grid items, but `sub-item` isn’t.

### Grid Track (row/column)

-   **MDN**: We define rows and columns on our grid with the `grid-template-rows` and `grid-template-columns` properties. These define grid tracks. A grid track is the space between any two adjacent lines on the grid.
-   **CSS-TRICK**: The space between two adjacent grid lines. You can think of them as the columns or rows of the grid. Here’s the grid track between the second and third-row grid lines.

### Grid Line

-   **MDN**: It should be noted that when we define a grid we define the grid tracks, not the lines. Grid then gives us numbered lines to use when positioning items.
-   **CSS-TRICK**: The dividing lines that make up the structure of the grid. They can be either vertical (“column grid lines”) or horizontal (“row grid lines”) and reside on either side of a row or column. Here the yellow line is an example of a column grid line.

### Grid Cells

-   **MDN**: A grid cell is the smallest unit on a grid. Conceptually it is like a table cell. 

    

### CSS-TRICK

-   The space between two adjacent row and two adjacent column grid lines. It’s a single “unit” of the grid. Here’s the grid cell between row grid lines 1 and 2, and column grid lines 2 and 3.

### Grid Area

-   **MDN**: Items can span one or more cells both by row or by column, and this creates a grid area.
-   **CSS-TRICK**: The total space surrounded by four grid lines. A grid area may be composed of any number of grid cells. Here’s the grid area between row grid lines 1 and 3, and column grid lines 1 and 3.

### Gutter

-   Gutters or alleys between grid cells can be created using the `column-gap` and `row-gap` properties, or the shorthand `gap`.



---

## Basic Usage 

### Grid Container Template

As a entry-level example, you can simply have a contrainer with multiple items inside, declare the container as a grid container via `display:grid` and its template column grid tracks via `grid-template-column` property, and in the property, you may give nave for the grid lines on ease-side of the track (so that you won't have to use number, but string formatted name instead). 

Blow are some of the examples, you can use play around using this file as the starting point: [example-grid-template-column.html](example-grid-template-column.html)

![grid-template-1](grid-template-1.png)

![grid-template-2](grid-template-2.png)

![named-grid-line-2](named-grid-line-1.png)

![named-grid-line-2](named-grid-line-2.png)

### Grid Auto-Wrapping / Responsive

You may want grid layout to automatically pick the number of columns for you based on the available space horizontally to achieve a responsive design for varies devices, this can be achieved via a combination of `auto-fill` and `minmax(a,b)` function All without using media query to define different `grid-template-column` for each breakpoint (original file: [example-autofit-minmax.html](example-autofit-minmax.html)): 

```css
grid-template-columns: repeat(auto-fill, minmax(500px, 1fr));
```

![2024-12-22T113327](2024-12-22T113327.gif)

 *(p.s. historically, there was a weakness here is that first value in `minmax()` (the 10rem value above). If the container is narrower than whatever that minimum is, elements in that single column will overflow. If you encounter this situation via `grid-template-columns: repeat(auto-fill, minmax(min(10rem, 100%), 1fr));`. (Ref: https://css-tricks.com/intrinsically-responsive-css-grid-with-minmax-and-min/)*

### Grid Item Placement (Manual)

You can place grid-item with its container by defining its start/end grid-line using one of the following css attributes: 

-   full declaration version: 
    -   **Row (= Y-Axis)**: `grid-row-start`, `grid-row-end`
    -   **Column (= X-Axis)**: `grid-column-start`, `grid-column-end`
-   shorthand version: 
    -   two attributes: `grid-column: col-start/col-end` , `grid-row: row-start/row-end`
    -   one attribute: `grid-area: row-start/col-start/row-end/col-end`

Note that:

-   you may use `span` keyword to declare the number of cells you would want a grid item to occupy, if you do that then the grid will automatically place the item within the next available space that can fit the item; For example `grid-area: span 2/span 3` is declaring that item having 2 
-   *you may use `positive`/ `negative indexes` for the start/end grid-line-number, or use the `grid-line name` you declared in the template; For example `grid-column-template: [hello] 100px [world] ...` then you can declare an grid column for a item using `grid-column: hello / world`)* 

-   you may place/cover/layer one grid-item on another, and control who's on top/bottom using the `z-index` css attribute (please see `item-3` and `item-4` in the below screenshot)

Please find the example of usage below: 

![2024-12-23T105117](2024-12-23T105117.png)

(the original file can be found at: [example-grid-item-placement.html](example-grid-item-placement.html))



### Grid Item Placement (Auto-Flow)

By default if you do not specify the placement of the item, it will occupy 1 cell of a grid area on the next available row/horizontal/x-axis space, and you may change the behavior via the `grid-auto-flow:column/row` css attribute on the grid-container: 

![2024-12-23T105914](2024-12-23T105914.gif)



### Grid Gutter (Gap)

You may define the spacing between each grid cells via one of the following: `column-gap`, `row-gap`, `gap`: 

![2024-12-23T110729](2024-12-23T110729.png)



### Grid Container Area

You may define the grid area template in the grid container, and place grid items on a area basis: 

![2024-12-23T114842](2024-12-23T114842.png)

(file can be found: [example-grid-area.html](example-grid-area.html)



### Grid Justify & Align

*(\*p.s.* 

-   ***Justify**: horizontal direction along the x-axis (or inline/row direction)*

- ***Align**: vertical direction along the y-axis (or block/column direction)*

#### Justify & Align of the Items within Grid 

![2024-12-23T115536](2024-12-23T115536.png)

```
.container           { justify-items: start/end/center/strech }
.container           {  align-items:  start/end/center/strech } 
.container > .item-x { justify-self:  start/end/center/strech } 
.container > .item-y {   align-self:  start/end/center/strech } 
```

#### Justify & Align of Grid Container's Columns/Rows

![2024-12-23T115654](2024-12-23T115654.png)

![2024-12-23T120238](2024-12-23T120238.png)

(Preety much like the flex `justify-content/align-items`

```
.container{ justify-content: start | end | center | stretch | space-around | space-between | space-evenly;  
.container{   align-content: start | end | center | stretch | space-around | space-between | space-evenly;  
```



---

## Reference
CSS Grid Basics 
- [CSS-TRICKS - CSS Grid Layout Guide](https://css-tricks.com/snippets/css/complete-guide-grid/#aa-properties-for-the-childrengrid-items)
- [CSS-TRICKS - CSS Grid Layout PDF CheatSheet](https://css-tricks.com/wp-content/uploads/2022/02/css-grid-poster.png)
- [Mdn web docs - Basic concepts of grid layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_grid_layout/Basic_concepts_of_grid_layout)
- [Slaying The Dragon - Learn CSS Grid - A 13 Minute Deep Dive](https://www.youtube.com/watch?v=EiNiSFIPIQE)

CSS Grid Extended Knowledge 

- [Codedamn - CSS Grid vs Flex](https://codedamn.com/news/frontend/difference-between-flexbox-and-css-grid)
- [Intrinsically Responsive CSS Grid with minmax() and min()](https://css-tricks.com/intrinsically-responsive-css-grid-with-minmax-and-min/) (maybe deprecated and may no longer apply)

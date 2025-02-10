---
title: "Common CSS Media Query Breakpoint"
date: "2024-02-26"
tags: ["CSS/SCSS"]
---



---

## Breakpoint in Drupal CMS

(The below breakpoint are concluded only from my expereience, and is not found anywhere on the standardized documentation

| **Device**   | **Upper bound (px)** | **Lower bound (px)** | Container Width (px) | Media Query                                                |
| ------------ | -------------------- | -------------------- | -------------------- | ---------------------------------------------------------- |
| `desktop-lg` | ∞                    | 1400                 | 1320                 | `@media (min-width:1400px)  {...}`                         |
| `desktop-md` | 1399                 | 1200                 | 1140                 | `@media (max-width:1399px)  and (min-width:1200px)  {...}` |
| `desktop-sm` | 1199                 | 1024                 | 960                  | `@media (max-width:1199px)  and (min-width:1024px)  {...}` |
| `mobile-lg`  | 1023                 | 768                  | 720                  | `@media (max-width:1023px)  and (min-width:768px)   {...}` |
| `mobile-md`  | 767                  | 576                  | 540                  | `@media (max-width:767px)   and (min-width:576px)   {...}` |
| `mobile-sm`  | 575                  | 0                    | Auto (100%)          | `@media (max-width:575px) {...}`                           |



Combined Version for ease of `Ctrl+C` and `Ctrl+V`:

```css
@media                         (min-width:1400px)  {...}
@media (max-width:1399px)  and (min-width:1200px)  {...}
@media (max-width:1199px)  and (min-width:1024px)  {...}
@media (max-width:1023px)  and (min-width:768px)   {...}
@media (max-width:767px)   and (min-width:576px)   {...}
@media (max-width:575px)                           {...}
```



----

## Breakpoints from Popular CSS Frameworks

### Bootstrap4 - default breakpoints

| Breakpoint        | Dimensions |
| ----------------- | ---------- |
| X-Small           | < 576px    |
| Small             | ≥ 576px    |
| Medium            | ≥ 768px    |
| Large             | ≥ 992px    |
| Extra large       | ≥ 1200px   |
| Extra extra large | ≥ 1400px   |



### Tailwind - default breakpoints

| Key   | CSS Media Query                         | Applies     |
| ----- | --------------------------------------- | ----------- |
| none  | none                                    | **< 640px** |
| `sm`  | `@media (min-width: 640px) { ... }`     | ≥**640px**  |
| `md`  | `@media screen and (min-width: 768px)`  | ≥**768px**  |
| `lg`  | `@media screen and (min-width: 1024px)` | ≥**1024px** |
| `xl`  | `@media screen and (min-width: 1280px)` | ≥**1280px** |
| `2xl` | `@media screen and (min-width: 1536px)` | ≥**1536px** |



### PureCSS - default breakpoints

| Key    | CSS Media Query                         | Applies     |
| ------ | --------------------------------------- | ----------- |
| none   | none                                    | **< 568px** |
| `sm`   | `@media screen and (min-width: 35.5em)` | ≥**568px**  |
| `md`   | `@media screen and (min-width: 48em)`   | ≥**768px**  |
| `lg`   | `@media screen and (min-width: 64em)`   | ≥**1024px** |
| `xl`   | `@media screen and (min-width: 80em)`   | ≥**1280px** |
| `xxl`  | `@media screen and (min-width: 120em)`  | ≥**1920px** |
| `xxxl` | `@media screen and (min-width: 160em)`  | ≥**2560px** |
| `x4k`  | `@media screen and (min-width: 240em)`  | ≥**3840px** |





---

## Reference

-   [https://blog.logrocket.com/css-breakpoints-responsive-design/](https://blog.logrocket.com/css-breakpoints-responsive-design/)
















---
title: "Hugo PowerMod: Custom CSS"
date: "2024-02-12"
tags: ["Hugo"]
---


## (From official document) Bundling Custom css with theme’s assets

For adding custom css to be bundled inside one minimized css:
Create folder & file in your project directory as
```
.(site root)
├── config.yml
├── content/
├── theme/hugo-PaperMod/
└── assets/
    └── css/
        └── extended/  <---
            ├── custom_css1.css <---
            └── any_name.css   <---

(All css files inside assets/css/extended will be bundled !)
```

Note: `blank.css` is just the placeholder so that it doesn’t break the theme when no files are present under assets/css/extended



## Reference
- [https://adityatelange.github.io/hugo-PaperMod/posts/papermod/papermod-faq/#bundling-custom-css-with-themes-assets](https://adityatelange.github.io/hugo-PaperMod/posts/papermod/papermod-faq/#bundling-custom-css-with-themes-assets)
- [https://discourse.gohugo.io/t/papermod-theme-how-to-add-custom-css/30165/11](https://discourse.gohugo.io/t/papermod-theme-how-to-add-custom-css/30165/11)
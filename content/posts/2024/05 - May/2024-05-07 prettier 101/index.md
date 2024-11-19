---
title: "Prettier 101 - [PENDING]"
date: "2024-05-07"
tags: ["Prettier"]
---



**THIS POST IS PENDING MORE EXPLORATION....**



## My `.prettier` file

```
"tabWidth": 4              # How many spaces is used for a single tab
"useTabs": true            # Use tab instead of space for indentation
"singleQuote": false       # Convert all single quote into doubel quote if possible
"insertPragma": false      # Do not insert the relevant @format/@prettier marker at the top of files when formatting
"requirePragma": false     # Does the file need to have @format/@prettier marker to be formatted ?
"arrowParens": "always"    # Transform any single parameter function such as x=>x into (x)=>x
"bracketSpacing": true     # If true: { foo: bar }; If false: {foo: bar}
```





## Prettier vs. Linters

**<u>How does it compare to ESLint/TSLint/stylelint, etc.?</u>**

(https://prettier.io/docs/en/comparison)

>   Linters have two categories of rules:
>
>   **Formatting rules**: eg: [max-len](https://eslint.org/docs/rules/max-len), [no-mixed-spaces-and-tabs](https://eslint.org/docs/rules/no-mixed-spaces-and-tabs), [keyword-spacing](https://eslint.org/docs/rules/keyword-spacing), [comma-style](https://eslint.org/docs/rules/comma-style)…
>
>   Prettier alleviates the need for this whole category of rules! Prettier is going to reprint the entire program from scratch in a consistent way, so it’s not possible for the programmer to make a mistake there anymore :)
>
>   **Code-quality rules**: eg [no-unused-vars](https://eslint.org/docs/rules/no-unused-vars), [no-extra-bind](https://eslint.org/docs/rules/no-extra-bind), [no-implicit-globals](https://eslint.org/docs/rules/no-implicit-globals), [prefer-promise-reject-errors](https://eslint.org/docs/rules/prefer-promise-reject-errors)…
>
>   Prettier does nothing to help with those kind of rules. They are also the most important ones provided by linters as they are likely to catch real bugs with your code!
>
>   In other words, use **Prettier for formatting** and **linters for catching bugs!**



## Prittier Configuration

(https://prettier.io/docs/en/configuration)

>   You can configure Prettier via (in order of precedence):
>
>   -   A `"prettier"` key in your `package.json` file.
>   -   A `.prettierrc` file written in JSON or YAML.
>   -   A `.prettierrc.json`, `.prettierrc.yml`, `.prettierrc.yaml`, or `.prettierrc.json5` file.
>   -   A `.prettierrc.js`, or `prettier.config.js` file that exports an object using `export default` or `module.exports` (depends on the [`type`](https://nodejs.org/api/packages.html#type) value in your `package.json`).
>   -   A `.prettierrc.mjs`, or `prettier.config.mjs` file that exports an object using `export default`.
>   -   A `.prettierrc.cjs`, or `prettier.config.cjs` file that exports an object using `module.exports`.
>   -   A `.prettierrc.toml` file.
>
>   The configuration file will be resolved starting from the location of the file being formatted, and searching up the file tree until a config file is (or isn’t) found.
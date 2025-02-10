---
title: "[Note] Compile SCSS file using Laravel Mix"
date: 2025-02-10

---


## Install Laravel Mix and SASS Dependencies

```bash
npm install laravel-mix sass sass-loader  --save-dev #install in current directory
npm install laravel-mix sass sass-loader  --global   #install in gloabal directory
```

## Create Larvel Mix Configuration File

create a new file `webpack.mix.js` in the root of the project

```js
const mix = require('laravel-mix');
mix.sass('scss/style.scss', 'css/style.css');
mix.options({processCssUrls: false});
if (!mix.inProduction()) { mix.sourceMaps(); }  // Enable source maps for development
```

## Create Package.json File
create a new file `package.json` in the root of the project

```json
{
    "scripts": {
        "dev": "npm run development",
        "development": "mix",
        "watch": "mix watch",
        "prod": "npm run production",
        "production": "mix --production"
    },
    "dependencies": {
        "laravel-mix": "^6.0.49",
        "sass": "^1.84.0",
        "sass-loader": "^16.0.4"
    }
}
```

## Compile SCSS File
compile or wathc compile scss file with different commands
```bash
npm run dev    # compile scss file once
npm run watch  # compile scss file and watch for changes
npm run prod   # compile scss file for production
```

## Reference
- [WebWash - Showdown of Bootstrap 5 Themes in Drupal](https://youtu.be/nuxOZU0Jw6o?t=3557)
- [Larvel Mix Documentation](https://laravel-mix.com/docs/6.0/installation)
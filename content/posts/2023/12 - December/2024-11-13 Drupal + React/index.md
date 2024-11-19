---
title: "React/Vue Framework Component in Drupal"
date: 2024-11-13
tags: ["Drupal"]
---



## Intuition

The notion has repeatedly occurred to me since I first entered the Drupal industry, where I have observed numerous online tutorials and blog posts asserting the necessity of frameworks such as Vue and React. These resources often emphasize that beginners, like I was at the time, should familiarize themselves with these technologies. Amidst the enthusiasm for these new frameworks, there exists a tendency to disparage traditional content management systems (CMS) such as WordPress, which are frequently characterized in bleak terms as an "old, dying whale." This rhetoric raises significant concerns about my future in the field. Which has lead to today's topic, are we allowed to integrate framework like react into drupal, enabling me to fulfill the commitments made by my agency to our clients while simultaneously exploring and learning React (and other front-end frameworks) in the process.



## Setup Process Breakdown

### Overview

In order to have drupal render a react component, there're three steps we will need to undertake:

-   **Step-1**: have Drupal outputting a html DOM element that contains data (that will be later used by the React component to render the styled component), and this is achievable via parargraph module + a custom theme's `twig` template.
-   **Step-2**: create the corresponding `js`/`jsx`/`ts` file that rendered the DOM element with data into a styled component, and use the appropriate bundler (for instance web-pack) to render these files into vanilla javasctipt that can be ran on browser.
-   **Step-3**: add the rendered single javasctipt file into the custom theme's library, and attach it to the relevant `twig` template

### Step-1: output DOM element

```twig
{# ================================ #}
{# EXAMPLE TWIG TEMPLATE FOR A TILE #}
{# ================================ #}

{% set unique_id        = random()                                                    %}
{% set base_url         = url('<front>', {}, { 'absolute': true })                    %}
{% set data_title       = content["field_txt_title"][0]["#context"].value             %}
{% set data_description = content["field_txt_description"][0]["#context"].value       %}
{% set data_link        = content["field_link"][0]["#title"]                          %}
{% set data_img_src     = content["field_media_image"].0["#media"]|file_uri|file_url  %}
{% set data             = "{"
                           ~ "\"id\":"          ~ "\"" ~ unique_id        ~ "\","
                           ~ "\"title\":"       ~ "\"" ~ data_title       ~ "\","
                           ~ "\"description\":" ~ "\"" ~ data_description ~ "\","
                           ~ "\"link\":"        ~ "\"" ~ data_link        ~ "\","
                           ~ "\"img_src\":"     ~ "\"" ~ data_img_src     ~ "\"}" %}
{% block paragraph %}
    <div style="background-color:lightgray;height:600px;width:100%;display:flex;justify-content:center;align-items:center;">
        <react-tile-component id="{{unique_id}}" data-json="{{data}}"/>
    </div>
{% endblock paragraph %}
```

### Step-2: Framework Related Code & Bundler

```js
// =====================================
// FILE TILE/index.jsx (REACT COMPONENT)
// =====================================

// importing reuqired libraryies
import React        from 'react';
import ReactDOM     from 'react-dom/client';
import Card         from '@mui/material/Card';
import CardActions  from '@mui/material/CardActions';
import CardContent  from '@mui/material/CardContent';
import CardMedia    from '@mui/material/CardMedia';
import Button       from '@mui/material/Button';
import Typography   from '@mui/material/Typography';

// Constructor for tile of well defined attributes/variables & render function
class Tile {
    constructor(data_json) {
      this.title        = data_json.title;
      this.description  = data_json.description;
      this.link         = data_json.link;
      this.img_src      = data_json.img_src;
    }
    renderTile_ver1(){
        return (
            <div style={{width:"300px", height:"500px", background:"gray", overflow:"hidden"}}>
                <a href={this.link}>
                    <img src={this.img_src} style={{height:"250px"}}/>
                    <h2>{this.title      } </h2>
                    <p> {this.description } </p>
                </a>
            </div>
        );
    }
    renderTile_ver2(){
        return(
            <Card sx={{ maxWidth: 345 }}>
                <CardMedia
                sx={{ height: 250 }}
                image={this.img_src}
                />
                <CardContent>
                    <Typography gutterBottom variant="h5" component="div">
                        {this.title}
                    </Typography>
                    <Typography variant="body2" sx={{ color: 'text.secondary' }}>
                        {this.description }
                    </Typography>
                </CardContent>
                <CardActions>
                    <Button href={this.link} size="small">Learn More</Button>
                </CardActions>
            </Card>
        );
    }
    render(){
        return this.renderTile_ver2();
    }
}

console.log(">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>");

document.querySelectorAll('react-tile-component').forEach((dom_component) => {
    // Getting data from the twig rendered html
    const data_jsonString  = dom_component.dataset.json;
    const data_json        = JSON.parse(data_jsonString);
                             console.log(data_jsonString);
                             console.log(data_json);
    // Initialize new tile object, and render component
    const tile = new Tile(data_json);
    ReactDOM.createRoot(dom_component).render(tile.render());
});

console.log("<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<");
```

```javascript
// =======================================
// FILE webpack.config.json FOR JS BUNDLER
// =======================================

const path = require('path');
const isDevMode = process.env.NODE_ENV !== 'production';
const WebpackShellPluginNext = require('webpack-shell-plugin-next');

module.exports = {
  entry: {
    tile: ["./js/src/tile/index.jsx"]
  },
  devtool: (isDevMode) ? 'source-map' : false,
  mode: (isDevMode) ? 'development' : 'production',
  output: {
    path: isDevMode ? path.resolve(__dirname, "js/dist_dev") : path.resolve(__dirname, "js/dist"),
    filename: '[name].min.js'
  },
  resolve: {
    extensions: ['.js', '.jsx', '.ts'],
  },
  module: {
    rules: [
      {
        test: /\.jsx?$/,
        loader: 'babel-loader',
        exclude: /node_modules/,
        include: path.join(__dirname, 'js/src'),
      }
    ],
  },
  plugins: [
    new WebpackShellPluginNext({
      onBuildEnd: {
        scripts: ['cd ../../.. && vendor/bin/drush cr;'],
        blocking: false,
        parallel: true
      }
    })
  ],
};
```

```
# ==================================
# INSTALL DEPENDENCIES AND RUN BUILD
# ==================================

> npm install --save-dev @babel/core @babel/preset-env @babel/preset-react babel-loader webpack webpack-cli
> npm install --save react react-dom prop-types
> npm install @mui/icons-material
> npm run build
```



### Step-3: Bundled JavaScript as Livrary

```yaml
# =============================================================
# FILE theme_name.libraries.yaml TO MAKE JS VIABLE AS A LIBRARY
# =============================================================

lib_paragraph_tile:
  version: VERSION
  js:
    js/dist_dev/tile.min.js: {minified: true}
```

```twig
{# =================================== #}
{# TWIG TEMPLATE WITH LIBRARY ATTACHED #}
{# =================================== #}

{% set unique_id        = random()                                                    %}
{% set base_url         = url('<front>', {}, { 'absolute': true })                    %}
{% set data_title       = content["field_txt_title"][0]["#context"].value             %}
{% set data_description = content["field_txt_description"][0]["#context"].value       %}
{% set data_link        = content["field_link"][0]["#title"]                          %}
{% set data_img_src     = content["field_media_image"].0["#media"]|file_uri|file_url  %}
{% set data             = "{"
                           ~ "\"id\":"          ~ "\"" ~ unique_id        ~ "\","
                           ~ "\"title\":"       ~ "\"" ~ data_title       ~ "\","
                           ~ "\"description\":" ~ "\"" ~ data_description ~ "\","
                           ~ "\"link\":"        ~ "\"" ~ data_link        ~ "\","
                           ~ "\"img_src\":"     ~ "\"" ~ data_img_src     ~ "\"}" %}
{% block paragraph %}
    <div style="background-color:lightgray;height:600px;width:100%;display:flex;justify-content:center;align-items:center;">
        <react-tile-component id="{{unique_id}}" data-json="{{data}}"/>
    </div>
{% endblock paragraph %}

{{ attach_library("react_theme/lib_paragraph_tile") }}

```

### Final Outcome & Example Code

The final outcome and the example code can be found as the following:

-   [example - outcome screenshot ](2024-11-17T200123.png)
-   [example - custom theme](example_custom_theme.zip)



## Reference

-   [React for Drupal](https://reactfordrupal.com/)
-   [Drupalize Me - Connect React to a Drupal Theme or Module](https://drupalize.me/tutorial/connect-react-drupal-theme-or-module)
-   [Data Binding in React](https://www.joshwcomeau.com/react/data-binding/)
-   [Add React to an Existing Project](https://react.dev/learn/add-react-to-an-existing-project)
-   [Adding assets (CSS, JS) to a Drupal module via *.libraries.yml](https://www.drupal.org/docs/develop/creating-modules/adding-assets-css-js-to-a-drupal-module-via-librariesyml#s-attaching-a-library-to-pages)
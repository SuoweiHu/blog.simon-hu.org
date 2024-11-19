---
title: "VS Code Custom Color Theme"
date: "2023-11-14"
# tags: ["VS Code", "Color Theme"]
# tags: ["VS Code"]
---

## Customizing Color Theme

### Themes from the market

Keeping this section for the sake of clean article structure, I will not spend any words on this one, if you have any questions simply refer to Google or the following official documentation:
> Reference:
> - [VS Code Documentation - Color Themes from the Marketplace](https://code.visualstudio.com/docs/getstarted/themes#_color-themes-from-the-marketplace)
> - [VS Code Documentation - Selecting the Color Theme](https://code.visualstudio.com/docs/getstarted/themes#_selecting-the-color-theme)
> - [VS Code Documentation - Auto Switching based on OS Color Theme](https://code.visualstudio.com/docs/getstarted/themes#_auto-switch-based-on-os-color-scheme)

### Theme Customization in Settings.json

The main focus of this section will be explaining how to customize your existing theme (ones you downloaded and installed from the market place), and list some of the most commonly customized components. The official documentation is here for a quick reference purpose: [Customizing Color Theme](https://code.visualstudio.com/docs/getstarted/themes#_customizing-a-color-theme).

Overall, in order to customize your theme, you will need to use keyword "`workbench.colorCustomization`" (for the purpose of changing editor UI element coloring) and "`editor.tokenColorCustomization`" (for the purpose of changing syntax highlighting colors) in the user "settings.json".

#### UI Component

To change the **"UI Element"** coloring such as the panel color for file exporer, activity bar, notinication, scroll bar, split view, buttons and more, use `workbench.colorCustomization`; The official documentation of this can be found at: [Workbench Colors](https://code.visualstudio.com/docs/getstarted/themes#_workbench-colors).

For instance, if you would like to change the color of the **sidebar** and **activity bar**, and you only want it to apply when you have selected the color theme **Ayu Dark**, you can do that via adding the following lines in the settings.json:

```json
{
	...
	"workbench.colorCustomizations": {
        "[Ayu Dark]": {
            "sideBar.background": "#DEB661",
            "activityBar.background": "#DEB661"
        },
    },
    ...
}
```

![2023.11.14 - 100119](2023.11.14%20-%20100119.jpg)

If you would like to get a full list of the element you can manipulate with (or keyword you can use in `workbench/colorCustomization`, you can checkout the [Theme Color Reference](https://code.visualstudio.com/api/references/theme-color).



#### Syntax Highlight (token)

To change the **"Syntax Highlighting"** (or token) coloring such as the color of the comment, the variables and the keywords, use `editor.otkenColorCustomization`; The offical documentation of this can be found at: [Editor syntax highlighting](https://code.visualstudio.com/docs/getstarted/themes#_editor-syntax-highlighting).

For instance, if you would like to change the syntax highlighting color for **comment** and **variables** in theme **Monkai**, and change the color of the syntax for **keywords** in theme **Abyss (Red)**, you can do that via adding the follwing in the settings.json:

```json
{
    ...
    "editor.tokenColorCustomizations": {
    "[Monokai]": {
        "comments": "#229977",
        "variables": "#229977",
    },
    "[Abyss][Red]": {
        "keywords": "#f00",
    }
    ...
}
```

![2023.11.14 - 100355](2023.11.14%20-%20100355.jpg)

If you would like to get a full list of the element you can manipulate with (or keyword you can use in `editor.tokenColorCustomization`, you can checkout the [Syntax Highlight / Token Color Reference](https://code.visualstudio.com/api/language-extensions/semantic-highlight-guide).




## Exporting Color Theme
In case you would like to export your color theme and save it as an extension to populate within your small hack community or extension store, you can do that via the following:
TODO: PENDING COMPLETE THIS SECTION !

> Reference
> [VS Code Documentation - Create a new Color Theme](https://code.visualstudio.com/docs/getstarted/themes#_customizing-a-color-theme)

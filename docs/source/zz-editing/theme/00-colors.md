# colors
furo is styled with [css variables](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties), so changing a color is a dictionary entry, not a stylesheet.

## how light and dark work
light mode is the default. dark mode kicks in when the browser asks for it, through `prefers-color-scheme: dark`.

dark mode **inherits** every light mode variable and only overrides what has to differ, so setting `light_css_variables` alone is usually enough. the switching mechanism itself is not configurable, the values are.

## set them

```py
html_theme_options = {
    "light_css_variables": {
        "color-brand-primary": "#7C4DFF",
        "color-brand-content": "#7C4DFF",
        "color-admonition-background": "orange",
    },
    "dark_css_variables": {
        "color-brand-primary": "#B39DFF",
    },
}
```

the three most used ones:

| variable | styles |
|---|---|
| `color-brand-primary` | links and sidebar content |
| `color-brand-content` | links inside the page body |
| `color-brand-visited` | visited links |

the full list lives in furo's source, split per concern:
[src/furo/assets/styles/variables](https://github.com/pradyunsg/furo/tree/main/src/furo/assets/styles/variables)

:::{caution}
typos in `*_css_variables` are **silently ignored** — no error, no warning. if a color does not change, check the spelling first.
:::

## code highlighting
code colors do not come from css variables, they come from pygments:

```py
pygments_style = "sphinx"
pygments_dark_style = "monokai"
```

`pygments_dark_style` is a furo addition, plain sphinx only has `pygments_style`.
any [pygments style name](https://pygments.org/styles/) works.

this template does not set either, so sphinx's default is used. it also sets `highlight_language = 'text'`, which means a code fence with no language gets no highlighting at all — see [code](../formatting/03-code.md).

## different content per mode
not a color, but the same light / dark split. furo ships two classes:

````md
```{image} diagram-light.png
:class: only-light
```

```{image} diagram-dark.png
:class: only-dark
```
````

use it for images with a baked in background. details in [images](../formatting/05-images.md).

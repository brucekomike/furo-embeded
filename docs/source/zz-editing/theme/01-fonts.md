# fonts
three css variables, set like any other.

```py
html_theme_options = {
    "light_css_variables": {
        "font-stack": "Arial, sans-serif",
        "font-stack--monospace": "Courier, monospace",
        "font-stack--headings": "Georgia, serif",
    },
}
```

| variable | used for |
|---|---|
| `font-stack` | body text |
| `font-stack--monospace` | code blocks and inline code |
| `font-stack--headings` | headings, falls back to `font-stack` |

dark mode inherits these, so light mode is the only place to set them.

:::{note}
furo's defaults are picked to look right on every major platform **without downloading a web font**. swapping them costs page load time, so only do it for brand reasons.
:::

## self hosted fonts
put the files under `source/_static`, load a stylesheet that declares them, then name them in `font-stack`.

`source/_static/fonts.css`:

```css
@font-face {
  font-family: "My Font";
  src: url("my-font.woff2") format("woff2");
}
```

`source/conf.py`:

```py
html_static_path = ['_static']
html_css_files = ["fonts.css", "footer.css"]
html_theme_options = {
    "light_css_variables": {
        "font-stack": "'My Font', sans-serif",
    },
}
```

the `@font-face` url is relative to the css file, and every file in `_static` lands at the build root, so `"my-font.woff2"` is correct.

see [injecting](07-injecting.md) for how `html_css_files` works.

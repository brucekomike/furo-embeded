# logo and title
the logo sits at the top of the left sidebar, the title next to it.

## one logo for both modes
plain sphinx. the path is relative to `source/`, and sphinx copies the file into the build for you.

```py
html_logo = "_static/logo.svg"
```

## separate light and dark logos
needed when the logo is transparent and only reads against one background.

```py
html_static_path = ["_static"]
html_theme_options = {
    "light_logo": "logo-light.png",
    "dark_logo": "logo-dark.png",
}
```

:::{important}
`light_logo` and `dark_logo` are **relative to `html_static_path`**, not to `source/`. the example above means `_static/logo-light.png`. that is the opposite of how `html_logo` behaves, and getting it wrong only shows up as a missing image in the browser.
:::

## favicon

```py
html_favicon = "_static/favicon.svg"
```

both lines are already in `conf.py`, commented out, next to the `## change required` block.

## hide the project name
when the logo already carries the name:

```py
html_theme_options = {
    "sidebar_hide_name": True,
}
```

## sidebar title
without `html_title` the sidebar reads `<project> <release> documentation`, built from the `project` and `release` values in `conf.py`. `release` is dropped when it is not set.

override the whole string:

```py
html_title = "my docs"
```

`html_title` also becomes the browser tab title. this template already sets it.

## related opengraph keys
the social preview card reuses the logo unless told otherwise:

```py
ogp_image = '_static/logo.svg'
ogp_image_alt = 'site logo'
```

see [opengraph](../extensions/opengraph.md).

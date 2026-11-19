# theme
look and feel of the site. nearly all of it is driven by `html_theme_options` in `source/conf.py`.

```{toctree}
:maxdepth: 2
:hidden:

00-colors
01-fonts
02-logo
03-source-buttons
04-footer
05-announcement
06-sidebar-and-toc
07-injecting
```

## where each thing lives

| to change | config key | page |
|---|---|---|
| colors | `light_css_variables`, `dark_css_variables`, `pygments_style` | [colors](00-colors.md) |
| fonts | `light_css_variables` | [fonts](01-fonts.md) |
| logo, favicon, sidebar title | `html_logo`, `light_logo`, `dark_logo`, `html_title` | [logo](02-logo.md) |
| edit / view buttons | `top_of_page_buttons`, `source_*` | [source buttons](03-source-buttons.md) |
| footer icons | `footer_icons` | [footer](04-footer.md) |
| top banner | `announcement` | [announcement](05-announcement.md) |
| sidebars | `sidebar_hide_name`, `html_sidebars`, `hide-toc` | [sidebar and toc](06-sidebar-and-toc.md) |
| your own css / js / html | `html_css_files`, `html_js_files`, `templates_path` | [injecting](07-injecting.md) |

## every key furo reads

out of `html_theme_options`:

| key | does |
|---|---|
| `light_css_variables` | css variables for light mode |
| `dark_css_variables` | css variables for dark mode |
| `light_logo` | logo file used in light mode |
| `dark_logo` | logo file used in dark mode |
| `sidebar_hide_name` | show only the logo in the sidebar |
| `navigation_with_keys` | left / right arrow keys change page |
| `top_of_page_buttons` | any subset of `"edit"` and `"view"` |
| `source_repository` | repository url, for github.com / gitlab.com / bitbucket.org |
| `source_branch` | branch the source links point at |
| `source_directory` | where the sources sit inside the repository |
| `source_edit_link` | explicit edit url template, for any other host |
| `source_view_link` | explicit view url template, for any other host |
| `footer_icons` | icon links at the bottom of the sidebar |
| `announcement` | html banner across the top of every page |
| `is_rtl` | right to left layout |

:::{note}
`top_of_page_button` (singular) is the old spelling and is deprecated. use `top_of_page_buttons`.
:::

furo inherits from sphinx's built in `basic` theme, but only the keys above are supported.

## what this template already sets

```py
html_theme_options = {
    "source_repository": "https://github.com/brucekomike/furo-embeded",
    "source_branch": "main",
    "source_directory": "docs/source/",
    "navigation_with_keys": True,
    #"source_view_link": "https://gitlab.change.this/OWNER/REPO/-/blob/main/docs/source/{filename}",
}
```

plus `html_title`, `html_css_files`, `highlight_language` and the opengraph keys.
everything is between the `## change required >>>` markers in `conf.py`.

## upstream

- [furo customisation](https://pradyunsg.me/furo/customisation/)
- [furo theme options](https://pradyunsg.me/furo/customisation/index.html#theme-options)
- [sphinx configuration values](https://www.sphinx-doc.org/en/master/usage/configuration.html)

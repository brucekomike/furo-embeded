# sidebar and toc
the left sidebar holds the brand, search and navigation. the right one holds the contents of the current page.

## contents sidebar
the right sidebar is hidden automatically on any page without inner headings. force it hidden with front matter at the top of the file:

```yaml
---
hide-toc: true
---
```

this template's `source/index.md` already does it, since the landing page is just an include and a toctree.

front matter is a yaml block on the first line of the file. it is sphinx's [file-wide metadata](https://www.sphinx-doc.org/en/master/usage/restructuredtext/field-lists.html#metadata), and furo reads `hide-toc` out of it.

## sidebar name

```py
html_theme_options = {
    "sidebar_hide_name": True,
}
```

leaves only the logo. pairs with [logo](02-logo.md).

## keyboard navigation

```py
html_theme_options = {
    "navigation_with_keys": True,
}
```

left and right arrows move between pages. already on in this template.

## right to left

```py
html_theme_options = {
    "is_rtl": True,
}
```

set it independently of sphinx's `language` — `language` picks the translation of furo's own strings, `is_rtl` flips the layout for arabic, persian and hebrew.

## rebuild the whole sidebar
`html_sidebars` replaces the fragment list. this is furo's default, taken from `theme.conf`:

```py
html_sidebars = {
    "**": [
        "sidebar/scroll-start.html",
        "sidebar/brand.html",
        "sidebar/search.html",
        "sidebar/navigation.html",
        "sidebar/ethical-ads.html",
        "sidebar/scroll-end.html",
        "sidebar/variant-selector.html",
    ]
}
```

:::{warning}
`sidebar/scroll-start.html` and `sidebar/scroll-end.html` must both stay in the list. whatever sits between them is the scrollable region, and anything outside it must fit in the viewport.
:::

move `sidebar/brand.html` and `sidebar/search.html` below `scroll-start.html` to make the entire sidebar scroll, brand included.

keep `sidebar/ethical-ads.html` if you host on read the docs.

:::{caution}
furo treats this list as unstable. an upgrade can rename or reorder fragments and there is no deprecation warning for it.
:::

## change one sidebar element
override a single fragment instead of the whole list. `templates_path = ['_templates']` is already set, so adding a file at the matching path is enough.

`source/_templates/sidebar/brand.html`:

```html
{%- extends "!sidebar/brand.html" -%}

{%- block sidebar_logo -%}
{{ super() }}
<div class="tagline">docs for the thing</div>
{%- endblock -%}
```

the `!` prefix means "the theme's own version of this file". the fragment list lives at
[src/furo/theme/furo/sidebar](https://github.com/pradyunsg/furo/tree/main/src/furo/theme/furo/sidebar).

## upstream
- [furo: changing sidebar elements](https://pradyunsg.me/furo/customisation/sidebar/)
- [furo: hiding contents sidebar](https://pradyunsg.me/furo/customisation/toc/)
- [furo: right to left](https://pradyunsg.me/furo/customisation/right-to-left/)

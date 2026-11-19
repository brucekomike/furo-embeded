# footer
two different things live at the bottom of a furo page. the sidebar icons, and the page footer text.

## footer icons
icon links at the bottom of the left sidebar.

```py
html_theme_options = {
    "footer_icons": [
        {
            "name": "GitHub",
            "url": "https://github.com/brucekomike/furo-embeded",
            "html": """
                <svg stroke="currentColor" fill="currentColor" stroke-width="0" viewBox="0 0 16 16">
                    <path fill-rule="evenodd" d="M8 0C3.58 0 0 3.58 0 8c0 3.54 ..."></path>
                </svg>
            """,
            "class": "",
        },
    ],
}
```

| key | meaning |
|---|---|
| `name` | label for screen readers |
| `url` | where the click goes |
| `html` | raw html drawn as the icon |
| `class` | added to the `<a>` tag as-is |

setting a non empty `footer_icons` replaces the defaults. the defaults only exist on read the docs builds anyway — a github link and an rtd link — so on github pages or a self hosted instance there is nothing to lose.

### inline svg
`html` is raw, so relative paths into `_static` do not work. embed the svg, or point at an absolute url.

use `stroke="currentColor"` and `fill="currentColor"` so the icon follows the theme color instead of clashing with dark mode.

grab paths from <https://react-icons.github.io/react-icons/> — inspect element on the icon, copy the `<svg>`.

### icon fonts
load the css, then use `class` instead of `html`:

```py
html_css_files = [
    "https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/fontawesome.min.css",
    "https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/brands.min.css",
]
html_theme_options = {
    "footer_icons": [
        {
            "name": "GitHub",
            "url": "https://github.com/brucekomike/furo-embeded",
            "html": "",
            "class": "fa-brands fa-github fa-2x",
        },
    ],
}
```

`fa-2x` is needed to get a sane icon size. icon fonts cost first page load time, which is why furo itself embeds svg.

### different icon per mode
put `only-light` or `only-dark` in `class`. mainly useful when you are forced into `<img>` tags.

## page footer text
the copyright line and the links under it are **not** a furo option. they come from the template's `_templates/page.html`, which extends furo's page and appends a `footer-contribute` block:

```html
{%- extends "!page.html" -%}

{%- block footer -%}
{{ super() }}
<div class="footer-contribute">
  <ul>
    <li><a href="https://github.com/brucekomike/furo-embeded">use this template</a></li>
    <li><a href="https://yourcustomlink.invalid">Your Custom Link</a></li>
  </ul>
</div>
{%- endblock footer -%}
```

edit the `<li>` entries to taste — this is where an ICP number or a privacy link goes. the styling for it is in `_static/footer.css`.

`{{ super() }}` keeps furo's own footer, so the copyright and "last updated" lines survive.

## upstream
[furo: changing footer icons](https://pradyunsg.me/furo/customisation/footer/)

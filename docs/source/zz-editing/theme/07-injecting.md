# injecting css, js and html
what to reach for once the theme options run out.

:::{caution}
furo treats direct css / js / html injection as **unstable**. it is not designed to accommodate it and makes no effort to stay compatible across releases. prefer a theme option when one exists.
:::

## css and js

```py
html_static_path = ['_static']
html_css_files = ["footer.css"]
html_js_files = ["my.js"]
```

paths are relative to a directory in `html_static_path`. remote urls work in both lists:

```py
html_css_files = [
    "footer.css",
    "https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/brands.min.css",
]
```

anything under `_static` is copied to the build root, so `_static/footer.css` is served as `/footer.css`.

`footer.css` is already wired up here. it only styles the `footer-contribute` block added by `_templates/page.html` — see [footer](04-footer.md).

## overriding templates
sphinx loads `templates_path` before the theme, so a file with the same name as a theme template replaces it.

```py
templates_path = ['_templates']
```

this template ships one override, `source/_templates/page.html`:

```html
{%- extends "!page.html" -%}

{%- block footer -%}
{{ super() }}
...
{%- endblock footer -%}
```

the pattern to copy: `extends "!<same name>"`, then override a block and call `{{ super() }}` to keep the original content. dropping `super()` replaces it.

browsable list of everything overridable:
[src/furo/theme/furo](https://github.com/pradyunsg/furo/tree/main/src/furo/theme/furo)
plus the [sphinx-basic-ng components](https://sphinx-basic-ng.readthedocs.io/en/latest/usage/components/) furo builds on.

templating is [jinja2](https://jinja.palletsprojects.com/), and sphinx's own
[templating guide](https://www.sphinx-doc.org/en/master/development/theming.html#templating) lists the variables available in a page template.

## landing page
replace the front page with a hand written template:

```py
templates_path = ["_templates"]
html_additional_pages = {"index": "landing.html"}
```

sphinx processes `html_additional_pages` **after** the normal pages and allows overwriting, so this replaces the page built from `index.md`. `_templates/landing.html` is then entirely yours to write.

a lighter option that keeps markdown: leave `index.md` alone and build the landing page out of `{grid}` cards — see [sphinx-design](../extensions/sphinx-design.md).

## what this template does not touch
`html_js_files` is empty and `html_sidebars` is unset, so both are free to use.

# announcement
a banner across the top of every page.

```py
html_theme_options = {
    "announcement": "<em>v2.0</em> is out, see the <a href='/changelog'>changelog</a>.",
}
```

the value is raw html and goes into the page as-is. leaving it unset, or setting it to an empty string, removes the banner entirely.

:::{note}
because it is raw html, relative links are resolved against the current page. `href='/changelog'` is a root relative url and works from anywhere; `href='changelog.html'` only works from the top level. use root relative urls, or absolute ones.
:::

## colors
the banner has two variables of its own:

```py
html_theme_options = {
    "announcement": "moving to a new home",
    "light_css_variables": {
        "color-announcement-background": "#000000dd",
        "color-announcement-text": "#eeebee",
    },
    "dark_css_variables": {
        "color-announcement-background": "#ffdb00",
        "color-announcement-text": "#1a1c1e",
    },
}
```

those are furo's own defaults, shown here so you can see what to change.

## setting it at build time
useful for a banner that should only appear in one deployment, without editing `conf.py`:

```py
import os

html_theme_options = {}
if os.environ.get("DOCS_PREVIEW"):
    html_theme_options["announcement"] = (
        "This is a preview build. "
        "<a href='https://example.com/'>Go to the real site</a>."
    )
```

## upstream
[furo: adding an announcement banner](https://pradyunsg.me/furo/customisation/announcement/)

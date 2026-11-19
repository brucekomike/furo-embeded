# opengraph
the `<meta property="og:*">` tags that decide what a link looks like when it is pasted into a chat app, a feed reader or a social site. no markup in the pages, all of it in `conf.py`.

```py
extensions = ["sphinxext.opengraph"]
```

already on here. the pip name is `sphinxext-opengraph`, the extension name uses a dot.

## what this template sets

```py
ogp_site_url = 'https://brucekomike.github.io/furo-embeded/'
#ogp_image = '_static/logo.svg'
#ogp_image_alt = 'site logo'
ogp_site_name = 'furo template'
ogp_use_first_image = True
```

`ogp_site_url` is the only one that really matters — without it the extension cannot build absolute urls, and an og tag with a relative url is ignored by every scraper. change it to wherever the site is published, including a self hosted gitlab pages url.

## the options

| option | default | does |
|---|---|---|
| `ogp_site_url` | `''` | base url of the published site, required |
| `ogp_site_name` | `html_title` | the `og:site_name` tag |
| `ogp_description_length` | `200` | truncate the page description to this many characters |
| `ogp_image` | `None` | image for every page, falls back to `html_logo` |
| `ogp_image_alt` | `None` | alt text for that image |
| `ogp_use_first_image` | `False` | otherwise use the first image found on each page |
| `ogp_type` | `'website'` | `og:type`, `article` for a blog style site |
| `ogp_canonical_url` | `''` | override the canonical url per site |
| `ogp_enable_meta_description` | `True` | also emit a plain `<meta name="description">` |
| `ogp_custom_meta_tags` | `()` | extra tags, see below |
| `ogp_social_cards` | `None` | generate a card image per page at build time |

`ogp_site_name` and `ogp_image_alt` accept `False` to omit the tag entirely rather than emit an empty one.

## per page
the extension reads sphinx page metadata, so front matter can override the site default. these are the only keys it looks for:

```yaml
---
og:image: _static/diagram.png
og:image:alt: a diagram of the pipeline
ogp_description_length: 120
---
```

| key | does |
|---|---|
| `og:image` | image for this page, and turns `ogp_use_first_image` off for it |
| `og:image:alt` | alt text for that image |
| `ogp_description_length` | description length for this page |
| `ogp_disable` | emit no og tags at all for this page |

the keys are the literal og property names, not `og_image` — `og:image` with a colon.

## the description
there is no `description` key. `og:description` is **derived from the page body**: the extension walks the doctree, skips the page title, skips every admonition and comment, and takes text up to `ogp_description_length` characters.

that means the first prose paragraph of a page is its social preview text. two consequences worth knowing:

- a page that opens with a `{note}` or a table produces a poor or empty description, because admonitions are skipped entirely
- putting the sentence you want shared first is the only way to control it

check what a page produced before relying on it, see {ref}`ogp-checking` below.

## extra tags

```py
ogp_custom_meta_tags = [
    {'name': 'twitter:card', 'content': 'summary_large_image'},
    {'property': 'article:author', 'content': 'brucekomike'},
]
```

each entry is a dict of the attributes to put on the `<meta>` tag, so `name` or `property` and `content` at minimum.

## generated social cards
`ogp_social_cards` renders a preview image per page at build time, instead of reusing the logo. it needs extra system dependencies for image handling and is off by default:

```py
ogp_social_cards = {
    "line_color": "#4051b5",
    "width": 1200,
}
```

for a template, `ogp_use_first_image = True` is the better default — no build dependencies, and any diagram on the page becomes the preview.

(ogp-checking)=
## checking it
the tags are in the built html, so grep them:

```sh
grep -o '<meta property="og:[^>]*>' build/index.html
```

or paste the published url into a scraper's own debugger — [opengraph.xyz](https://www.opengraph.xyz/) and the linkedin post inspector both show what a crawler sees. a scraper caches aggressively, so a fix does not show up immediately.

## upstream
[sphinxext-opengraph documentation](https://sphinxext-opengraph.readthedocs.io/)

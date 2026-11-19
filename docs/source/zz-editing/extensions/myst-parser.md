# myst-parser
what makes markdown a sphinx source format. it is the reason every file in this project is `.md`.

```py
extensions = ["myst_parser"]
source_suffix = {
   '.rst': 'restructuredtext',
   '.txt': 'markdown',
   '.md': 'markdown',
   '': 'markdown',
}
```

`source_suffix` maps file extensions to parsers. this template also maps `''`, so a toctree entry can be written as `00` instead of `00.md` — which is what `00-manual/index.md` does.

## syntax extensions
plain markdown is only part of it. `myst_enable_extensions` switches on the rest, and **almost everything useful is off by default**:

```py
myst_enable_extensions = [
    "amsmath",
    "colon_fence",
    "deflist",
    "dollarmath",
    "fieldlist",
    "html_admonition",
    "html_image",
    "linkify",
    "replacements",
    "smartquotes",
    "strikethrough",
    "substitution",
    "tasklist",
]
```

that is what this template enables. the full list in myst-parser 5 is:

| extension | adds | on here |
|---|---|---|
| `colon_fence` | `:::{note}` instead of a backtick fence | yes |
| `deflist` | term / definition lists | yes |
| `fieldlist` | `:Author:` style field lists | yes |
| `tasklist` | `- [x]` checkboxes | yes |
| `strikethrough` | `~~gone~~` | yes |
| `linkify` | bare urls become links | yes |
| `substitution` | `{{ env.config.project }}` | yes |
| `smartquotes` | typographic quotes and apostrophes | yes |
| `replacements` | `(c)` `...` `+-` and friends | yes |
| `dollarmath` | `$x^2$` and `$$x^2$$` | yes |
| `amsmath` | `\begin{equation}` blocks | yes |
| `html_admonition` | `<div class="admonition">` | yes |
| `html_image` | `<img>` and `<picture>` as images | yes |
| `alert` | github style `> [!NOTE]` | no |
| `attrs_block` | `{...}` attributes on a block | no |
| `attrs_inline` | `{...}` attributes on inline markup | no |
| `attrs_image` | `![alt](img.png){width=100px}` | no |
| `gfm_autolink` | github's own autolink rules | no |

each one has a demo on the [formatting](../formatting/index.md) pages.

## the config prefix
every myst option in `conf.py` is `myst_` plus the field name:

| conf.py | field |
|---|---|
| `myst_enable_extensions` | `enable_extensions` |
| `myst_substitutions` | `substitutions` |
| `myst_heading_anchors` | `heading_anchors` |
| `myst_url_schemes` | `url_schemes` |
| `myst_all_links_external` | `all_links_external` |
| `myst_number_code_blocks` | `number_code_blocks` |
| `myst_enable_checkboxes` | `enable_checkboxes` |
| `myst_inventories` | `inventories` |

the full set, with defaults, is printed at the start of every build — the `myst v5.1.0: MdParserConfig(...)` line. that is the fastest way to check what is actually active.

## options worth knowing

### heading anchors
```py
myst_heading_anchors = 3
```
puts an id on every heading down to `###`, so `page.html#some-heading` works without a `(label)=`. off here.

### disabling syntax
```py
myst_disable_syntax = ["math_block"]
```
turns a CommonMark or MyST rule back off. the counterpart to `myst_enable_extensions`.

### custom substitutions
```py
myst_substitutions = {
    "product": "the widget",
}
```
then `{{ product }}` in any page. front matter substitutions in a page override these.

### warnings
myst routes its own warnings through sphinx's `suppress_warnings` with a `myst.` prefix:

```py
suppress_warnings = ["myst.strikethrough"]
```

`myst_suppress_warnings` also exists in the config but sphinx ignores it — only the docutils path reads that one. see [text](../formatting/00-text.md) for the strikethrough case specifically.

## upstream
- [myst markdown syntax](https://myst-parser.readthedocs.io/en/latest/syntax/typography.html)
- [myst configuration](https://myst-parser.readthedocs.io/en/latest/configuration.html)
- [roles and directives in MyST](https://myst-parser.readthedocs.io/en/latest/syntax/roles-and-directives.html)

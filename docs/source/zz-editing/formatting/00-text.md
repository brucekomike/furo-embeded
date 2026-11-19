# text
inline markup, paragraphs and the small block level things markdown covers.

## inline

````md
*emphasis*, **strong**, `inline code`
````

*emphasis*, **strong**, `inline code`

## strikethrough

````md
~~gone~~
````

builds to `<s>gone</s>`. it is not shown live on this page, because myst-parser emits a warning for every use:

```
Strikethrough is currently only supported in HTML output
```

docutils has no strikethrough node, so myst falls back to a raw html `<s>` tag and tells you about it. the output is correct in html, the warning is noise. silence it in `conf.py`:

```py
suppress_warnings = ["myst.strikethrough"]
```

:::{note}
it is sphinx's own `suppress_warnings`, not `myst_suppress_warnings` — under sphinx the myst one is ignored. the value is `myst.` plus the warning tag shown in square brackets.
:::

## subscript and superscript
markdown has no syntax for these, so they are roles:

````md
H{sub}`2`O and E = mc{sup}`2`
````

H{sub}`2`O and E = mc{sup}`2`

## abbreviations and standards

````md
{abbr}`HTML (Hyper Text Markup Language)`, {pep}`8`, {rfc}`822`
````

{abbr}`HTML (Hyper Text Markup Language)`, {pep}`8`, {rfc}`822`

the abbreviation shows as a tooltip. `pep` and `rfc` are built into sphinx's standard domain, no extension needed.

## keyboard input

````md
{kbd}`Ctrl`+{kbd}`C`
````

{kbd}`Ctrl`+{kbd}`C`

## blockquote

````md
> quoted text
>
> a second paragraph inside the quote
````

> quoted text
>
> a second paragraph inside the quote

## horizontal rule

````md
text above

---

text below
````

three or more `-` on a line of their own. needs blank lines around it, otherwise the line above turns into a heading.

## footnotes

````md
a claim[^1] and another[^note].

[^1]: the first footnote.
[^note]: a named footnote.
````

a claim[^1] and another[^note].

[^1]: the first footnote.
[^note]: a named footnote.

definitions can sit anywhere in the file, sphinx collects them into a list at the bottom. numbers and names both work; names are easier to reorder.

## substitutions
`substitution` is enabled, so `conf.py` values drop straight into prose with jinja syntax:

````md
this site is {{ env.config.project }} {{ env.config.release }}, page {{ env.docname }}.
````

this site is {{ env.config.project }} {{ env.config.release }}, page {{ env.docname }}.

`env` is sphinx's build environment. `env.config` reaches every value in `conf.py`.

:::{caution}
`{{ env.project }}` is **not** the project name — that is sphinx's internal `Project` object and it renders as `<sphinx.project.Project object at 0x...>`. always go through `env.config`.
:::

your own substitutions:

```py
myst_substitutions = {
    "product": "the widget",
}
```

then `{{ product }}` in any page.

## smart quotes and replacements
`smartquotes` and `replacements` are both enabled here.

````md
"quoted" ... it's +- 1/2 (c) (tm) (r)
````

"quoted" ... it's +- 1/2 (c) (tm) (r)

`replacements` swaps the ascii forms for their typographic ones: `...` for an ellipsis, `(c)` `(tm)` `(r)` for the symbols, `+-` for plus-minus, `1/2` for a fraction. `smartquotes` does the quote marks and apostrophes.

both are off by default in myst, and both are on in this template.

## field lists
`fieldlist` is enabled. mid page it renders as a two column table:

````md
:Author: brucekomike
:Version: 0.3
````

:Author: brucekomike
:Version: 0.3

at the very top of a file a field list becomes page metadata instead — but in MyST you want the yaml front matter form for that, see [formatting](index.md).

## raw html
MyST passes html blocks and inline html through. `html_image` additionally lets an `<img>` or `<picture>` stand in for a markdown image:

````md
<img src="../../_static/example.svg" width="120">
````

<img src="../../_static/example.svg" width="120">

:::{caution}
paths in raw html are resolved by the **browser** against the built page url, not by sphinx. this page builds to `zz-editing/formatting/00-text.html`, so reaching `_static` takes `../../`. sphinx does not copy the file for you either — it only gets there because `_static` is in `html_static_path`. `{image}` handles both, which is the reason to prefer it.
:::

`html_admonition` turns a `<div class="admonition">` into a real admonition. useful when a page was written for another generator, but a directive is clearer — see [admonitions](06-admonitions.md).

:::{note}
raw html is invisible to every non-html builder. latex, epub and plain text output will drop it.
:::

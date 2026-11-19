# links

## external

````md
[the text](https://example.com)
````

[the text](https://example.com)

a bare url in angle brackets becomes a link on its own:

````md
<https://example.com>
````

<https://example.com>

`linkify` is enabled in `conf.py`, so a bare url without brackets is linked too:

````md
https://example.com
````

https://example.com

:::{note}
`linkify` needs the `linkify-it-py` package. it is covered by the `myst-parser[linkify]` line in `requirements.txt`. without it the extension is silently inert.
:::

## reference style
the url at the bottom of the file, the label where you want it. worth it when the same url appears more than once, or when the url is long enough to break the sentence up:

````md
see [text](../theme/00-colors.md) and [fonts](../theme/01-fonts.md).

[text]: ../theme/00-colors.md
[fonts]: ../theme/01-fonts.md
````

see [text][lk1] and [fonts][lk2].

[lk1]: ../theme/00-colors.md
[lk2]: ../theme/01-fonts.md

## to another page
a markdown link with a relative path to the `.md` source, not the built `.html`:

````md
see [colors](../theme/00-colors.md) and the [tutorial index](../tutorial/index.md).
````

see [colors](../theme/00-colors.md) and the [tutorial index](../tutorial/index.md).

sphinx rewrites the target to the right output url, and warns when the file does not exist. paths are relative to the current file, and a leading `/` means "from the source root":

````md
[text](../theme/00-colors.md)               relative to this file
[text](/zz-editing/theme/00-colors.md)      from the source root
````

the root form survives the file being moved.

## to a heading
put a label in parentheses on the line directly above the heading, then reference it:

````md
(target-name)=
## a heading

...somewhere else in the project...

see {ref}`target-name`.
````

(target-name)=
## a heading

see {ref}`target-name`.

a bare ``{ref}`label` `` pulls the heading title in, and keeps working if the heading is renamed. for your own link text:

````md
{ref}`the link text <target-name>`
````

{ref}`the link text <target-name>`

labels are global across the whole project, so make them specific — `(colors)=` on two pages is an ambiguity warning, `(furo-colors)=` is not.

`myst_heading_anchors` in `conf.py` also emits an id on every heading up to a given depth, so `00-colors.html#set-them` works as a plain url. it is unset here, so only explicit labels are linkable.

## to a specific thing
sphinx's cross reference roles resolve against its domains:

````md
{doc}`/zz-editing/formatting/00-text`   a page, no extension
{ref}`target-name`                      a label
{any}`some name`                        anything, searched across domains
{term}`, {keyword}`, {option}`          std domain entries
{envvar}`, {program}`, {command}`       things something must declare first
````

all of them need a matching declaration somewhere in the project, otherwise sphinx warns about an unknown target. `{doc}` and `{ref}` are the two that work with no setup at all, and `{doc}` is the RST-era equivalent of a markdown page link — prefer the markdown link.

the code roles (``{py:func}``, ``{py:class}``, ``{py:mod}``) only resolve once something declares them, either through `sphinx.ext.autodoc` reading real source, or a manual ```` ```{py:function} ```` directive. neither is configured in this template.

## to another project's docs
`sphinx.ext.intersphinx` is not configured here. adding it makes a role like ``{py:class}`pathlib.Path` `` resolve against python's own documentation:

```py
extensions = ["sphinx.ext.intersphinx"]
intersphinx_mapping = {
    "python": ("https://docs.python.org/3", None),
    "sphinx": ("https://www.sphinx-doc.org/en/master", None),
}
```

myst has a lighter built in form that needs no extension:

```py
myst_inventories = {
    "python": ["https://docs.python.org/3", "https://docs.python.org/3/objects.inv"],
}
```

## url schemes
`http`, `https`, `mailto` and `ftp` become links by default. add your own:

```py
myst_url_schemes = ["http", "https", "mailto", "ftp", "doi"]
```

or control the rendered form per scheme:

```py
myst_url_schemes = {
    "http": None,
    "https": None,
    "mailto": None,
    "doi": {
        "url": "https://doi.org/{{ path }}",
        "title": "DOI: {{ path }}",
        "classes": ["doi"],
    },
}
```

`None` means "default behaviour". `{{ path }}`, `{{ scheme }}` and `{{ netloc }}` are filled in from the url.

## bulk settings

| config | does |
|---|---|
| `myst_all_links_external = True` | stop resolving internal links, treat everything as a plain url |
| `myst_links_external_new_tab = True` | `target="_blank"` on external links |

both off by default. the second one surprises people who middle click, so leave it off unless there is a reason.

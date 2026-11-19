# editing memo
how to use and customise this template.

```{toctree}
tutorial/index
formatting/index
theme/index
extensions/index
```

| section | for |
|---|---|
| [tutorial](tutorial/index.md) | getting the template running, and the changes every project has to make |
| [formatting](formatting/index.md) | the markups available in a page — text, lists, tables, code, links, images, admonitions, tabs |
| [theme](theme/index.md) | the look of the site — colors, fonts, logo, buttons, footer, sidebars |
| [extensions](extensions/index.md) | what `conf.py` loads, and the markup each extension adds |

## the short version
- pages are markdown, parsed by [myst-parser](extensions/myst-parser.md)
- markdown first, a `{directive}` only where markdown has no syntax for it
- everything to change in `conf.py` sits between the `## change required >>>` markers
- a build should produce **zero warnings**, treat any warning as a bug

# extensions
what this template loads in `conf.py`, and the markup each one adds.

```{toctree}
:maxdepth: 2
:hidden:

myst-parser
sphinx-design
inline-tabs
copybutton
opengraph
math
mermaid
graphviz
```

## what is on

| extension | adds | on by default |
|---|---|---|
| `myst_parser` | markdown as a sphinx source format | yes |
| `sphinx_design` | dropdowns, cards, grids, badges, buttons, icons, tabs | yes |
| `sphinx_inline_tabs` | `{tab}` | yes |
| `sphinx_copybutton` | a copy button on every code block | yes |
| `sphinxext.opengraph` | social preview meta tags | yes |
| `sphinx.ext.githubpages` | the `CNAME` file github pages wants | yes |
| `sphinxcontrib.mermaid` | `{mermaid}` diagrams from text | no, commented out |
| `sphinx.ext.mathjax` | rendered maths | no, commented out |
| `sphinx.ext.graphviz` | `{graphviz}` / `{digraph}` from DOT | no, not listed |

`requirements.txt` installs all of them, including the optional ones, so switching one on is a `conf.py` edit and nothing else.

## turning one on
add it to `extensions`, then rebuild:

```py
extensions = [
    "myst_parser",
    "sphinx_design",
    "sphinxcontrib.mermaid",
]
```

the two optional blocks in `conf.py` are marked `## change required >>>` / `<<<` so they are easy to find.

:::{note}
`sphinx_design` is imported with an underscore and `sphinxcontrib.mermaid` with a dot — the pip package name, the python module name and the sphinx extension name are not always the same string. `sphinx-design` on pip, `sphinx_design` in `extensions`.
:::

## upstream
- [sphinx built in extensions](https://www.sphinx-doc.org/en/master/usage/extensions/index.html)
- [sphinx-design](https://sphinx-design.readthedocs.io/)
- [myst-parser](https://myst-parser.readthedocs.io/)

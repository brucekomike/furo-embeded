# formatting
the markups this template understands. MyST markdown first, a directive only where markdown has no syntax for it.

```{toctree}
:maxdepth: 2
:hidden:

00-text
01-lists
02-tables
03-code
04-links
05-images
06-admonitions
07-tabs
```

every page shows the source first, in a highlighted fence, then what it builds into directly below.

## the two forms of directive
markdown covers most of it. where it does not, use a directive — a code fence whose language is `{name}`:

````md
```{note}
body
```
````

or the colon fence, which needs no backticks:

```
:::{note}
body
:::
```

`colon_fence` is enabled in `conf.py`, so both work everywhere here. pick one and stay with it — this template's own pages use colon fences in prose and backtick fences when nesting.

two rules that bite:

- a nested directive needs a **longer** fence than the ones inside it. ```` ```` ```` around ```` ``` ````.
- options go on their own lines right after the opening fence, at column 0, before a blank line and the body.

## roles
inline markup in curly braces and backticks:

````md
{sub}`2` and {kbd}`Ctrl`+{kbd}`C`
````

{sub}`2` and {kbd}`Ctrl`+{kbd}`C`

:::{tip}
to *show* a role instead of running it, wrap it in **double** backticks with a space either side, like ``{doc}`path` `` on this line. single backticks would not work — the inner backticks close the span early.
:::

## front matter
a yaml block on line 1 of a file sets page metadata:

```yaml
---
hide-toc: true
orphan: true
---
```

`hide-toc` is furo's, `orphan` is sphinx's (keeps a page out of a toctree without warning). more in [sidebar and toc](../theme/06-sidebar-and-toc.md).

## upstream
- [MyST markdown syntax](https://myst-parser.readthedocs.io/en/latest/syntax/typography.html)
- [furo markup reference](https://pradyunsg.me/furo/reference/)
- [furo kitchen sink](https://pradyunsg.me/furo/kitchen-sink/)

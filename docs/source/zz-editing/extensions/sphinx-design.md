# sphinx-design
the component library. dropdowns, cards, grids, badges, buttons, icons and tabs, all of them styled to match furo.

```py
extensions = ["sphinx_design"]
```

already on here. the pip name is `sphinx-design`, the extension name uses an underscore.

## dropdown
a block hidden behind a clickable header. the thing markdown cannot express, and the most used component here.

````md
```{dropdown}
content, header taken from the first line
```

```{dropdown} a real title
content
```

```{dropdown} open by default
:open:
content
```

```{dropdown} with options
:color: primary
:icon: alert-fill
:animate: fade-in
content
```
````

```{dropdown}
content, header taken from the first line
```

```{dropdown} a real title
content
```

```{dropdown} open by default
:open:
content
```

| option | does |
|---|---|
| `:open:` | start expanded |
| `:color:` | `primary`, `secondary`, `success`, `info`, `warning`, `danger`, `light`, `dark`, `muted` |
| `:icon:` | an octicon name next to the title |
| `:animate:` | `fade-in`, `fade-in-slide-down`, `flip`, ... |
| `:class-container:` | css classes on the outer box |
| `:class-title:` / `:class-body:` | css classes on the parts |
| `:margin:` | pull it into the page margin |

:::{caution}
options must start at column 0, on the lines directly after the opening fence. indenting them — as you would in RST — makes myst warn `expected key to start at column 0`. a blank line separates the options from the body.
:::

shadows, from the kitchen sink:

````md
```{dropdown} "md" shadow
:class-container: sd-shadow-md
content
```
````

```{dropdown} "md" shadow
:class-container: sd-shadow-md
content
```

`sd-shadow-sm`, `sd-shadow-md`, `sd-shadow-lg`, `sd-shadow-none`.

## card
a bordered box with an optional header and footer. `^^^` splits the header off, `+++` splits the footer:

````md
```{card} Card Title
Header
^^^
Card content
+++
Footer
```
````

```{card} Card Title
Header
^^^
Card content
+++
Footer
```

a whole card can be a link:

````md
```{card} Clickable Card
:link: https://example.com
The entire card can be clicked to navigate.
```
````

```{card} Clickable Card
:link: https://example.com
The entire card can be clicked to navigate.
```

`:link:` takes a url, or with `:link-type: doc` a page path, or with `:link-type: ref` a label. `:link-alt:` sets the link text for screen readers.

:::{note}
`{link-card}` does not exist in sphinx-design 0.7.0 — it needs 0.8 or newer, and `requirements.txt` does not pin a version. `:link:` on the card does the same job on any version.
:::

## grid
responsive columns. the argument is **one number or four** — the column count at extra-small, small, medium and large breakpoints:

`````md
````{grid} 1 1 2 3
```{grid-item-card} One
:link: https://example.com/
content one
```

```{grid-item-card} Two
content two
```

```{grid-item-card} Three
content three
```
````
`````

````{grid} 1 1 2 3
```{grid-item-card} One
:link: https://example.com/
content one
```

```{grid-item-card} Two
content two
```

```{grid-item-card} Three
content three
```
````

one column on a phone, two on a tablet, three on a desktop. this is the usual way to build a landing page out of markdown instead of hand writing a template.

a single number applies at every breakpoint: ```` ```{grid} 3 ```` is three columns everywhere.

:::{caution}
two or three values is an error, not a shorthand:

```
Invalid directive argument: argument must be 1 or 4 (xs sm md lg) values,
and each value should be either auto or an integer from 1 to 12
```

write out all four, or use one. each value is `auto` or an integer from 1 to 12.
:::

:::{caution}
children of a `{grid}` must be `{grid-item}` or `{grid-item-card}`. a plain `{card}` inside a `{grid}` is **not** wrapped for you and produces `All children of a 'grid-row' should be 'grid-item'` for every card, on every page. use `{grid-item-card}`.
:::

`{grid-item-card}` takes everything `{card}` does — `:link:`, `:link-type:`, `:img-top:`, `:img-bottom:`, `:header:`, `:footer:` — plus `:class-item:` for `only-light` / `only-dark`.

a card with an image on top:

`````md
````{grid} 1 1 2 2
```{grid-item-card} With an image
:img-top: ../../_static/example.svg
content
```
````
`````

````{grid} 1 1 2 2
```{grid-item-card} With an image
:img-top: ../../_static/example.svg
content
```
````

plain `{grid-item}` is for content that is not a card:

`````md
````{grid} 1 1 2 2
```{grid-item}
left column, no box
```

```{grid-item}
right column, no box
```
````
`````

````{grid} 1 1 2 2
```{grid-item}
left column, no box
```

```{grid-item}
right column, no box
```
````

## card-carousel
a horizontally scrollable row of cards. the argument is how many show at once:

`````md
````{card-carousel} 2
```{card} card 1
```
```{card} card 2
```
```{card} card 3
```
```{card} card 4
```
````
`````

````{card-carousel} 2
```{card} card 1
```
```{card} card 2
```
```{card} card 3
```
```{card} card 4
```
````

unlike `{grid}` this one takes plain `{card}` children.

## badges
inline pill labels. `{bdg}` is plain, `{bdg-<color>}` is filled, `{bdg-<color>-line}` is outlined:

````md
{bdg}`plain`

{bdg-primary}`primary` {bdg-primary-line}`primary-line`
{bdg-success}`success` {bdg-success-line}`success-line`
{bdg-warning}`warning` {bdg-danger}`danger`
````

{bdg}`plain`

{bdg-primary}`primary` {bdg-primary-line}`primary-line`
{bdg-success}`success` {bdg-success-line}`success-line`
{bdg-warning}`warning` {bdg-danger}`danger`

the colors are `primary`, `secondary`, `success`, `info`, `warning`, `danger`, `light`, `dark`, `muted`.

clickable versions swap the prefix:

| role | target |
|---|---|
| ``{bdg}`text` `` | nothing |
| ``{bdg-link-primary}`url` `` | a url |
| ``{bdg-ref-primary}`label` `` | a `{ref}` label |

````md
{bdg-link-success}`https://example.com`
````

{bdg-link-success}`https://example.com`

## buttons
````md
```{button-link} https://example.com
Button text
```

```{button-link} https://example.com
:color: primary
Button text
```

```{button-link} https://example.com
:color: secondary
:expand:
```
````

```{button-link} https://example.com
Button text
```

```{button-link} https://example.com
:color: primary
Button text
```

```{button-link} https://example.com
:color: secondary
:expand:
```

| option | does |
|---|---|
| `:color:` | one of the badge colors |
| `:expand:` | stretch to the full width |
| `:outline:` | outlined instead of filled |
| `:align:` | `left`, `center`, `right` |
| `:class:` | extra css classes |
| `:tooltip:` | hover text |
| `:ref-type:` | with `{button-ref}`, `doc` or `ref` |

`{button-ref}` is the same thing pointing at an internal label instead of a url:

````md
```{button-ref} target-name
:ref-type: ref
:color: primary
go to the heading
```
````

## icons
````md
{octicon}`heart-fill;1em;sd-text-danger`
{octicon}`mark-github`
{octicon}`alert-fill;2em`
````

{octicon}`heart-fill;1em;sd-text-danger`
{octicon}`mark-github`
{octicon}`alert-fill;2em`

the three parts are `name;size;classes`, and the last two are optional. sizes are any css length; classes include the `sd-text-*` color helpers.

names come from [github's octicons](https://primer.style/foundations/icons/octicons-v1), with no size suffix on the name — `mark-github`, not `mark-github-16`.

:::{note}
the `{octicon}` **role** takes a size suffix in its content, but the `:icon:` **option** on a dropdown does not. `{octicon}`alert-fill;1em`` is right, `:icon: alert-fill;1em` is not.
:::

fontawesome and material icon roles exist too, but they need the extra packages:

```py
extensions = ["sphinx_design[material,rtd,fontawesome]"]
```

they are not installed here.

## article-info
author, date and read time in one block:

````md
```{article-info}
:avatar: https://avatars.githubusercontent.com/u/3275593?s=80&v=4
:avatar-link: https://pradyunsg.me
:avatar-outline: muted
:author: brucekomike
:date: Nov 11, 2026
:read-time: 5 min read
```
````

```{article-info}
:avatar: https://avatars.githubusercontent.com/u/3275593?s=80&v=4
:avatar-link: https://pradyunsg.me
:avatar-outline: muted
:author: brucekomike
:date: Nov 11, 2026
:read-time: 5 min read
```

`:avatar-outline:` takes a badge color. every option is optional.

## div
the escape hatch — a bare `<div>` with classes, for wrapping anything:

````md
```{div} sd-text-center sd-fs-5
centered, larger text
```
````

```{div} sd-text-center sd-fs-5
centered, larger text
```

the argument is the class list, space separated. also useful for giving a wide table a scrolling wrapper, see [tables](../formatting/02-tables.md).

## css helper classes
sphinx-design ships a bootstrap flavoured set, all prefixed `sd-`:

| prefix | examples |
|---|---|
| `sd-text-*` | `sd-text-center`, `sd-text-danger`, `sd-text-muted` |
| `sd-fs-*` | `sd-fs-1` to `sd-fs-6`, font size |
| `sd-m*` / `sd-p*` | `sd-mb-3`, `sd-px-2`, margin and padding |
| `sd-shadow-*` | `sd-shadow-sm`, `sd-shadow-md`, `sd-shadow-lg` |
| `sd-w-*` / `sd-h-*` | `sd-w-50`, `sd-h-100` |
| `sd-d-*` | `sd-d-flex`, `sd-d-none`, display |
| `sd-rounded-*` | `sd-rounded-1`, `sd-circle` |

usable from `:class:`, `:class-container:`, `{div}` and `{grid-item-card}`'s `:class-item:`.

## custom directives
rename or restyle a component without forking it:

```py
sd_custom_directives = {
    "dropdown-primary": {
        "base": "dropdown",
        "options": {"color": "primary", "open": True},
    },
}
```

then ```` ```{dropdown-primary} ```` behaves as a `{dropdown}` with those options baked in.

## upstream
- [sphinx-design documentation](https://sphinx-design.readthedocs.io/en/latest/)
- [furo kitchen sink: sphinx-design](https://pradyunsg.me/furo/kitchen-sink/sphinx-design.html)
- [css helper classes](https://sphinx-design.readthedocs.io/en/latest/css/style.html)

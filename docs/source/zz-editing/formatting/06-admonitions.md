# admonitions
a callout box that does not interrupt the flow of the page. every one of them takes the same shape:

````md
```{note}
the body goes here
```
````

or the colon fence form, which is what this page uses in prose:

```
:::{note}
the body goes here
:::
```

anything goes in the body — paragraphs, lists, code fences, tables, other admonitions. a nested directive needs a longer fence than the ones inside it.

## the types
sphinx ships these, and furo styles each one with its own color and icon.

### note

````md
```{note}
the neutral one, for asides
```
````

```{note}
the neutral one, for asides
```

### tip

```{tip}
something that makes the task easier
```

### hint

```{hint}
a pointer towards the right answer
```

### important

```{important}
cannot be skipped without breaking something
```

### seealso

```{seealso}
links to related material
```

### attention

```{attention}
worth stopping for
```

### caution

```{caution}
a mistake here is recoverable but annoying
```

### warning

```{warning}
a mistake here loses data or breaks the build
```

### danger

```{danger}
irreversible
```

### error

```{error}
this is broken
```

### todo

needs `sphinx.ext.todo` in `extensions`, which this template does not load, so it is not rendered here. with it enabled, `{todo}` items are collected into a list by `{todolist}`.

## custom title
`{admonition}` is the generic one, and it takes the title as its argument:

````md
```{admonition} a title of your own
the body
```
````

```{admonition} a title of your own
the body
```

it renders neutral, without an icon. give it a `:class:` to borrow another type's styling:

````md
```{admonition} a title of your own
:class: warning

the body
```
````

```{admonition} a title of your own
:class: warning

the body
```

## nesting
possible, and furo's own docs advise against it — nested boxes read as noise. one level is the practical limit:

`````md
````{note}
the outer box

```{warning}
the inner box
```
````
`````

````{note}
the outer box

```{warning}
the inner box
```
````

## github style alerts
myst-parser 5 has an `alert` extension for the github flavour:

```py
myst_enable_extensions = [
    ...,
    "alert",
]
```

then in a page:

````md
> [!NOTE]
> the body

> [!WARNING]
> the body
````

`NOTE`, `TIP`, `IMPORTANT`, `WARNING` and `CAUTION` are recognised. not enabled in this template — the directive form above already covers it, and `{admonition}` can do things an alert cannot.

## styling them
two css variables cover most of it:

```py
html_theme_options = {
    "light_css_variables": {
        "color-admonition-background": "transparent",
    },
}
```

per type, furo uses `--color-admonition-title--note`, `--color-admonition-title-background--note` and so on for each of the names above. a fully custom admonition with its own icon is a css job — see [injecting](../theme/07-injecting.md) and [furo's custom admonitions](https://pradyunsg.me/furo/reference/admonitions/#custom-admonitions).

## collapsible
not an admonition, but the usual next question: `{dropdown}` from sphinx-design hides a block behind a clickable header. see [sphinx-design](../extensions/sphinx-design.md).

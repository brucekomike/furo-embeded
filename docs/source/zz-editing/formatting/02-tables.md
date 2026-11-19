# tables

## pipe table
the everyday form, github flavoured markdown:

````md
| header     | another header |
|------------|----------------|
| field 1    | something      |
| field 2    | something else |
````

| header     | another header |
|------------|----------------|
| field 1    | something      |
| field 2    | something else |

the dashes in the separator row are only structural, one each is enough. padding the columns to line up makes the source readable and changes nothing in the output.

## column alignment
colons in the separator row:

````md
| left   | center  | right  |
|:-------|:-------:|-------:|
| a      | b       | c      |
| longer | content | here   |
````

| left   | center  | right  |
|:-------|:-------:|-------:|
| a      | b       | c      |
| longer | content | here   |

## inline markup in cells
works as you would expect:

````md
| markup      | renders as        |
|-------------|-------------------|
| `*x*`       | *x*               |
| `` `code` ``| `code`            |
| a [link](https://example.com) | a link |
````

| markup      | renders as        |
|-------------|-------------------|
| `*x*`       | *x*               |
| `` `code` ``| `code`            |
| a [link](https://example.com) | a link |

:::{note}
a cell cannot contain a blank line, so a pipe table can never hold two paragraphs, a list or a code fence. that is the point where you need `{list-table}`.
:::

## when markdown is not enough
`{list-table}` is the escape hatch — cells hold arbitrary block content, and it can span rows and columns.

````md
```{list-table}
:header-rows: 1
:widths: 1 2

* - header
  - another header
* - a cell with a list

    - one
    - two
  - a cell with a fence

    ```sh
    make html
    ```
* - spans both
  -
```
````

```{list-table}
:header-rows: 1
:widths: 1 2

* - header
  - another header
* - a cell with a list

    - one
    - two
  - a cell with a fence

    ```sh
    make html
    ```
* - spans both
  -
```

`:header-rows:` marks how many leading rows are headers, `:widths:` sets relative column widths.

RST has two more table forms that markdown and MyST directives both lack — grid tables, which draw the borders in ascii, and simple tables, which align by column width. they can express row spans more compactly than `{list-table}`. if you ever need one, that is the case for putting an `.rst` file in the tree: `source_suffix` in `conf.py` already maps `.rst` to `restructuredtext`.

## long tables
furo gives the page body a fixed max width. a wide table overflows it and gets cut off rather than scrolling. three ways out:

- fewer columns, shorter cells
- `{list-table}` with `:widths:`
- wrap it in a scrolling div

````md
```{div} table-wrapper
| a | b | c | d | e | f |
|---|---|---|---|---|---|
```
````

`{div}` comes from sphinx-design, see [extensions](../extensions/sphinx-design.md). pair it with css in `_static`:

```css
.table-wrapper { overflow-x: auto; }
```

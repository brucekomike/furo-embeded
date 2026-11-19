# lists

## bullet

````md
- a point
- another point
  - nested, indented two spaces or more
  - they can just show up inline
- multiple paragraphs are allowed

  blank line, then indent to the same level
````

- a point
- another point
  - nested, indented two spaces or more
  - they can just show up inline
- multiple paragraphs are allowed

  blank line, then indent to the same level

markdown is forgiving here — nesting needs two or more spaces, and blank lines around a nested list are optional. RST is stricter: exactly two spaces, and blank lines required.

## numbered

````md
1. first
2. second
   1. nested numbering restarts at 1
3. third
````

1. first
2. second
   1. nested numbering restarts at 1
3. third

the numbers you type are ignored, only the order matters. `1.` on every line renders exactly the same, which makes inserting an item a one line change:

````md
1. first
1. second
1. third
````

1. first
1. second
1. third

## start at a number other than 1
the **first** number in a list is honoured, the rest are not:

````md
3. three
4. this renders as 4
5. and this as 5
````

3. three
4. this renders as 4
5. and this as 5

so a list that has to begin at 3 just says `3.` first. continuing a list that was interrupted by a heading or a paragraph is the case markdown cannot express — that needs RST.

## definition
`deflist` is enabled in `conf.py`. a term on its own line, then `:` indented by one space:

````md
term one
: what term one means

term two
: what term two means, which can run
  over more than one line
````

term one
: what term one means

term two
: what term two means, which can run
  over more than one line

good for glossaries and for option lists, and it is the one list type markdown has no native syntax for.

## task list
`tasklist` is enabled in `conf.py`:

````md
- [x] done
- [ ] still to do
- [ ] and this
````

- [x] done
- [ ] still to do
- [ ] and this

:::{note}
the boxes render but are not clickable. myst-parser has `enable_checkboxes` for that, off by default:

```py
myst_enable_checkboxes = True
```

it turns them into real form inputs, which only makes sense if something behind them stores the state.
:::

a task list also works with numbered items, and nested ones need the same indentation as any other list.

## lists inside other things
list items can hold code fences, admonitions and tables. indent the block to the level of the item text:

````md
1. a step that runs a command

   ```sh
   make html
   ```

1. a step worth flagging

   :::{warning}
   this one is destructive
   :::
````

1. a step that runs a command

   ```sh
   make html
   ```

1. a step worth flagging

   :::{warning}
   this one is destructive
   :::

:::{tip}
blank line plus matching indentation is what makes the block part of the list item rather than a sibling of the list. miss the indentation and the numbering restarts.
:::

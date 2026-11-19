# tabs
two extensions here provide tabs, and both are already enabled.

| extension | markup | best for |
|---|---|---|
| `sphinx_inline_tabs` | `{tab}` | a couple of alternatives, inline in prose |
| `sphinx_design` | `{tab-set}` + `{tab-item}` | structured sets, sync, nesting |

## sphinx-inline-tabs
the smallest thing that works. one directive per tab:

`````md
````{tab} *nux
```sh
source .venv/bin/activate
```
````

````{tab} windows
```sh
.venv\Scripts\activate
```
````
`````

````{tab} *nux
```sh
source .venv/bin/activate
```
````

````{tab} windows
```sh
.venv\Scripts\activate
```
````

consecutive `{tab}` directives at the same level group themselves into one tab set, so there is no wrapper to open and close. the argument is the label.

this is the form the template's own [building](../tutorial/04-building.md) page uses.

## sphinx-design
an explicit wrapper, which means tabs can be nested and options can go on the set:

`````md
````{tab-set}
```{tab-item} label one
content one
```

```{tab-item} label two
content two
```
````
`````

````{tab-set}
```{tab-item} label one
content one
```

```{tab-item} label two
content two
```
````

`{tab-item}` options:

| option | does |
|---|---|
| `:selected:` | open this tab by default instead of the first |
| `:sync:` | a sync key, shared across tab sets |
| `:class-container:` | css classes on the tab |
| `:class-content:` | css classes on the body |

`{tab-set}` takes `:class:` and `:sync-group:`.

### synced tabs
the reason to reach for `{tab-set}` over `{tab}`. two sets on one page, and choosing in one chooses in the other:

`````md
````{tab-set}
```{tab-item} macos
:sync: macos
brew install graphviz
```

```{tab-item} debian
:sync: debian
apt install graphviz
```
````
`````

the second set is the same markup with different commands, and the same `:sync:` keys:

````{tab-set}
```{tab-item} macos
:sync: macos
brew install graphviz
```

```{tab-item} debian
:sync: debian
apt install graphviz
```
````

````{tab-set}
```{tab-item} macos
:sync: macos
brew install mermaid-cli
```

```{tab-item} debian
:sync: debian
apt install mermaid-cli
```
````

pick one of the two sets above and the other follows, and the choice survives a page reload. that is `:sync:` doing the work — matching keys, no javascript of your own.

## code tabs
`{tab-set-code}` takes code fences and makes one tab per fence, labelling each from its language:

`````md
````{tab-set-code}
```python
print("hello")
```

```javascript
console.log("hello");
```
````
`````

````{tab-set-code}
```python
print("hello")
```

```javascript
console.log("hello");
```
````

no `{tab-item}` wrappers and no labels to type, which is the whole appeal when the same thing is shown in three languages.

## which to use
`{tab}` when the tabs are a couple of lines and sit inside prose — less markup, easier to read in the source. `{tab-set}` when you need sync, nesting, a selected default, or a body that is more than code.

:::{tip}
furo's own reference pages use `{tab}` to show the markdown and the RST form of the same markup side by side. this project is markdown first, so there is usually only one form to show — but the pattern is a good one when a snippet really does have two spellings.
:::

## upstream
- [furo: tabs](https://pradyunsg.me/furo/reference/tabs/)
- [sphinx-inline-tabs](https://github.com/pradyunsg/sphinx-inline-tabs#readme)
- [sphinx-design tabs](https://sphinx-design.readthedocs.io/en/latest/tabs.html)

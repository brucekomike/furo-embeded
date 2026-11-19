# sphinx-inline-tabs
one directive, no options, no configuration.

```py
extensions = ["sphinx_inline_tabs"]
```

## use

`````md
````{tab} label
content
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

consecutive `{tab}` directives at the same nesting level become one tab set. the argument is the label, the body is the content. that is the whole extension.

## what it does not do

| want | use instead |
|---|---|
| remember the reader's choice across sets | `{tab-set}` with `:sync:`, see [sphinx-design](sphinx-design.md) |
| open a tab other than the first | `{tab-item}` with `:selected:` |
| nest tabs | `{tab-set}` inside `{tab-item}` |
| css classes on a tab | `{tab-item}` with `:class-container:` |

`{tab}` and `{tab-set}` can be mixed on the same page, they just will not sync with each other.

## the config
there is none. the package registers no config values at all — `pip show sphinx-inline-tabs` and grep for `add_config_value` comes up empty. it adds the `{tab}` directive and a stylesheet, and that is it.

## upstream
[sphinx-inline-tabs readme](https://github.com/pradyunsg/sphinx-inline-tabs#readme)

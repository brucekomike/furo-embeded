# graphviz
render graphs from [DOT](https://graphviz.org/doc/info/lang.html) text with [graphviz](https://graphviz.org/).

## enable
unlike mermaid, graphs are rendered at build time, so the tool itself must exist on the machine that builds the docs:

- install graphviz (`dot`):
  - macos: `brew install graphviz`
  - debian / ubuntu: `apt install graphviz`
- add `'sphinx.ext.graphviz',` to `extensions` in `conf.py`.
  it is built into sphinx, so no pip package is needed.
- optional, keep images sharp in the browser:

```py
graphviz_output_format = 'svg'
```

## use
put the dot code into a `graphviz` directive:

````
```{graphviz}
digraph G {
  rankdir=LR
  download --> extract --> run
}
```
````

`{digraph}` (directed) and `{graph}` (undirected) are shortcut directives, use them without the outer `digraph G {}` wrapper:

````
```{digraph}
rankdir=LR
download --> extract --> run
```
````

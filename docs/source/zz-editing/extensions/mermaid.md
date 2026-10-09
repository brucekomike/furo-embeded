# mermaid
draw diagrams from text with [mermaid](https://mermaid-js.github.io/mermaid/).

## enable
this extension is off by default in this template:
- `sphinxcontrib-mermaid` is already in `requirements.txt`
- un-comment `'sphinxcontrib.mermaid',` in `conf.py`

rendering runs in the browser (the js is loaded from cdn),
so nothing extra needs to be installed at build time.

## use
put the diagram code into a `mermaid` code fence:

````
```{mermaid}
flowchart LR
  draft --> review --> publish
```
````

as `colon_fence` is enabled in `myst_enable_extensions`, this works too:

```
:::{mermaid}
flowchart LR
  draft --> review --> publish
:::
```

see the [mermaid gallery](https://mermaid.js.org/examples/) for more diagram types.

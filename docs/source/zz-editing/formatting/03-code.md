# code

## the fence
three backticks, then a language name:

`````md
````sh
make html
````
`````

```sh
make html
```

the language name picks the pygments lexer. leave it out and the block is highlighted with whatever `highlight_language` says — this template sets it to `'text'`, so an unlabelled fence gets **no** highlighting:

````md
```
no language, no highlighting
```
````

```
no language, no highlighting
```

use `text` explicitly when you mean it:

````md
```text
a tree, some output, a config fragment
```
````

```text
a tree, some output, a config fragment
```

common lexer names here: `sh`, `bash`, `py`, `python`, `yaml`, `json`, `toml`, `ini`, `html`, `css`, `javascript`, `md`, `dockerfile`, `diff`. the full list is the [pygments lexers](https://pygments.org/docs/lexers/).

## the indent form
four spaces of indentation also makes a code block. it is fine for a short literal, but it cannot carry a language, so it never gets highlighting and it is easy to trigger by accident inside a list. prefer fences.

## inline code

````md
run `sphinx-build -b html source build` to build.
````

run `sphinx-build -b html source build` to build.

to show a backtick inside inline code, use more backticks on the outside than any run inside:

`````md
````a `backtick` inside````
`````

````a `backtick` inside````

## line numbers and highlighting
needs the directive form, because these are options:

`````md
````{code-block} python
:caption: docs/source/conf.py
:linenos:
:emphasize-lines: 2-3
extensions = [
    "myst_parser",
    "sphinx_design",
]
html_theme = "furo"
````
`````

```{code-block} python
:caption: docs/source/conf.py
:linenos:
:emphasize-lines: 2-3
extensions = [
    "myst_parser",
    "sphinx_design",
]
html_theme = "furo"
```

options go straight after the opening fence, one per line, before the code.

| option | does |
|---|---|
| `:caption:` | a title above the block, and an anchor for linking |
| `:linenos:` | number the lines |
| `:emphasize-lines:` | highlight lines, `2-3` and `1,4` both work |
| `:name:` | a label so `{ref}` can point at the block |
| `:class:` | extra css classes on the wrapper |

:::{caution}
`:emphasize-lines:` counts lines in the **code**, starting at 1 on the first line after the options. a blank line inside the code still counts. if the wrong lines light up, that is nearly always it.
:::

`{code-block}`, `{code}` and `{sourcecode}` are three names for the same directive.

## number lines without a directive
myst can add line numbers to plain fences per language:

```py
myst_number_code_blocks = ["python", "sh"]
```

not set in this template.

## copy button
`sphinx-copybutton` is enabled, so every highlighted block gets a copy button in the top right. it needs no markup.

strip shell prompts out of what gets copied:

```py
copybutton_prompt_text = r">>> |\.\.\. |\$ |# "
copybutton_prompt_is_regexp = True
```

details in [copybutton](../extensions/copybutton.md).

## include a file instead of pasting it

````md
```{literalinclude} ../../conf.py
:language: python
:start-after: "# -- General configuration"
:end-before: "# -- Options for HTML output"
```
````

the path is relative to the file doing the including, so from `zz-editing/formatting/` up to `source/` is `../../`. keeps a snippet honest, because it is the real file. `{literalinclude}` also takes `:lines:`, `:emphasize-lines:` and `:caption:`.

## literal markup, not executed
a fence is literal, so showing sphinx markup is safe inside one:

`````md
````md
```{note}
this stays text, it does not become a note
```
````
`````

````md
```{note}
this stays text, it does not become a note
```
````

that is the trick behind every "source then result" pair on these pages.

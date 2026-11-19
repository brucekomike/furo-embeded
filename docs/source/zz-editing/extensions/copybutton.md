# sphinx-copybutton
a copy button in the top right of every code block. pure javascript, nothing to write in the pages.

```py
extensions = ["sphinx_copybutton"]
```

already on here. try it on the block below:

```sh
$ pip install -r requirements.txt
$ make html
```

## shell prompts
the button copies the prompt characters along with the command by default, which is annoying to paste into a terminal. two options fix it:

```py
copybutton_prompt_text = "$ "
```

copies only the lines that start with `$ `, and strips the `$ `. try the block above with this set — the `$ ` disappears from what lands on the clipboard.

several prompts at once, with a regex:

```py
copybutton_prompt_text = r">>> |\.\.\. |\$ |# "
copybutton_prompt_is_regexp = True
```

that covers the python repl, its continuation lines, a shell and a root shell. `copybutton_prompt_is_regexp = True` is what makes the string a pattern rather than a literal.

## related options

| option | default | does |
|---|---|---|
| `copybutton_only_copy_prompt_lines` | `True` | with a prompt set, skip lines that do not have one |
| `copybutton_remove_prompts` | `True` | strip the prompt out of what is copied |
| `copybutton_copy_empty_lines` | `True` | keep blank lines |
| `copybutton_line_continuation_character` | `""` | e.g. `"\\"`, joins continued lines into one |
| `copybutton_here_doc_delimiter` | `""` | skips heredoc bodies |
| `copybutton_selector` | `"div.highlight pre"` | css selector for which blocks get a button |
| `copybutton_exclude` | `".linenos"` | css selector for parts left out of the copy |
| `copybutton_image_svg` | `""` | replace the icon with your own inline svg |
| `copybutton_image_path` | `""` | or with an image file |

the defaults are sensible for this template. `copybutton_selector` is the one to reach for if you add a custom block type that should not get a button.

## which blocks
sphinx wraps highlighted code in `div.highlight > pre`, which is what the default selector matches. a block produced by ```` ```{code-block} ```` gets one, and so does a plain fence, because both end up in that structure.

an indented four space literal block does too, but with no language it is highlighted as `highlight_language` — `'text'` in this template.

## upstream
[sphinx-copybutton documentation](https://sphinx-copybutton.readthedocs.io/)

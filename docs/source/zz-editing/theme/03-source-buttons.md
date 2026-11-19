# source buttons
the edit and view links at the top right of every page. they come from [sphinx-basic-ng](https://sphinx-basic-ng.readthedocs.io/), which furo builds on.

## which buttons show

```py
html_theme_options = {
    "top_of_page_buttons": ["view", "edit"],
}
```

any subset of `"edit"` and `"view"`, in any order. `[]` hides both.

## github.com, gitlab.com, bitbucket.org
these three hosts are recognised from the repository url, which is what this template ships with:

```py
html_theme_options = {
    "source_repository": "https://github.com/brucekomike/furo-embeded",
    "source_branch": "main",
    "source_directory": "docs/source/",
}
```

furo builds both links from those three.

## any other host
a self hosted gitlab, gitea, codeberg or forgejo instance is **not** recognised. the templates have to be spelled out:

```py
html_theme_options = {
    "source_edit_link": "https://gitlab.example.com/OWNER/REPO/-/edit/main/docs/source/{filename}",
    "source_view_link": "https://gitlab.example.com/OWNER/REPO/-/blob/main/docs/source/{filename}",
}
```

`{filename}` is replaced with `pagename + page_source_suffix`, so the page you are reading becomes `zz-editing/theme/03-source-buttons.md`.

:::{caution}
set **both**, even if you only want one button.

the edit and view links are built by two independent template macros, and each one falls back to parsing `source_repository` when its own key is missing. setting only `source_view_link` still prints

```
Could not understand `source_repository` provided
```

twice on every page. on a 24 page site that is 48 warnings from one missing key.
:::

:::{note}
furo does not check these urls for you — no `{filename}` requirement, no correctness check. click one after building.
:::

the gitlab line is already sitting commented out at the bottom of `html_theme_options` in this template's `conf.py`.

`source_repository` / `source_branch` / `source_directory` can stay in place alongside them, they act as the fallback.

## link to the copied source instead
if none of the above is configured and sphinx copies sources into the build (the default), the view button points at the `.md` file sitting next to the built page. turn that behaviour off with:

```py
html_copy_source = False
html_show_sourcelink = False
```

## read the docs
projects built on read the docs from a github repository get these buttons inferred from the rtd build environment, with no config at all. any explicit key above wins over the inference.

## upstream
[furo: changing buttons on page](https://pradyunsg.me/furo/customisation/top-of-page-buttons/)

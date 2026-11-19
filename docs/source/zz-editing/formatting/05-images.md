# images
one example file ships with the template at `_static/example.svg`, used throughout this page. from here the relative path is `../../_static/example.svg`.

## the markdown form

````md
![a short description](../../_static/example.svg)
````

![a short description](../../_static/example.svg)

the alt text is required by the syntax and read out by screen readers. sphinx copies the file into the build and fixes up the url.

## with options
markdown has no place to put a width, an alignment or a css class, so use the directive:

````md
```{image} ../../_static/example.svg
:align: center
:width: 200px
:class: my-image
```
````

```{image} ../../_static/example.svg
:align: center
:width: 200px
```

| option | does |
|---|---|
| `:align:` | `left`, `center`, `right` |
| `:width:` / `:height:` | any css length |
| `:scale:` | a percentage |
| `:class:` | extra css classes on the `<img>` |
| `:alt:` | alt text, when the markdown form is not enough |
| `:target:` | wrap the image in a link |

## with a caption
a caption needs a `{figure}`, which is an image plus surrounding text:

````md
```{figure} ../../_static/example.svg
:align: center
:width: 240px
:name: example-figure

the caption, which is what `{ref}`example-figure`` links to.
```
````

```{figure} ../../_static/example.svg
:align: center
:width: 240px
:name: example-figure

the caption, which is what ``{ref}`example-figure` `` links to.
```

everything after the blank line is the caption. `:name:` gives the figure a label so [links](04-links.md) can point at it. `:figclass:` puts a class on the figure wrapper, `:class:` on the image inside it.

## different image per color mode
furo ships `only-light` and `only-dark` classes. put one on each of two images and the browser shows whichever matches:

````md
```{image} diagram-light.svg
:class: only-light
```

```{image} diagram-dark.svg
:class: only-dark
```
````

```{image} ../../_static/example.svg
:width: 240px
:class: only-light
```

```{image} ../../_static/example.svg
:width: 240px
:class: only-dark
```

the two above are the same file, so nothing appears to change — flip your browser theme and one of the two slots stays visible. the mechanism is what matters: both images are in the html, and css hides one.

on a `{figure}` the equivalent option is `:figclass:`, because `:class:` is taken by the image:

````md
```{figure} diagram-light.svg
:figclass: only-light
```
````

an inline `<img>` in raw html takes the class directly, and so does a `{grid-item-card}` through `:class-item:`.

## svg or png
svg is sharper at any zoom, smaller for diagrams, and can inherit `currentColor` so it adapts to dark mode by itself. that is the reason `example.svg` uses a stroke of the brand blue rather than a baked in color.

use png or webp for photographs. furo's own docs use `html_logo` with an svg for exactly this reason.

## remote images

````md
![alt text](https://example.com/diagram.png)
````

sphinx does not download these, the browser does. that means the image breaks when the reader is offline, and the remote host sees your traffic. prefer committing the file into `_static`.

## what is already here

```py
html_static_path = ['_static']
ogp_use_first_image = True
```

`ogp_use_first_image` makes the opengraph card pick up the first image on each page — see [opengraph](../extensions/opengraph.md). `html_logo` and `html_favicon` are commented out in `conf.py`, ready to fill in — see [logo](../theme/02-logo.md).

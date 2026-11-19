# math
maths in this template is **half enabled**, and the half that is missing fails silently.

## the two halves

| half | where | state here |
|---|---|---|
| parsing `$x^2$` and `\begin{equation}` | `myst_enable_extensions` | on — `dollarmath` and `amsmath` |
| rendering it in the browser | `extensions` | **off** — `sphinx.ext.mathjax` is commented out |

so the markup is understood and produces math nodes, but nothing is loaded to draw them. the build reports no warning and no error: the raw LaTeX just appears as literal text on the page, `\int_0^1 x^2 dx` and all.

that silence is the trap. if maths looks like source code in the browser, this is why.

## turn it on
uncomment the line in `conf.py`:

```py
extensions = [
    ...,
    'sphinx.ext.mathjax',
]
```

mathjax then loads from a cdn at page view time, so nothing extra is installed and the build stays fast.

## offline, or air gapped
the cdn is the problem for an internal site. host mathjax yourself:

1. download it from <https://www.mathjax.org/#installnow>, or take the whole thing from
   <https://github.com/mathjax/MathJax/archive/master.zip>
2. put the file in `source/_static`, e.g. `_static/tex-svg-full.js`
3. point `mathjax_path` at it:

```py
mathjax_path = 'tex-svg-full.js'
```

the path is relative to `html_static_path`, same rule as [logo](../theme/02-logo.md). the line in `conf.py` says `tex-svg.js` — match whatever filename you actually dropped in.

`tex-svg-full` is the combined build with every input and output format, and it is the largest. `tex-svg` is enough for latex in and svg out, which is all a docs site needs, and it is a fraction of the size.

## markup
with `dollarmath` on, inline maths uses single dollars and a block uses double:

````md
inline $x^2$ and a block:

$$
\int_0^1 x^2 \, dx = \frac{1}{3}
$$
````

a labelled block, so `{eq}` can point at it:

````md
$$
e^{i\pi} + 1 = 0
$$ (euler)

see {eq}`euler`.
````

`dmath_allow_labels`, `dmath_allow_space` and `dmath_double_inline` tune the dollar parsing; the defaults are fine. `dmath_double_inline = True` is what makes `$...$` inside a single line behave like `$$...$$`.

with `amsmath` on, the ams environments work directly, no dollars:

````md
```{math}
\begin{align}
a &= b + c \\
d &= e + f
\end{align}
```
````

```` ```{math} ```` is the sphinx directive and works regardless of the myst extensions — it is the form to reach for when a `$$` block is being difficult about its surroundings.

## the other renderers

| extension | how | trade off |
|---|---|---|
| `sphinx.ext.mathjax` | javascript in the browser | nothing to install, needs the js at view time |
| `sphinx.ext.imgmath` | latex rendered to png or svg at build time | works with js off and in non-html output, needs latex and dvisvgm installed |
| `sphinx.ext.jsmath` | an older javascript path | needs you to host jsmath, no advantage over mathjax |

`imgmath` is the one to pick for pdf or epub output, since mathjax is html only:

```py
extensions = ['sphinx.ext.imgmath']
imgmath_image_format = 'svg'
```

## upstream
- [sphinx: math support](https://www.sphinx-doc.org/en/master/usage/extensions/math.html)
- [myst: mathematics](https://myst-parser.readthedocs.io/en/latest/syntax/math.html)

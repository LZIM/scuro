# A memoir-based article template for markdown

This pandoc template and Makefile make it possible to generate an article-length document in PDF, making use of some of the layout and formatting capacities of the `memoir` package. The included Makefile allows us to govern xelatex and biber with a single `make` (relying on latexmk to determine the number of passes needed).

The included `memoir-article.latex` template adds support for a few further metadata variables:

`anon`: Remove author information (including from PDF metadata) for anonymous submission.

`thanks`: An unnumbered note is added to the first package with the contents of this variable (which can be any LaTeX).

Fonts: the `mainfont`, `mainfontoptions`, etc. metadata variables work as in the pandoc default. The typeface for the title block can be configured with `titlefont`. (If none is specified, the main font is used.)

Page headers and footers: these can be set with metadata variables `olhead` (odd-side left header), `ecfoot` (even-side center footer), etc.; these variables can contain LaTeX (e.g. `ecfoot: '\thepage'`).

If the title block layout used here does not appeal, set `manual-title: true` (in which case `\maketitle` is not used) and compose one as you prefer.

On my system, the example [paper.md](paper.md) is converted into this PDF: [paper.pdf](http://andrewgoldstone.com/memarticle/paper.pdf). I have used a commercial font, Garamond Premier Pro. Change `mainfont` (and `titlefont`, and the corresponding `*options`) to your own choices. The name of any system font should work.

Note in the example `paper.md` file the use of `classoption` to set symmetric margins. More exacting control over the overall page layout is best achieved by writing a file of LaTeX using `memoir`'s layout facilities to include in the preamble. If the styling file is called `layout.tex`, then change the Makefile definition of `PANDOC_OPTIONS` to insert the relevant file into the preamble:

```Make
PANDOC_OPTIONS := -H layout.tex
```

## Chicago Style

To use the marvelous `biblatex-chicago` package for *Chicago Manual of Style* bibliography generation, set:

```yaml
biblatex: true
biblatex-chicago: true
biblatexoptions: notes
bibliography: ../mybib.bib
```

Note that the bibliography path is relative to the `out` directory that is created by the Makefile. The `biblatexoptions` are given to `biblatex-chicago` (e.g. you might try `[notes,short,noibid]`).

Footnotes are also formatted according to Chicago's recommendations. To use widely spaced ellipses, specify `chicago-ellipses: true`.


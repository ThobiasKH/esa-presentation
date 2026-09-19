# Edge Geography: modular portrait poster

A custom LaTeX project for the ESA 2026 paper by Thobias Kvalvik Høivik and
Erlend Raa Vågset. A1 portrait is the default. There are three empty figure
panels and a reserved HVL logo slot. The text is a starting draft for discussion
and editing, not a final print submission.

## Build

Run commands from the directory containing `poster.tex`:

```sh
latexmk -pdf poster.tex
```

This produces `poster.pdf`. You can also open `poster.tex` in VimTeX and compile
as usual. Its first line requests pdfLaTeX. Included section files have root
comments pointing back to `poster.tex`, so VimTeX can find the main document
while you edit a section. Start in this project directory so that an older
Gemini document is not selected as your main file.

Without latexmk, run `pdflatex poster.tex` twice.

There are no custom fonts, Gemini dependencies, bibliography runs, external
graphics, or shell-escape requirements. The packages used are conventional
TeX Live/MiKTeX packages: Latin Modern (`lmodern`), `geometry`, `amsmath`,
`amssymb`, `etoolbox`, `xcolor`, `graphicx`, `tikz`, `tcolorbox`, and `hyperref`.

## Choose the physical size

Edit one line in `config.tex`:

```latex
\providecommand{\PosterPaper}{A1}
```

The accepted values are `A0`, `A1` and `A2`; all three are portrait.

| Size | Width x height | Approximate main body text |
| --- | --- | --- |
| A0 | 841 x 1189 mm | 34 pt |
| A1 (default) | 594 x 841 mm | 24 pt |
| A2 | 420 x 594 mm | 17 pt |

The source scales fonts, margins, gutters, and figure heights together. A2
works best for close reading; if people should read the poster while standing
farther away, start with A1 or A0. The setting changes the PDF's actual page
size, so print at 100% once the desired size is selected.

You can also build another size without changing the default:

```sh
latexmk -pdf poster-A0.tex
latexmk -pdf poster-A2.tex
```

## Where to edit

| File or folder | What belongs there |
| --- | --- |
| `poster.tex` | Short entry point; normally leave it alone |
| `config.tex` | Paper size, font sizes, spacing, figure heights, colours, logo path |
| `layout.tex` | Reading order and column proportions |
| `style.tex` | Definitions of the reusable layout components |
| `content/metadata.tex` | Title, authors, affiliation and links |
| `content/game.tex` | Game rules and motivation |
| `content/results.tex` | Main result cards and the FPT result |
| `content/hardness.tex` | Reduction sketch |
| `content/algorithm.tex` | Interface algorithm sketch |
| `content/outlook.tex` | Open question |
| `content/demo.tex` | QR-code invitation to the live browser demo |
| `content/footer.tex` | Paper links and citation |
| `figures/` | One short file per figure; can contain TikZ directly |
| `assets/` | PDF/PNG/JPEG figures and, later, the HVL logo |

## Workshop the layout

`layout.tex` uses a small set of components:

```latex
% Two natural-height columns; the fraction applies after subtracting the gutter.
\PosterColumns{0.5}{
  \input{content/hardness}
}{
  \input{content/algorithm}
}

% A full-width section followed by the common gap.
\input{content/outlook}
\PosterGap
```

Change `0.5` to `0.6` for a 60/40 split, or swap the input files to reorder
sections. To add a new section, create a file in `content/` and input it from
`layout.tex`. Most rows have natural height, so adding or removing text moves
later rows instead of silently overlapping them. Result cards and figure panels
have explicit heights; adjust them if their content becomes too large.

Useful component commands:

```latex
\PosterHeading{05}{A new section}
\PosterHeading[PosterHardness]{05}{A differently coloured section}
\PosterPara                 % consistent paragraph gap
\PosterSpace{6}             % 6 mm at A1, scaled for other sizes
{\PosterSmallFont A short caption.\par}
```

Keep `\par` inside a group that changes the font size, as in the last example,
so multiline paragraphs use the intended line spacing.

After substantial edits, check that the output is still one page. The project
emits a warning if it spills onto a second page. This is a layout warning, not
automatic shrinking: reduce content or figure heights and review the result.

## Replace figures and add the logo

Add `assets/game.pdf`, `assets/hardness.pdf`, and `assets/algorithm.pdf`.
They replace their respective placeholders automatically and retain their
aspect ratios. Figure heights are set together in `config.tex`.

For different filenames, change the calls in `figures/`. For a native TikZ
figure, replace the contents of the relevant `figures/*.tex` file. Use
`\linewidth` to refer to the current column width.

Add an official HVL logo as `assets/hvl-logo.pdf` whenever you are ready. Its
path is configurable; the header preserves its aspect ratio. No logo is
included or recreated in this project.

The demo callout uses `assets/game-qr.pdf` and links to
`https://thobiashoivik.com/lab/geography-playground`. The QR code is also
available as `assets/game-qr.svg` if you want to reuse it in the website or in
another design.

If you want empty spaces without labels while editing, change these flags:

```latex
\PosterShowFigurePlaceholdersfalse
\PosterShowLogoPlaceholderfalse
```

## Content sources

- Published paper: https://doi.org/10.4230/LIPIcs.ESA.2026.114
- Full version: https://arxiv.org/abs/2607.03189

The three result statements distinguish pathwidth hardness, the XP algorithm
for tree-partition width on simple graphs, and FPT for directed Edge Geography
under treewidth plus maximum degree. Review all wording and figures before
printing.

## Included previews and verification

The `previews/` folder contains the compiled A1, A0, and A2 PDFs. All three
were built with pdfLaTeX through latexmk, checked for the correct physical
page dimensions, and visually inspected. Each is a single portrait page with
embedded fonts and visible text. There were no missing-character or
overfull-box warnings in the final build logs. The source files compile
without any of the preview PDFs present.

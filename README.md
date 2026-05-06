# Diploma Thesis Template (equivalent to Master's Thesis) – University of Patras (ECE)

A **LaTeX template** for preparing a Diploma Thesis (equivalent to a Master's Thesis) at the
**Department of Electrical and Computer Engineering (ECE), University of Patras**.

The template is preconfigured with the formatting, fonts, bibliography style, and bilingual
(Greek / English) support that the department's thesis guidelines expect, so you can focus on
writing your thesis instead of fighting LaTeX.

> **Important:** You **must compile with XeLaTeX** (not pdfLaTeX or LuaLaTeX). Greek text and
> the `fontspec`/`Noto Sans` configuration in `main.tex` will not work otherwise.

---

## Table of Contents

- [Repository Structure](#repository-structure)
- [Requirements](#requirements)
- [How to Compile](#how-to-compile)
  - [Command Line](#command-line)
  - [Overleaf](#overleaf)
  - [TeXstudio](#texstudio)
  - [VS Code (LaTeX Workshop)](#vs-code-latex-workshop)
- [Customizing the Template](#customizing-the-template)
  - [Cover Page](#cover-page)
  - [Abstracts and Acknowledgements](#abstracts-and-acknowledgements)
  - [Adding Chapters](#adding-chapters)
  - [Figures](#figures)
  - [Bibliography](#bibliography)
  - [Acronyms / Glossary](#acronyms--glossary)
  - [Cross-references](#cross-references)
- [Packages Used](#packages-used)
- [Troubleshooting](#troubleshooting)
- [License](#license)
- [Acknowledgments](#acknowledgments)

---

## Repository Structure

```
patras-thesis-template-latex/
├── main.tex                      # Main thesis file – compile this with XeLaTeX
├── thesis.bib                    # Bibliography database (BibLaTeX / Biber)
├── cover.pdf                     # Pre-rendered cover page (Greek & English)
│
├── content/                      # All thesis text lives here
│   ├── abstract-eng.tex          # English abstract
│   ├── abstract-gr.tex           # Extended Greek abstract (required for English theses)
│   ├── acknowledgements.tex      # Acknowledgments
│   └── introduction.tex          # Example chapter (Introduction)
│
├── img/                          # Figures and images
│   └── figure.jpg                # Example figure used in the introduction
│
├── README.md                     # This file
└── LICENSE                       # MIT License
```

You can extend the template by creating additional chapter files inside `content/`
(e.g. `content/chapter2.tex`, `content/methodology.tex`, `content/results.tex`,
`content/conclusion.tex`) and including them in `main.tex` with `\input{content/<filename>}`.

---

## Requirements

To compile this template you need:

1. **A full TeX distribution** that includes XeLaTeX and Biber:
   - [TeX Live](https://www.tug.org/texlive/) (Linux / macOS / Windows)
   - [MacTeX](https://www.tug.org/mactex/) (macOS)
   - [MiKTeX](https://miktex.org/) (Windows)
2. **The Noto Sans font** (used as the main font via `\setmainfont{Noto Sans}`).
   - On most modern Linux distributions it is preinstalled or available via the package manager
     (e.g. `sudo apt install fonts-noto`).
   - On macOS / Windows, install it from [Google Fonts – Noto Sans](https://fonts.google.com/noto/specimen/Noto+Sans).
   - If you prefer not to install Noto, you can change the `\setmainfont{...}` line in `main.tex`
     to any other system font (e.g. `Liberation Serif`, `Times New Roman`, `Latin Modern Roman`).
3. **A LaTeX editor** (optional but recommended): TeXstudio, TeXworks, VS Code with the
   *LaTeX Workshop* extension, or [Overleaf](https://www.overleaf.com/) (online).

---

## How to Compile

### Command Line

From the repository root, run:

```bash
xelatex main.tex
biber main
xelatex main.tex
xelatex main.tex
```

Why four commands?

- The first `xelatex` generates the `.aux`, `.bcf`, and `.glo` files.
- `biber` processes the bibliography from `thesis.bib`.
- The next two `xelatex` runs resolve cross-references, citations, table of contents,
  list of figures, list of tables, and the glossary/acronyms.

If you also want the acronyms list to be fully populated, run `makeglossaries main`
between the second and third `xelatex` runs:

```bash
xelatex main.tex
biber main
makeglossaries main
xelatex main.tex
xelatex main.tex
```

### Overleaf

1. Create a new project on [Overleaf](https://www.overleaf.com/) and upload all files
   (or import this repository directly via *New Project → Import from GitHub*).
2. Open **Menu → Settings**.
3. Set **Compiler** to **XeLaTeX**.
4. Set **TeX Live version** to a recent one (the latest available is fine).
5. Click **Recompile**. Overleaf will run XeLaTeX + Biber automatically.

### TeXstudio

1. Open `main.tex`.
2. Go to **Options → Configure TeXstudio → Build**.
3. Set **Default Compiler** to `XeLaTeX`.
4. Set **Default Bibliography Tool** to `Biber`.
5. Press **F5** (Build & View). Run twice if cross-references / TOC are not yet resolved.

### VS Code (LaTeX Workshop)

Add the following to your `.vscode/settings.json` (or the user settings) so that VS Code uses
XeLaTeX + Biber for this project:

```json
{
  "latex-workshop.latex.tools": [
    {
      "name": "xelatex",
      "command": "xelatex",
      "args": ["-synctex=1", "-interaction=nonstopmode", "-file-line-error", "%DOC%"]
    },
    {
      "name": "biber",
      "command": "biber",
      "args": ["%DOCFILE%"]
    }
  ],
  "latex-workshop.latex.recipes": [
    {
      "name": "xelatex → biber → xelatex × 2",
      "tools": ["xelatex", "biber", "xelatex", "xelatex"]
    }
  ],
  "latex-workshop.latex.recipe.default": "xelatex → biber → xelatex × 2"
}
```

Then open `main.tex` and press **Ctrl+Alt+B** (or run *LaTeX Workshop: Build LaTeX project*).

---

## Customizing the Template

### Cover Page

The cover page is shipped as a pre-rendered **`cover.pdf`** (it includes both the Greek and
English title page, as required by the department). It is included in `main.tex` via:

```latex
\includepdf[pages={-}]{cover.pdf}
```

To customize it:

- Edit `cover.pdf` directly using a PDF editor (replacing title, name, supervisor, year, etc.), **or**
- Replace `cover.pdf` with your own version (keep the same filename, or update the `\includepdf`
  path in `main.tex`).

### Abstracts and Acknowledgements

These short, front-matter sections are in `content/`:

- `content/abstract-eng.tex` – the English abstract. Replace the placeholder title, names, and
  text with your own. Update the keywords list at the bottom.
- `content/abstract-gr.tex` – the *extended* Greek abstract. According to the department's
  regulations, theses written in English must be accompanied by a paper-length Greek summary.
- `content/acknowledgements.tex` – your acknowledgments to supervisors, family, collaborators, etc.

### Adding Chapters

Create a new file under `content/` (e.g. `content/methodology.tex`) and start with:

```latex
\section{Methodology}\label{sec:methodology}

\subsection{Overview}
Your text here…
```

Then include it in `main.tex` after the introduction:

```latex
\input{content/introduction}
\input{content/methodology}
\input{content/results}
\input{content/conclusion}
```

> The template uses the `article` document class, so top-level structure is `\section` /
> `\subsection` / `\subsubsection` rather than `\chapter`. This matches the department's
> recommended layout for diploma theses.

### Figures

Place image files inside the `img/` directory and include them like this:

```latex
\begin{figure}[H]
    \centering
    \captionsetup{justification=centering}
    \includegraphics[width=0.7\linewidth, frame]{img/your-figure.png}
    \caption{Descriptive caption goes here.}
    \label{fig:your-label}
\end{figure}
```

You can then reference the figure with `\cref{fig:your-label}` (which will print
*Fig. N* automatically).

Supported formats with XeLaTeX: `.pdf`, `.png`, `.jpg`, `.jpeg`. For vector graphics,
prefer `.pdf` exported from Inkscape, Matplotlib, or TikZ.

### Bibliography

Add references to `thesis.bib` in BibLaTeX format. Example:

```bibtex
@article{Author2024,
  title   = {A great paper title},
  author  = {Author, First and Coauthor, Second},
  date    = {2024-05-01},
  journaltitle = {Journal of Examples},
  volume  = {12},
  number  = {3},
  pages   = {45--67},
  doi     = {10.1234/example.2024.001},
}
```

Cite it in your text with `\cite{Author2024}`. The bibliography is rendered in IEEE style
(`\usepackage[style=ieee]{biblatex}`) and is processed by **Biber**, not BibTeX.

### Acronyms / Glossary

Define acronyms near the top of `main.tex`:

```latex
\newacronym{cg}{CG}{Computer Graphics}
\newacronym{ml}{ML}{Machine Learning}
```

Then use them in the text with `\gls{cg}`. The first occurrence prints the full form
("Computer Graphics (CG)"); subsequent ones print just "CG". The acronym list is printed
automatically by `\printglossary[type=\acronymtype,nonumberlist]` in `main.tex`.

### Cross-references

The template loads `cleveref`, so use:

- `\cref{sec:introduction}` → "Section 1"
- `\cref{fig:first_figure}` → "Fig. 1"
- `\cref{tab:results}` → "Tab. 1"

`cleveref` automatically inserts the right label (Section / Fig. / Tab.) and capitalization.

---

## Packages Used

The template loads, among others:

| Package        | Purpose                                                                  |
|----------------|--------------------------------------------------------------------------|
| `babel`        | Greek + English language support                                         |
| `geometry`     | A4 paper, 1in top/bottom and 1.25in left/right margins                   |
| `fontspec`     | OpenType font selection (requires XeLaTeX/LuaLaTeX)                      |
| `microtype`    | Subtle typographic improvements (better justification, kerning)          |
| `graphicx`     | Image inclusion                                                          |
| `adjustbox`    | Alignment tweaks for figures                                             |
| `float`        | The `[H]` placement specifier for fixed-position figures                 |
| `caption`      | Captions labelled `Fig.` and `Tab.` (IEEE-style)                         |
| `subcaption`   | Sub-figures (e.g. `(a)`, `(b)` panels)                                   |
| `hyperref`     | Clickable links and PDF metadata (links are hidden by default)           |
| `cleveref`     | Smart cross-references (`\cref`)                                         |
| `biblatex`     | Bibliography management with IEEE style                                  |
| `siunitx`      | Typesetting of SI units and numbers                                      |
| `glossaries`   | Acronym list                                                             |
| `listings`     | Source code listings                                                     |
| `xcolor`       | Coloured text (used by `listings`)                                       |
| `pdfpages`     | Embedding the cover PDF                                                  |
| `titlesec`     | Custom paragraph formatting                                              |
| `indentfirst`  | Indent the first paragraph of every section                              |

---

## Troubleshooting

**"Font 'Noto Sans' not found" / `fontspec` error**
Install the Noto Sans font (see [Requirements](#requirements)), or change the
`\setmainfont{Noto Sans}` line in `main.tex` to a font that is installed on your system.

**Greek text appears as boxes / wrong characters**
You are most likely compiling with `pdflatex`. Switch to **XeLaTeX**.

**Citations show up as `[?]`**
You forgot to run `biber main` (or your editor is configured to run `bibtex` instead of
`biber`). Run the full sequence: `xelatex → biber → xelatex → xelatex`.

**Acronym list is empty**
Run `makeglossaries main` between the first and last `xelatex` runs, or let your editor's
build recipe handle it (Overleaf does this automatically).

**Cross-references show `??`**
Not all `.aux` files have been generated yet. Compile **at least twice** after a change to
labels or section numbering.

**Overleaf compilation timeout**
The `glossaries` package can be slow. Consider reducing the size of figures or splitting
long chapters into separate files while drafting.

---

## License

This template is released under the **[MIT License](LICENSE)**.

You are free to **use, copy, modify, merge, publish, distribute, sublicense, and/or sell**
copies of the template, for both personal and commercial purposes, provided that the
original copyright notice and the license text are included in any substantial portion of
the work. There are **no obligations** to share modifications, mention the original author
inside your thesis, or use a particular workflow.

In short: it's a template — take it, adapt it, and write your thesis.

> Note: the MIT License covers only the template files (LaTeX sources, README, LICENSE).
> The text *you* write in your thesis is yours, and any third-party assets you add
> (figures, datasets, fonts, citations) are governed by their own licenses.

---

## Acknowledgments

This template was created by **Lampros Konstantellos** in 2024, a graduate of the
**Department of Electrical and Computer Engineering, University of Patras**.

It follows the official departmental guidelines and best practices for thesis writing,
and incorporates contributions and feedback from students and faculty of the department.

Contributions, fixes, and improvements via pull requests or issues are welcome.

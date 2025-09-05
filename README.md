# Diploma Thesis Template (equivalent to Master’s Thesis) – University of Patras (ECE)

This repository contains a **LaTeX template** for preparing a Diploma Thesis (equivalent to a Master’s Thesis) at the  
**Department of Electrical and Computer Engineering, University of Patras**.  

It is fully compatible with any LaTeX editor, but you **must use the XeLaTeX compiler** to support Greek and English text properly.

---

## Repository Structure

```
├── main.tex              # Main thesis file (compile this one with XeLaTeX)
├── thesis.bib            # Bibliography file (BibTeX)
├── cover.pdf             # Cover page template (Greek & English)
├── figure.jpg            # Example figure
│
├── abstract-eng.tex      # English abstract
├── abstract-gr.tex       # Greek abstract
├── acknowledgements.tex  # Acknowledgments
├── introduction.tex      # Example chapter (Introduction)
│
└── README.md             # This file
```

You can extend this by creating more chapter `.tex` files (e.g., `chapter2.tex`, `results.tex`) and including them in `main.tex`.

---

## How to Compile

### 1. Requirements
- A full TeX distribution (e.g., [TeX Live](https://www.tug.org/texlive/) or [MiKTeX](https://miktex.org/))  
- Editor of your choice: TeXstudio, Overleaf, VS Code + LaTeX Workshop, etc.  

### 2. Compilation steps
Always compile with **XeLaTeX**. From terminal:

```bash
xelatex main.tex
biber main
xelatex main.tex
xelatex main.tex
```

(or set your editor to use **XeLaTeX** + **Biber**).

---

## Features
- Predefined **cover page** in both Greek and English  
- Templates for:
  - Greek & English abstracts
  - Acknowledgments
  - Chapters & appendices
  - References (BibTeX)
- Sample figure (`figure.jpg`) for demonstration  
- Follows department guidelines for formatting  

---

## Usage
1. Replace placeholders in `cover.pdf` (title, name, supervisor, year).  
2. Write your thesis content in the provided `.tex` files or add new chapters.  
3. Insert your references in `thesis.bib`.  
4. Add figures in the repository (e.g., `images/` directory) and include them with `\includegraphics`.  

---

## License
This template is provided under the **MIT License**.  
You may freely use, adapt, and share it.

---

## Acknowledgments
This template was created by **Lampros Konstantellos** in 2024, who is now a graduate of the  
**Department of Electrical and Computer Engineering, University of Patras**.  

It follows the official departmental guidelines and best practices for thesis writing.  
It is also based on contributions from students and faculty of the department.

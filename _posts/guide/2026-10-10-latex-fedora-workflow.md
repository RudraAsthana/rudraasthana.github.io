---
layout: default
title: "Minimalist LaTeX Typesetting on Fedora Workstation"
category: guide
---

# Minimalist LaTeX Typesetting on Fedora Workstation

This is a quick reference manual for setting up a clean, distraction-free LaTeX environment on Fedora. Heavy IDEs are unnecessary when you can achieve perfect typesetting with a minimal terminal workflow.

### 1. Installation

Grab the core packages using `dnf`. You do not need the full TeX Live distribution (which is massive) if you only want the essentials.

```bash
sudo dnf install texlive-scheme-basic texlive-collection-latex texlive-collection-fontsrecommended
```

### 2. Standard Preamble

I use this preamble for almost all my study manuals and procedural frameworks. It implements the TeX Gyre Bonum font and utilizes `parskip` for cleaner paragraph spacing without automatic indentation.

```latex
\documentclass[11pt, a4paper]{article}
\usepackage{geometry}
\geometry{margin=1in}
\usepackage{parskip}
\usepackage{enumitem}
\usepackage{tgbonum} % TeX Gyre Bonum font

\begin{document}
% Your content here
\end{document}
```

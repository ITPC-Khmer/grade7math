# Grade 7 LaTeX Document (Khmer-ready)

This project is set up to typeset Khmer text (e.g., the title) using XeLaTeX and fontspec/polyglossia.

Checklist
- Engine: XeLaTeX (not pdfLaTeX)
- Khmer font: Google Battambang (preferred) or fallbacks
- Preamble: fontspec + polyglossia with Khmer support

How to build (macOS, zsh)
1) Ensure XeLaTeX is installed (from MacTeX / TeX Live):
```
xelatex --version
```
If not installed, download MacTeX from https://tug.org/mactex/

2) Install a Khmer font
- Preferred: Google Battambang
  - Download from https://fonts.google.com/specimen/Battambang and install (double-click the .ttf to add via Font Book), OR
  - Using Homebrew (if available):
```
brew tap homebrew/cask-fonts
brew install --cask font-battambang
```
- Fallbacks (any of these also work): Noto Sans Khmer, Khmer MN, Khmer Sangam MN, FreeSerif.
For Noto Sans Khmer via Homebrew:
```
brew tap homebrew/cask-fonts
brew install --cask font-noto-sans-khmer
```

3) Compile with latexmk (recommended):
```
latexmk src/main.tex
```
This repo includes a `.latexmkrc` that defaults to XeLaTeX.

Or compile directly with XeLaTeX:
```
xelatex -interaction=nonstopmode -synctex=1 -output-directory=src src/main.tex
```
Run XeLaTeX twice if cross-references are added later.

Notes about Google Fonts
- The HTML `<link>` tags for Google Fonts do not affect LaTeX. LaTeX loads fonts installed on your system.
- We configured the document to use Battambang if the font is installed locally; otherwise it falls back to other Khmer fonts.

Troubleshooting
- Error: `\msg_fatal:nn {fontspec} {cannot-use-pdftex}`
  - Cause: Compiling with pdfLaTeX. Solution: Use XeLaTeX (see commands above) or run `latexmk` provided here.
- Khmer text shows as squares (tofu):
  - Install a Khmer font (Battambang or Noto Sans Khmer), then recompile.
- Editor still uses pdfLaTeX:
  - The file `src/main.tex` contains `% !TEX program = xelatex` to hint supported editors. Ensure your editor respects this, or select XeLaTeX manually.


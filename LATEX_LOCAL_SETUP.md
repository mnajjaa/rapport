# How We Got Overleaf-Style LaTeX Working Locally in VS Code

No more uploading files to Overleaf. Everything compiles locally, live preview updates on save, and it all runs inside VS Code just like an IDE.

---

## What You Need to Install

### 1. MiKTeX (the LaTeX compiler)
- Download from: https://miktex.org/download
- Choose the Windows installer
- During install, set **"Install missing packages on-the-fly"** to `Yes`
- This is the engine that actually compiles your `.tex` files into PDF

### 2. VS Code
- Download from: https://code.visualstudio.com
- You probably already have this

### 3. LaTeX Workshop (VS Code Extension)
- Open VS Code → Extensions (Ctrl+Shift+X)
- Search for **LaTeX Workshop** by James Yu
- Install it
- This extension gives you:
  - Auto-compile on save
  - Live PDF preview inside VS Code
  - Error highlighting
  - Syntax highlighting and autocomplete

### 4. ChkTeX (optional — linter)
- Comes bundled with most MiKTeX installs
- Gives you red/yellow squiggles in VS Code for LaTeX style warnings
- You can suppress specific warnings per-file with `% chktex-file 44` at the top

---

## Project Structure

Your project folder should look like this:

```
your-project/
├── main.tex              ← entry point, \include all chapters here
├── packages.tex          ← all \usepackage{} calls go here
├── config.tex            ← custom settings
├── title.tex             ← title page
├── references.bib        ← bibliography entries
└── chapters/
    ├── introduction.tex
    ├── chapter1.tex
    ├── chapter2.tex
    └── chapter3.tex
```

Keep `\usepackage{}` calls out of individual chapter files — put them all in `packages.tex` and `\include{packages}` at the top of `main.tex`.

---

## How to Compile

### Auto-compile (recommended)
LaTeX Workshop compiles automatically every time you save a `.tex` file.
Just hit **Ctrl+S** and the PDF updates in a few seconds.

### Manual compile
- Press **Ctrl+Alt+B** to build manually
- Or click the green play button at the top right of VS Code

### View the PDF
- Press **Ctrl+Alt+V** to open the live PDF preview in a side panel
- The preview updates automatically after each compile
- You can also click any word in the PDF and it jumps to that line in the source (SyncTeX)

---

## How LaTeX Workshop Knows What to Compile

LaTeX Workshop looks for a `main.tex` file automatically. If your entry point has a different name, add this to the top of that file:

```tex
% !TEX root = main.tex
```

Or set it in VS Code settings (`latex-workshop.latex.rootFile.useSubFileAsRoot`).

---

## Handling Missing Packages

When MiKTeX encounters a package it doesn't have, it pops up a dialog asking to install it. Click **Install** and it downloads automatically from CTAN. This only happens once per package.

If you don't see the dialog, open **MiKTeX Console** from the Start menu and check for updates.

---

## Common Issues and Fixes

| Problem | Fix |
|---------|-----|
| PDF doesn't update after save | Check the Output panel (Ctrl+Shift+U → LaTeX Workshop) for errors |
| `\headheight too small` warning | Add `\setlength{\headheight}{14.5pt}` to your packages file |
| `Package X not found` | MiKTeX installs it automatically on next compile |
| chktex red squiggles you don't care about | Add `% chktex-file 44` at the top of the file |
| Overfull `\hbox` warnings | Your content is wider than the column — widen the column with `p{1.3cm}` instead of `p{0.5cm}` |
| PDF preview blank | Close and reopen with Ctrl+Alt+V |

---

## The Workflow (day to day)

1. Open the project folder in VS Code
2. Open `main.tex` or any chapter file
3. Edit your content
4. Hit **Ctrl+S**
5. Watch the PDF update in the side panel in 3-5 seconds
6. Click anywhere in the PDF to jump to that line in the source

That's it. Same experience as Overleaf, fully offline, no file size limits, no upload/download, and version-controlled with Git.

---

## Why Local Instead of Overleaf?

| | Overleaf | Local (VS Code + MiKTeX) |
|--|----------|--------------------------|
| Works offline | No | Yes |
| File size limit | Yes (free tier) | No |
| Compile speed | Slow on free tier | Fast |
| Git integration | Paid only | Native |
| Your own AI assistant | No | Yes (Claude Code in VS Code) |
| Cost | Free / paid | Free |

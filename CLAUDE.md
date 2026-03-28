# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Build

Compile the CV to PDF using XeLaTeX:
```bash
xelatex cv.tex
```
Or with latexmk (recommended):
```bash
latexmk -xelatex cv.tex
```
Output is `cv.pdf` (gitignored). PDFs are only distributed via GitHub Releases as `CV_Orzes_Matteo.pdf`.

## Architecture

LaTeX CV using the [Awesome CV](https://github.com/posquit0/Awesome-CV) template with XeLaTeX for custom font support.

- `cv.tex` — Main document: personal info, layout config, imports sections in order
- `awesome-cv.cls` — Template class file (do not modify unless changing the template itself)
- `cv/` — Content sections (`education.tex`, `skills.tex`, `experience.tex`), imported by `cv.tex` via `\input{}`
- `fonts/` — Roboto family + FontAwesome, referenced via `\fontdir[fonts/]`

**To edit CV content**, modify files in `cv/`. To change personal info or section order, edit `cv.tex`.

## Key LaTeX Commands

```latex
\cventry{position}{organization}{location}{dates}{description}  % Experience/education entries
\cvskill{category}{skills list}                                  % Skills entries
\cvsection{Title}                                                % Section headers
\begin{cvitems}...\end{cvitems}                                  % Bullet lists inside cventry
```

## Release Workflow — Critical Details

**The `version` file is tightly coupled to CI.** Every PR to master must bump it. Format: `X.Y.Z` (no `v` prefix — workflows add it).

Three workflows exist:
1. **FeaturePush.yml** — Any non-master push: compile-only validation
2. **MergeRequest.yml** — PR to master: validates version format, checks tag uniqueness, builds PDF, creates+deletes a temporary draft release as a smoke test
3. **CreateReleaseAfterMerge.yml** — Push to master: creates git tag `vX.Y.Z`, compiles PDF, publishes GitHub Release with `CV_Orzes_Matteo.pdf` attached

**If the version tag already exists, both PR and release workflows will fail.** Always increment the version when making changes.

All GitHub Actions are pinned to full commit SHAs (not version tags) for security. Renovate auto-merges minor/patch action updates weekly (Monday before 5am CET).

# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is a LaTeX-based curriculum vitae (CV) repository using the Awesome CV template. The repository uses GitHub Actions for automated CV compilation and release management.

## Building the CV

### Compile to PDF
The CV uses XeLaTeX for compilation. To build:
```bash
xelatex cv.tex
```

Or use `latexmk` with XeLaTeX:
```bash
latexmk -xelatex cv.tex
```

The build process generates `cv.pdf` as the output (though .pdf files are gitignored).

## Document Structure

### Main Document
- `cv.tex` - Main document that includes all sections and defines personal information
- `awesome-cv.cls` - Custom LaTeX class file defining all styles, commands, and layouts

### Content Sections (in `cv/` directory)
- `cv/education.tex` - Education section
- `cv/skills.tex` - Skills section
- `cv/experience.tex` - Professional experience section

To modify CV content, edit these section files. The main `cv.tex` file imports them in order using `\input{cv/filename.tex}`.

## Personal Information

Personal details are defined in `cv.tex` using these commands:
- `\name{Firstname}{Lastname}`
- `\position{Job Title}`
- `\mobile{Phone}`
- `\email{Email}`
- `\linkedin{username}`
- `\photo{./profile.png}`
- `\quote{Quote text}`

## CV Structure Commands

The Awesome CV class provides these main commands:

**Sections:**
- `\cvsection{Title}` - Major section header

**Experience entries:**
- `\cventry{position}{organization}{location}{dates}{description}`
- Use `\begin{cvitems}...\end{cvitems}` within description for bulleted lists

**Skills:**
- `\cvskill{category}{skills list}`

**Education:**
- Same as `\cventry` but typically simpler

## GitHub Actions Workflows

### Versioning
The repository uses semantic versioning stored in the `version` file at the root. This must follow the format `X.Y.Z` (e.g., `1.0.0`).

### Workflow Triggers

**FeaturePush.yml** - Runs on all branches except master:
- Builds the LaTeX document to verify compilation

**MergeRequest.yml** - Runs on pull requests to master:
- Validates version tag format (must be `X.Y.Z`)
- Checks that the version tag doesn't already exist
- Builds the CV and creates `CV_Orzes_Matteo.pdf`
- Creates a temporary draft release for testing
- Cleans up the test tag and release

**CreateReleaseAfterMerge.yml** - Runs on pushes to master:
- Validates and creates the version tag
- Compiles the CV to `CV_Orzes_Matteo.pdf`
- Creates a GitHub release with the compiled PDF

## Updating the CV

To add a new version:
1. Edit the relevant `.tex` files in `cv/` directory
2. Update the `version` file with the new version number
3. Commit changes to a feature branch
4. Create a pull request to master - this will validate the build
5. After merge to master, a release is automatically created with the compiled PDF

## Fonts

Custom fonts are in the `fonts/` directory:
- Roboto family (Regular, Bold, Italic, Light, Medium, Thin variants)
- FontAwesome for icons

The document uses XeLaTeX to support these custom fonts.

## Color Scheme

Available color themes defined in the class file:
- awesome-emerald
- awesome-skyblue
- awesome-red (currently selected)
- awesome-pink
- awesome-orange
- awesome-nephritis
- awesome-concrete
- awesome-darknight

Change the color in `cv.tex`:
```latex
\colorlet{awesome}{awesome-red}
```
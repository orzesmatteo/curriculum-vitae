# Curriculum Vitae

A professional CV built with LaTeX using the [Awesome CV](https://github.com/posquit0/Awesome-CV) template.

## Overview

This repository contains my curriculum vitae with automated building and release management via GitHub Actions. The CV is written in LaTeX and compiled to PDF automatically when changes are merged.

## Building Locally

### Prerequisites

You need a LaTeX distribution with XeLaTeX support:

- **Linux**: Install TeX Live
  ```bash
  sudo apt-get install texlive-xetex texlive-fonts-extra
  ```

- **macOS**: Install MacTeX
  ```bash
  brew install --cask mactex
  ```

- **Windows**: Install MiKTeX or TeX Live
  - [MiKTeX](https://miktex.org/download)
  - [TeX Live](https://www.tug.org/texlive/windows.html)

### Compiling the CV

Using XeLaTeX directly:
```bash
xelatex cv.tex
```

Using latexmk (recommended):
```bash
latexmk -xelatex cv.tex
```

The output will be `cv.pdf` in the same directory.

## Repository Structure

```
.
├── cv.tex                    # Main CV document
├── awesome-cv.cls            # LaTeX class file (template)
├── cv/
│   ├── education.tex         # Education section
│   ├── experience.tex        # Work experience section
│   └── skills.tex            # Skills section
├── fonts/                    # Custom fonts (Roboto, FontAwesome)
├── profile.png               # Profile photo
├── version                   # Semantic version number
└── .github/workflows/        # CI/CD workflows
```

## Modifying the CV

### Personal Information

Edit the header section in `cv.tex`:

```latex
\name{Firstname}{Lastname}
\position{Job Title}
\mobile{Phone Number}
\email{email@example.com}
\linkedin{linkedin-username}
\photo{./profile.png}
```

### Content Sections

Modify the content files in the `cv/` directory:

- **cv/experience.tex** - Work experience entries
- **cv/education.tex** - Educational background
- **cv/skills.tex** - Technical and soft skills

Use the provided LaTeX commands:

```latex
\cventry{position}{organization}{location}{dates}{description}
\cvskill{category}{skills list}
```

### Customization

Change the color scheme in `cv.tex`:

```latex
\colorlet{awesome}{awesome-red}
```

Available colors: `awesome-emerald`, `awesome-skyblue`, `awesome-red`, `awesome-pink`, `awesome-orange`, `awesome-nephritis`, `awesome-concrete`, `awesome-darknight`

## Automated Workflows

This repository uses GitHub Actions for automated building and releases:

### Feature Branches
When you push to any branch except `master`, the workflow validates that the CV compiles successfully.

### Pull Requests
When you create a PR to `master`:
- Validates the version format in the `version` file
- Checks that the version tag doesn't already exist
- Builds the CV and creates a temporary draft release
- Cleans up the test artifacts

### Master Branch
When changes are merged to `master`:
- Validates and creates a version tag (e.g., `v1.0.0`)
- Compiles the CV to `CV_Orzes_Matteo.pdf`
- Creates a GitHub Release with the PDF attached
- The PDF is available for download from the Releases page

## Updating and Releasing

To create a new version:

1. Create a feature branch:
   ```bash
   git checkout -b update-cv
   ```

2. Make your changes to the `.tex` files in `cv/`

3. Update the version number in the `version` file:
   ```
   1.1.0
   ```
   Follow [semantic versioning](https://semver.org/): `MAJOR.MINOR.PATCH`

4. Commit and push your changes:
   ```bash
   git add .
   git commit -m "Update CV with new experience"
   git push origin update-cv
   ```

5. Create a pull request to `master`

6. After the PR is approved and merged, a new release is automatically created

## License

The Awesome CV LaTeX template is licensed under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).

## Credits

- **Template**: [Awesome CV](https://github.com/posquit0/Awesome-CV) by Claud D. Park
- **Fonts**: Roboto and FontAwesome

## Troubleshooting

### Compilation Errors

**Missing fonts**: Ensure you have the fonts in the `fonts/` directory and XeLaTeX is properly installed.

**Package errors**: Update your LaTeX distribution:
- TeX Live: `sudo tlmgr update --all`
- MiKTeX: Use the MiKTeX Console to update packages

**Profile image errors**: Ensure `profile.png` exists in the root directory.

### GitHub Actions Failures

**Version tag already exists**: Update the `version` file with a new, unique version number.

**Build fails**: Check the Actions tab for detailed error logs. Common issues:
- LaTeX syntax errors in `.tex` files
- Missing required packages
- Malformed YAML in workflow files

## Support

For issues related to:
- **Template**: See the [Awesome CV repository](https://github.com/posquit0/Awesome-CV)
- **This repository**: Open an issue in this repository

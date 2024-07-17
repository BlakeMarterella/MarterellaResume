# Blake Marterella Latex Resume

## Overview

After 4+ years of fine-tuning and tailoring my resume in Google Docs, it was time to make the leap and create my first LaTeX resume. Having a single source of truth for my resume that can be easily updated and version-controlled was the main motivation for this project. I also wanted to further my understanding of LaTeX and have total control over the styling.

### Benefits of a LaTex Resume

- **Version Control**: Easily track changes to your resume over time with git, especially by use of different branches and tools like `latexdiff`.
- **Consistency**: Ensure that your resume is consistent across all platforms and devices.
- **Customization**: Have total control over the styling and layout of your resume.
- **Flexibility**: Easily create multiple versions of your resume for different job applications.

## Getting Started

Prior to this project, my LaTeX knowledge didn't extended far beyond the few research papers I had created with this technology. To give myself a starting point, I decided to use a Resume Template that I found on Overleaf, [link to orginial resume template created by Andrew C.](https://www.overleaf.com/latex/templates/andrewresumeworkshop/yrpwhsjdypmw). You can choose to modify the template using the Overleaf's online editor but I decided to export the `.tex` file and import it into my Github repository. See the section below for information on how I used VSCode with some nifty extensions to craft my ideal resume.

### Development Tools

To make changes and alter my resume, I use [VSCode](https://code.visualstudio.com/) with the [LaTeX Workshop](https://marketplace.visualstudio.com/items?itemName=James-Yu.latex-workshop) and [Grammarly](https://github.com/znck/grammarly) extension. This extension allows me to compile my resume and preview it in realtime.

If you want to avoid installing LaTeX on your machine, you can use an online editor like [Overleaf](https://www.overleaf.com/). Overleaf is a cloud-based LaTeX editor that allows you to create, edit, and share your LaTeX documents but you do miss the git shenanigans.

#### Latex Workshop Configuration

The default configuration for the LaTeX Workshop extension in VSCode is to output the compiled PDF and build files (`.aux`, `.log`, `.out`, `.synctex.gz`) to the same directory as the `.tex` file. I wanted to change this so that these files would be output to a separate directory, leaving only the `.tex` in the root of the repository. To do this, I added the following configuration to my `settings.json` file:

```json
"latex-workshop.latex.outDir": "ouput",
"latex-workshop.latex.tools": [
    {
        "name": "latexmk",
        "command": "latexmk",
        "args": [
            "-synctex=1",
            "-interaction=nonstopmode",
            "-file-line-error",
            "-pdf",
            "-outdir=%OUTDIR%",
            "%DOC%"
        ],
        "env": {}
    },
    {
        "name": "pdflatex",
        "command": "pdflatex",
        "args": [
            "-synctex=1",
            "-interaction=nonstopmode",
            "-file-line-error",
            "-output-directory=%OUTDIR%",
            "%DOC%"
        ],
        "env": {}
    },
    {
        "name": "bibtex",
        "command": "bibtex",
        "args": [
            "%OUTDIR%/%DOCFILE%"
        ],
        "env": {}
    }
]
```

*Note:* I work on a Mac, these settings may be different on Windows or Linux machines. In the background, the LatexWorkshop extension uses `pdflatex` and other tools to compile the `.tex` file into a `.pdf` file, you can fine more information on the [pdflatex man page](https://linux.die.net/man/1/pdflatex).

##  Using LaTeX Commands

The template that I found already had a good foundation but it was missing a couple sections specific to my resume. I needed a way to elegantly and uniformly display my certifications on a single line with proper spacing. For that reson, I created the command called `resumeCertification` which takes in 3 parameters, the certification name, issuing organization, and date, applies some text formatting, and adjusts the spacing.

```
\newcommand{\resumeCertification}[3]{
    \item
    \begin{tabular*}{0.97\textwidth}{l@{\extracolsep{\fill}}r}
      {\small \textbf{#1}, {#2}} & \textit{\small #3} \\
    \end{tabular*}\vspace{-7pt}
}
```

I can now use this command multiple times, anywhere in my `tex` file:

```
\resumeCertification {AWS Cloud Practitioner}{Amazon Web Services}{January 2022}
```

The end result looks something like this:

<image>

## Future Development

Eventually, I would like to be able to break my resume into individual sections and import them into the main `.tex` file. The compilations and lift required to do this are a bit more than I am willing to take on at the moment but [this Github boilerplate project](https://github.com/ethwu/multidoc/blob/main/README.md) is a good starting point for anyone willing to take on the task.

## Resources

- [Why I write my resume in Latex - Logan Marchione](https://www.loganmarchione.com/2019/03/why-i-write-my-resume-in-latex/)
- [Designing latex resumes for maximum impact, a complete guide - The Latexum Team](https://latexum.com/designing-latex-resumes-for-maximum-impact-a-complete-guide/)
- [Git Latex Workflow - StackOverflow](https://stackoverflow.com/questions/6188780/git-latex-workflow)
- [Latexdiff](https://www.ctan.org/tex-archive/support/latexdiff/)
- [How to configure the output directory for latex workshop in VSCode](https://github.com/James-Yu/LaTeX-Workshop/issues/548)
- [Latex Template for a Resume - Andrew C](https://www.overleaf.com/latex/templates/andrewresumeworkshop/yrpwhsjdypmw)
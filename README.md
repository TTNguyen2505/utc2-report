# Academic Report & Thesis LaTeX Template (UTC2)

[![LaTeX Engine: XeLaTeX](https://img.shields.io/badge/Engine-XeLaTeX-blue.svg)](https://tug.org/xetex/)
[![TeX Distribution: MiKTeX](https://img.shields.io/badge/TeX-MiKTeX%2024%2B-teal.svg)](https://miktex.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![GitHub Repository](https://img.shields.io/badge/GitHub-utc2--report-181717.svg?logo=github)](https://github.com/TTNguyen2505/utc2-report)
[![Author: TTNguyen2505](https://img.shields.io/badge/Author-TTNguyen2505-blue.svg)](https://github.com/TTNguyen2505)

A professional, modular, and standardized **XeLaTeX template** designed for academic assignments, course projects, and graduation theses according to Vietnamese higher education and MoET formatting specifications. Converted and refined from standard institutional Microsoft Word guidelines into a clean, reproducible, and automated LaTeX project.

The template strictly adheres to the official formatting standards of the **Faculty of Information Technology, University of Transport and Communications, Campus in Ho Chi Minh City (UTC2)**.

---

## Getting Started

### Clone the Repository

Clone the project repository to your local workstation using Git, then change into the project directory:

```bash
git clone https://github.com/TTNguyen2505/utc2-report.git
cd utc2-report
```

---

## Prerequisites & System Requirements (Windows)

### 1. TeX Distribution: MiKTeX
This template relies on the **XeLaTeX** engine and standard CTAN packages. Download and install **MiKTeX for Windows** from [miktex.org](https://miktex.org/download).

> [!IMPORTANT]
> **Enable Automatic Package Installation On-the-Fly:**
> 1. Open **MiKTeX Console** from the Start Menu.
> 2. Switch to **Administrator** or **User** mode (depending on your installation).
> 3. Navigate to **Settings** $\rightarrow$ **General**.
> 4. Under **"You can choose whether missing packages are to be installed automatically"**, select **"Always install missing packages on-the-fly"** (or **"Yes"**).
> 5. Click **Apply**. This allows MiKTeX to automatically fetch required font and macro packages upon first build without manual intervention.

### 2. Perl Environment: Strawberry Perl
Perl is required by LaTeX automation tools, bibliography compilation helpers, and `latexmk`.
- Download and install **Strawberry Perl** (64-bit) from [strawberryperl.com](https://strawberryperl.com/).
- Ensure `C:\Strawberry\perl\bin` is added to your system `PATH` (handled automatically by the installer).

### 3. Verify CLI Environment
Open PowerShell or Command Prompt and verify that all necessary command-line tools are available:

```powershell
# Verify XeTeX / XeLaTeX engine
xelatex --version

# Verify BibTeX bibliography processor
bibtex --version

# Verify Perl interpreter
perl --version
```

---

## Build via CLI

### Official Full Build Pipeline

To ensure all cross-references, citations, Table of Contents, and float lists are completely synchronized, execute the full 4-stage build sequence:

#### PowerShell (Recommended)
```powershell
xelatex -interaction=nonstopmode main.tex; bibtex main; xelatex -interaction=nonstopmode main.tex; xelatex -interaction=nonstopmode main.tex
```

#### Windows Command Prompt (CMD)
```cmd
xelatex -interaction=nonstopmode main.tex && bibtex main && xelatex -interaction=nonstopmode main.tex && xelatex -interaction=nonstopmode main.tex
```

> [!TIP]
> **Avoid PDF File Locking on Windows:**
> Adobe Acrobat Reader locks open PDF files with exclusive access, causing `dvipdfmx: fatal: Unable to open "main.pdf"`.
> Use **SumatraPDF**, web browsers (Microsoft Edge / Google Chrome), or the **VS Code PDF Viewer** extension when developing; these tools automatically reload the document without file locking.

---

### Clean Up Auxiliary Files

LaTeX generates several auxiliary files during compilation. To clean up intermediate cache files and keep only source files and the final `main.pdf`:

#### PowerShell
```powershell
Remove-Item -Force -ErrorAction SilentlyContinue main.aux, main.bbl, main.blg, main.lof, main.log, main.lol, main.lot, main.out, main.toc, main.synctex.gz, "main.synctex(busy)"
```

#### Windows Command Prompt (CMD)
```cmd
del /f /q main.aux main.bbl main.blg main.lof main.log main.lol main.lot main.out main.toc main.synctex.gz "main.synctex(busy)" 2>nul
```

---

## Project Directory Structure

```text
.
├── .gitignore                      # Git ignore rules for LaTeX auxiliary files
├── LICENSE                         # MIT open-source license
├── README.md                       # Project documentation and user guide
├── main.tex                        # Master document assembling all components
│
├── assets/                         # Graphic, diagram, and external data assets
│   ├── figures/                    # Vector and raster graphics
│   │   ├── ch01/                   # Figures for Chapter 1
│   │   │   └── example_figure.pdf  # Sample vector PDF diagram
│   │   ├── ch03/                   # Figures for Chapter 3
│   │   └── ch04/                   # Figures for Chapter 4
│   ├── logos/                      # Institutional logos and emblems
│   │   └── university_logo.pdf     # Primary university logo (UTC2)
│   └── tables/                     # Modular data tables and external components
│       ├── ch01/                   # Tables for Chapter 1
│       │   └── example_table.tex   # Sample modular external table file
│       └── ch02/                   # Tables for Chapter 2
│
├── backmatter/                     # End matter sections
│   ├── references.bib              # BibTeX literature citations (IEEE format)
│   └── appendices/                 # Appendix chapters
│       ├── appendix_a_source_code.tex  # Appendix A: Source code & scripts
│       └── appendix_b_survey_data.tex  # Appendix B: Experimental & survey data
│
├── chapters/                       # Main content chapters
│   ├── 01_introduction.tex         # Chapter 1: Headings, lists, floats & listings
│   ├── 02_literature_review.tex    # Chapter 2: Theoretical basis, inline & display math
│   ├── 03_system_architecture.tex  # Chapter 3: System architecture & models
│   ├── 04_implementation.tex       # Chapter 4: Implementation & testing
│   └── 05_conclusion.tex           # Chapter 5: Conclusion & future work
│
├── config/                         # Configuration and typography macros
│   ├── abbreviations.tex           # Three-column abbreviations table
│   ├── format.sty                  # Document layout, captions, headings & TOC styles
│   ├── metadata.tex                # Project dynamic variables and author definitions
│   └── packages.sty                # Core CTAN package dependencies
│
└── frontmatter/                    # Front matter sections
    ├── 00_cover.tex                # Main outer cover with 3pt institutional border
    ├── 00_subcover.tex             # Inside sub-cover with formal double border
    ├── 01_lecturer_review.tex      # Instructor assessment sheet (unpaginated)
    ├── 02_task_assignment.tex      # Student task distribution table
    ├── 03_affirmation.tex          # Academic integrity commitment (page i)
    ├── 04_acknowledgments.tex      # Acknowledgments statement (page ii)
    └── 05_lists.tex                # Table of Contents, Figures, Tables & Listings
```

---

## Customization Guide

### 1. Setting Up Project Metadata
Edit `config/metadata.tex` to configure your project details:

```latex
\university{TRƯỜNG ĐẠI HỌC GIAO THÔNG VẬN TẢI \n PHÂN HIỆU TẠI TP. HỒ CHÍ MINH}
\faculty{Bộ môn Công nghệ thông tin}
\institutionlogo{assets/logos/university_logo.pdf}

\subject{Tên môn học}
\reporttitle{Báo cáo bài tập lớn}
\subtitle{Tên đề tài nghiên cứu}

\supervisor{ThS. Trần Văn A}
\submissiondate{TP. Hồ Chí Minh, Ngày 10 Tháng 10 Năm 2026}
\studentclass{Mã lớp quản lý (Ví dụ: CQ.66.CNTT)}
\cohort{Khoá nhập học (Ví dụ: K66)}
```

### 2. Adding Authors Dynamically
Authors are registered using the `\addauthor` command in `config/metadata.tex`:

```latex
% Syntax: \addauthor{Index}{Full Name}{Student ID}{Assigned Task}{Contribution%}
\addauthor{1}{Nguyễn Văn B}{65510200XX}{Nhiệm vụ 1}{20\%}
\addauthor{2}{Nguyễn Văn C}{66510710XX}{Nhiệm vụ 2}{30\%}
\addauthor{3}{Nguyễn Văn D}{66510710XX}{Nhiệm vụ 3}{25\%}
\addauthor{4}{Nguyễn Văn E}{66510710XX}{Nhiệm vụ 4}{15\%}
\addauthor{5}{Nguyễn Văn F}{66510710XX}{Nhiệm vụ 5}{10\%}
```

All author information is automatically reflected across:
- **Main Cover Page** (`frontmatter/00_cover.tex`)
- **Inside Sub-Cover Page** (`frontmatter/00_subcover.tex`)
- **Academic Affirmation** (`frontmatter/03_affirmation.tex`)
- **Task Assignment Board** (`frontmatter/02_task_assignment.tex`)

---

## License & Credits

### License
This project is open-source and released under the [MIT License](LICENSE). You are free to use, modify, and distribute this template for academic and personal projects.

### Credits & Author
- **Author:** Trần Trọng Nguyên
- **GitHub:** [@TTNguyen2505](https://github.com/TTNguyen2505)
- **Repository:** [https://github.com/TTNguyen2505/utc2-report](https://github.com/TTNguyen2505/utc2-report)
- **Email:** [trantrongnguyen2505@outlook.com](mailto:trantrongnguyen2505@outlook.com)

Contributions, feature suggestions, and bug reports are warmly welcome via GitHub Issues and Pull Requests!

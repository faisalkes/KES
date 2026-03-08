# PDF & Word (DOCX) Export Guide
## Converting Proposal Markdown Files to PDF and DOCX

**Proposal #:** PROP-2026-AVAYA-001  
**Date:** March 7, 2026

---

## Overview

All proposal documents in this repository are written in **Markdown (.md)** format for easy editing and version control. This guide explains how to export them to:

- **PDF** – For formal delivery to the customer.
- **Word (DOCX)** – For customer review, editing, or signature.
- **HTML** – For web browser viewing.

The recommended export tool is **[Pandoc](https://pandoc.org/)** – a free, open-source document converter.

---

## Method 1: Pandoc (Command Line – Recommended)

### 1.1 Installation

| Platform | Installation Command |
|----------|---------------------|
| Ubuntu / Debian | `sudo apt-get install pandoc texlive-xetex` |
| macOS (Homebrew) | `brew install pandoc` + `brew install --cask mactex` |
| Windows | Download installer from [pandoc.org/installing.html](https://pandoc.org/installing.html) |

> **Note:** For PDF output, Pandoc requires a LaTeX engine (e.g., `xelatex`). Install **TeX Live** (Linux/Mac) or **MiKTeX** (Windows) alongside Pandoc.

### 1.2 Convert Markdown to PDF

```bash
# Single file to PDF
pandoc proposal/Avaya_IPOffice_Proposal.md \
  -o output/Avaya_IPOffice_Proposal.pdf \
  --pdf-engine=xelatex \
  --variable geometry:margin=2.5cm \
  --variable fontsize=11pt \
  --variable mainfont="DejaVu Serif" \
  --variable monofont="DejaVu Sans Mono" \
  --toc \
  --toc-depth=3

# All proposal files to PDF (batch)
for f in proposal/*.md; do
  pandoc "$f" -o "output/$(basename "${f%.md}").pdf" \
    --pdf-engine=xelatex \
    --variable geometry:margin=2.5cm \
    --toc
done
```

### 1.3 Convert Markdown to Word (DOCX)

```bash
# Single file to DOCX
pandoc proposal/Avaya_IPOffice_Proposal.md \
  -o output/Avaya_IPOffice_Proposal.docx \
  --reference-doc=template/reference.docx

# Without custom template
pandoc proposal/Avaya_IPOffice_Proposal.md \
  -o output/Avaya_IPOffice_Proposal.docx

# All proposal files to DOCX (batch)
for f in proposal/*.md; do
  pandoc "$f" -o "output/$(basename "${f%.md}").docx"
done
```

### 1.4 Convert Markdown to HTML

```bash
# Self-contained HTML (embeds CSS)
pandoc proposal/Avaya_IPOffice_Proposal.md \
  -o output/Avaya_IPOffice_Proposal.html \
  --self-contained \
  --toc \
  --css=template/style.css
```

### 1.5 Merge All Proposal Files into One PDF

```bash
# Merge all proposal documents into a single professional PDF
pandoc \
  proposal/Avaya_IPOffice_Proposal.md \
  proposal/STC_SIP_Trunk_Configuration.md \
  proposal/BOM_Pricing_Detailed.md \
  proposal/Project_Timeline.md \
  proposal/Acceptance_Form.md \
  -o output/KES_Avaya_Proposal_PROP-2026-AVAYA-001_Complete.pdf \
  --pdf-engine=xelatex \
  --variable geometry:margin=2.5cm \
  --variable fontsize=11pt \
  --toc \
  --toc-depth=3 \
  --metadata title="Avaya IP Office Server Edition Proposal PROP-2026-AVAYA-001"
```

### 1.6 Custom DOCX Template

To apply a branded Word template (company colors, fonts, header/footer):

1. Create a reference DOCX: `pandoc -o template/reference.docx --print-default-data-file reference.docx`
2. Open `template/reference.docx` in Microsoft Word and customize styles.
3. Use `--reference-doc=template/reference.docx` in your pandoc commands.

---

## Method 2: Visual Studio Code (GUI)

### Required Extensions

- **Markdown Preview Enhanced** (Yiyi Wang) – Install from VS Code Extensions.
- **Markdown PDF** (yzane) – One-click PDF export.

### Steps

1. Open the `.md` file in VS Code.
2. Press `Ctrl+Shift+P` → Type `Markdown PDF: Export (pdf)`.
3. The PDF is saved in the same folder as the `.md` file.

> **Tip:** Markdown Preview Enhanced supports custom CSS and LaTeX math rendering for more professional output.

---

## Method 3: Typora (GUI – Windows/Mac/Linux)

[Typora](https://typora.io/) is a paid Markdown editor with excellent export capabilities.

### Steps

1. Open the `.md` file in Typora.
2. File → Export → **PDF** or **Word (.docx)** or **HTML**.
3. Choose page size (A4 recommended) and margins.

> Typora produces clean, professional PDF output without requiring LaTeX.

---

## Method 4: GitHub / GitLab (Online Preview)

GitHub renders Markdown files automatically when viewed in the browser.

- **View online:** Navigate to any `.md` file in the repository on GitHub.com.
- **Print to PDF:** Use browser `Ctrl+P` → Print → Save as PDF.
  - Recommended: Chrome or Edge browser for best table rendering.
  - Set margins to Narrow or Custom (10mm).

---

## Method 5: Microsoft Word (Manual)

1. Open the `.md` file in a text editor (Notepad++, VS Code).
2. Copy the content.
3. Paste into Microsoft Word and apply heading styles manually.
4. Export as PDF via File → Save As → PDF.

> This method is the least efficient but works without any additional tools.

---

## Recommended Workflow for Customer Delivery

```
1. Edit .md files in VS Code or any text editor
2. Run Pandoc to generate:
   a. PDF for formal customer copy
   b. DOCX for customer review/signature
3. Review PDF for formatting (especially tables and code blocks)
4. Add company letterhead/cover page in Word if needed
5. Password-protect PDF (optional): 
   Use Adobe Acrobat or qpdf:
   qpdf --encrypt <user-pass> <owner-pass> 128 -- input.pdf output-protected.pdf
```

---

## Pandoc Quick Reference

| Command | Description |
|---------|-------------|
| `pandoc input.md -o output.pdf` | Basic MD to PDF |
| `pandoc input.md -o output.docx` | Basic MD to DOCX |
| `pandoc input.md -o output.html` | Basic MD to HTML |
| `--pdf-engine=xelatex` | Use XeLaTeX for PDF (supports Unicode/Arabic) |
| `--toc` | Generate table of contents |
| `--toc-depth=3` | TOC depth (H1/H2/H3) |
| `--variable geometry:margin=2.5cm` | Page margins |
| `--reference-doc=template.docx` | Custom Word template |
| `--self-contained` | Embed images/CSS in HTML |
| `--metadata title="..."` | Set document title |

---

## Notes on Arabic Language Support

If the proposal needs to be translated to Arabic and exported to PDF:

1. Use `--pdf-engine=xelatex`.
2. Set `--variable mainfont="Arial"` or another Arabic-supporting font.
3. Install Arabic fonts: `sudo apt-get install fonts-arabeyes` (Ubuntu).
4. For right-to-left (RTL) text, use the `polyglossia` LaTeX package in a custom template.

---

*[YOUR COMPANY NAME] | PDF Export Guide | PROP-2026-AVAYA-001*

# Visio Export Instructions
## Exporting draw.io Diagrams to Visio (.vsdx), PDF, and PNG

**Proposal #:** PROP-2026-AVAYA-001  
**Date:** March 7, 2026

---

## Overview

The network diagrams in this repository are in **draw.io XML format** (`.drawio`). This guide explains how to export them to:

- **Visio (.vsdx)** – For Microsoft Visio users.
- **PDF** – For document-quality printing and sharing.
- **PNG / SVG** – For embedding in presentations and documents.

---

## Method 1: diagrams.net (draw.io) Web App

### Open Diagram

1. Go to [https://app.diagrams.net](https://app.diagrams.net) in your browser.
2. Click **Open Existing Diagram**.
3. Select the `.drawio` file from your local folder.

### Export to Visio (.vsdx)

1. With the diagram open, click **Extras** → **Edit Diagram** to verify it loaded correctly.
2. Click **File** → **Export As** → **VSDX (Visio)…**
3. Choose export settings:
   - **Page:** All Pages or Current Page
   - Click **Export**
4. Download the `.vsdx` file.

> **Note:** draw.io → Visio export preserves shapes and text. Complex custom shapes may render differently in Visio. Review after export.

### Export to PDF

1. Click **File** → **Export As** → **PDF…**
2. Settings:
   - **Page:** All Pages or Current Page
   - **Fit Page:** ✅ Enable
   - **Include background:** ✅ Enable
   - **Grid:** ❌ Disable (for clean output)
3. Click **Export** → Download PDF.

### Export to PNG

1. Click **File** → **Export As** → **PNG…**
2. Settings:
   - **Zoom:** 150% or 200% for high resolution
   - **Background:** White (recommended)
   - **Shadow:** Disable
   - **Fit Page:** Enable
3. Click **Export** → Download PNG.

### Export to SVG

1. Click **File** → **Export As** → **SVG…**
2. SVG is resolution-independent – ideal for presentations.
3. Click **Export** → Download SVG.

---

## Method 2: draw.io Desktop Application

### Installation

Download the free draw.io desktop app from:  
[https://github.com/jgraph/drawio-desktop/releases](https://github.com/jgraph/drawio-desktop/releases)

Available for Windows, macOS, and Linux.

### Open and Export

1. Launch draw.io desktop app.
2. **File** → **Open** → Select `.drawio` file.
3. Use **File** → **Export As** → same options as web app:
   - **VSDX** – Visio format
   - **PDF** – PDF document
   - **PNG** – Raster image
   - **SVG** – Vector image

---

## Method 3: Command Line Export (draw.io CLI)

For automated / batch export, use the draw.io command-line interface:

### Installation (Linux/macOS)

```bash
# Install via npm
npm install -g drawio-exporter

# OR use draw.io desktop CLI directly
# On macOS:
/Applications/draw.io.app/Contents/MacOS/draw.io --help

# On Linux (AppImage):
./drawio-x86_64.AppImage --help
```

### Batch Export to PDF

```bash
# Export single file to PDF
/path/to/drawio --export --format pdf --output output/ diagrams/Network_Architecture.drawio

# Export all .drawio files to PDF
for f in diagrams/*.drawio; do
  /path/to/drawio --export --format pdf --output output/ "$f"
done
```

### Batch Export to PNG

```bash
# Export to PNG (300 DPI for print quality)
/path/to/drawio --export --format png --scale 2 --output output/ diagrams/Network_Architecture.drawio

# All files
for f in diagrams/*.drawio; do
  /path/to/drawio --export --format png --scale 2 --output output/ "$f"
done
```

### Batch Export to Visio

```bash
# Export to VSDX
/path/to/drawio --export --format vsdx --output output/ diagrams/Network_Architecture.drawio
```

---

## Method 4: Microsoft Visio (Direct Import)

### Open draw.io XML in Visio

> **Visio 2019 / Microsoft 365 Visio** supports importing draw.io files directly.

1. Open Microsoft Visio.
2. **File** → **Open** → Browse to `.drawio` file.
3. Visio will import and convert the diagram.
4. Review and adjust shapes as needed.
5. **File** → **Save As** → `.vsdx`.

> **Alternative:** Export from draw.io as VSDX first (Method 1), then open in Visio.

---

## Diagram Files in This Repository

| File | Description | Recommended Export |
|------|-------------|-------------------|
| `diagrams/Network_Architecture.drawio` | Full network topology | A3 PDF, PNG 200% |
| `diagrams/SIP_Trunk_STC_Architecture.drawio` | STC SIP trunk + SBC + IP Office | A4 PDF, PNG |
| `diagrams/Building_Detail_A.drawio` | Building A detail | A3 PDF, VSDX |
| `diagrams/Building_Detail_B.drawio` | Building B + survivability | A3 PDF, VSDX |

---

## Recommended Export Settings for Customer Delivery

| Output Format | Settings | Use Case |
|---------------|----------|----------|
| PDF (A3) | Fit page, 150%, white background | Formal proposal appendix |
| PDF (A4) | Fit page, portrait | Quick reference |
| PNG (200%) | 200% zoom, white background | PowerPoint/Word embedding |
| SVG | Default | Web / scalable presentations |
| VSDX | All pages | Visio users for editing |

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Visio shapes not rendering | Use draw.io shapes library compatible with Visio; avoid Cisco-specific shapes |
| PDF text cut off | Increase page margins in export settings; use "Fit Page" |
| PNG too low resolution | Increase zoom to 200% or 300% |
| Draw.io file won't open | Ensure valid XML; open in text editor to check for corruption |
| Missing fonts in Visio | Install matching fonts on the Visio machine |

---

*[YOUR COMPANY NAME] | Visio Instructions | PROP-2026-AVAYA-001*

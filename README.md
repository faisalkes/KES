# KES – Avaya IP Office V2 Server Edition Proposal Package

This repository contains a complete proposal package for an **Avaya IP Office Server Edition R12.x** deployment serving two buildings connected via fiber optic cable, with an STC Saudi Telecom SIP trunk.

---

## Deliverables Index

### Proposal Documents (`proposal/`)

| File | Description |
|------|-------------|
| [Avaya_IPOffice_Proposal.md](proposal/Avaya_IPOffice_Proposal.md) | Full professional proposal – cover page, executive summary, architecture, BOM summary, T&C, acceptance |
| [STC_SIP_Trunk_Configuration.md](proposal/STC_SIP_Trunk_Configuration.md) | Detailed STC SIP trunk & SBC (Avaya SBCE / AudioCodes) configuration guide |
| [BOM_Pricing.csv](proposal/BOM_Pricing.csv) | CSV Bill of Materials & pricing template (all prices are estimates) |
| [BOM_Pricing_Detailed.md](proposal/BOM_Pricing_Detailed.md) | Markdown-formatted BOM with subtotals and grand total |
| [Project_Timeline.md](proposal/Project_Timeline.md) | 12–16 week project implementation plan |
| [Acceptance_Form.md](proposal/Acceptance_Form.md) | Standalone customer acceptance / sign-off form |
| [PDF_Export_Guide.md](proposal/PDF_Export_Guide.md) | How to export Markdown → PDF / DOCX using Pandoc & GUI tools |

### Network Diagrams (`diagrams/`)

| File | Description |
|------|-------------|
| [Network_Architecture.drawio](diagrams/Network_Architecture.drawio) | Full topology: STC cloud, WAN, firewall, SBC, server, both buildings |
| [SIP_Trunk_STC_Architecture.drawio](diagrams/SIP_Trunk_STC_Architecture.drawio) | STC SIP trunk focus: SBC, firewall, IP Office |
| [Building_Detail_A.drawio](diagrams/Building_Detail_A.drawio) | Building A detail: server, IP500 V2 #1, IP phones, analog extensions |
| [Building_Detail_B.drawio](diagrams/Building_Detail_B.drawio) | Building B detail: IP500 V2 #2, IP phones, analog extensions, survivability |
| [Visio_Instructions.md](diagrams/Visio_Instructions.md) | How to export draw.io diagrams to Visio (.vsdx), PDF, and PNG |

---

## System Summary

| Parameter | Value |
|-----------|-------|
| Platform | Avaya IP Office Server Edition R12.x |
| Primary server | On-premise physical server (Dell PowerEdge R250 / HPE DL20 Gen10+) |
| Building A controller | Avaya IP500 V2 + 2× Phone 16 V2 cards |
| Building B controller | Avaya IP500 V2 + 2× Phone 16 V2 cards |
| IP phones | 1,000 total (500 per building) – J-Series |
| Analog extensions | 60 total (30 per building) |
| SIP trunk | 100 channels via STC Saudi Telecom |
| Session Border Controller | Avaya SBCE (primary) / AudioCodes Mediant (alternative) |
| Voicemail Pro | Centralized, 50 concurrent ports |
| Total endpoints | ~1,060 |

---

## Proposal Reference

- **Proposal #:** PROP-2026-AVAYA-001  
- **Date:** March 7, 2026  
- **Prepared for:** [CUSTOMER NAME]  
- **Prepared by:** [YOUR COMPANY NAME]

---

> **Note:** STC SIP proxy/registrar IP addresses, FQDN details, and DID ranges are provided by STC Saudi Telecom and must be confirmed during the pre-implementation phase.

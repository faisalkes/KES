# Bill of Materials & Pricing – Detailed
## Avaya IP Office Server Edition R12.x Proposal

**Proposal #:** PROP-2026-AVAYA-001  
**Date:** March 7, 2026  
**Prepared by:** [YOUR COMPANY NAME]  
**Prepared for:** [CUSTOMER NAME]

> ⚠️ **IMPORTANT DISCLAIMER:** All prices listed in this document are **estimates only** for budgetary planning purposes. Actual pricing is subject to Avaya partner pricing, current market rates, applicable VAT, customs duties in the Kingdom of Saudi Arabia, and final scope confirmation. A formal, binding quotation will be provided upon written request.

---

## Table of Contents

1. [Server Hardware](#1-server-hardware)
2. [Session Border Controller](#2-session-border-controller)
3. [IP500 V2 Controllers & Analog Cards](#3-ip500-v2-controllers--analog-cards)
4. [IP Phones – J-Series](#4-ip-phones--j-series)
5. [Analog Phones (Optional)](#5-analog-phones-optional)
6. [Software & Licenses](#6-software--licenses)
7. [Network Infrastructure – PoE Switches](#7-network-infrastructure--poe-switches)
8. [Professional Services](#8-professional-services)
9. [Training](#9-training)
10. [Support & Maintenance – Year 1](#10-support--maintenance--year-1)
11. [Grand Total Summary](#11-grand-total-summary)

---

## 1. Server Hardware

| Item # | Part Description | Model | Qty | Unit Price (USD) | Total (USD) |
|--------|-----------------|-------|-----|-----------------|-------------|
| SH-001 | Physical Server – Dell PowerEdge R250 (Intel Xeon E-2314 / 32GB RAM / 2×480GB SSD RAID1 / 2×1GbE) | Dell PowerEdge R250 | 1 | $4,500 | $4,500 |
| SH-002 | Rack mounting kit 1U | Dell ReadyRails 1U | 1 | $150 | $150 |
| SH-003 | UPS for server rack (1500VA) | APC SMT1500 | 1 | $600 | $600 |
| SH-004 | Server rack cabinet (12U) | Generic 12U Rack | 1 | $350 | $350 |

**Subtotal – Server Hardware: $5,600**

---

## 2. Session Border Controller

> **Note:** Price either the Avaya SBCE option (SBC-001 + SBC-002) **OR** the AudioCodes Mediant alternative (SBC-ALT-001). Do not price both.

### Option A – Avaya SBCE (Primary Recommendation)

| Item # | Part Description | Model | Qty | Unit Price (USD) | Total (USD) |
|--------|-----------------|-------|-----|-----------------|-------------|
| SBC-001 | Avaya SBCE – Session Border Controller for Enterprise (software license, 100 sessions) | Avaya SBCE | 1 | $9,500 | $9,500 |
| SBC-002 | SBCE dedicated server appliance hardware | Avaya SBCE Appliance | 1 | $2,500 | $2,500 |

**Subtotal – SBC Option A (Avaya SBCE): $12,000**

### Option B – AudioCodes Mediant (Alternative)

| Item # | Part Description | Model | Qty | Unit Price (USD) | Total (USD) |
|--------|-----------------|-------|-----|-----------------|-------------|
| SBC-ALT-001 | AudioCodes Mediant 800 SBC (100 SIP sessions) | AudioCodes Mediant 800 | 1 | $6,500 | $6,500 |

**Subtotal – SBC Option B (AudioCodes): $6,500**

---

## 3. IP500 V2 Controllers & Analog Cards

| Item # | Part Description | Model | Qty | Unit Price (USD) | Total (USD) |
|--------|-----------------|-------|-----|-----------------|-------------|
| CTL-001 | Avaya IP500 V2 Control Unit – Building A | Avaya IP500 V2 | 1 | $4,500 | $4,500 |
| CTL-002 | Avaya IP500 V2 Control Unit – Building B | Avaya IP500 V2 | 1 | $4,500 | $4,500 |
| CTL-003 | Phone 16 V2 Card (16 analog ports) – Building A Card 1 | Avaya Phone 16 V2 | 1 | $800 | $800 |
| CTL-004 | Phone 16 V2 Card (16 analog ports) – Building A Card 2 | Avaya Phone 16 V2 | 1 | $800 | $800 |
| CTL-005 | Phone 16 V2 Card (16 analog ports) – Building B Card 1 | Avaya Phone 16 V2 | 1 | $800 | $800 |
| CTL-006 | Phone 16 V2 Card (16 analog ports) – Building B Card 2 | Avaya Phone 16 V2 | 1 | $800 | $800 |
| CTL-007 | IP500 V2 Base Card – VCM 64 (Voice Compression Module) | Avaya VCM 64 | 2 | $700 | $1,400 |

**Subtotal – IP500 V2 Controllers & Cards: $13,600**

> **Analog capacity:** 2 × Phone 16 V2 = 32 ports per building. 30 ports used, 2 spare. Total: 64 ports across 2 buildings; 60 in use.

---

## 4. IP Phones – J-Series

| Item # | Model | Description | Role | Qty | Unit Price (USD) | Total (USD) |
|--------|-------|-------------|------|-----|-----------------|-------------|
| PH-001 | Avaya J129 | Monochrome 2.3" display, 1 line | Lobby / Common Area | 50 | $95 | $4,750 |
| PH-002 | Avaya J139 | Monochrome 3.2" display, 3 lines, 24 keys | General Staff | 300 | $120 | $36,000 |
| PH-003 | Avaya J159 | Color 3.5" display, 5 lines, Bluetooth, USB | Standard Office | 400 | $155 | $62,000 |
| PH-004 | Avaya J169 | Color 3.5" display, 16 lines, Bluetooth, USB | Power User / Reception | 150 | $185 | $27,750 |
| PH-005 | Avaya J179 | Color 3.5" display, 16 lines, Bluetooth, USB | Manager / Supervisor | 70 | $210 | $14,700 |
| PH-006 | Avaya J189 | Color 5.5" display, 16 lines, Bluetooth | Senior Executive | 20 | $280 | $5,600 |
| PH-007 | Avaya J199 | Color 7" touchscreen, 16 lines, USB-A/C | C-Suite / Boardroom | 10 | $420 | $4,200 |

**Subtotal – IP Phones (1,000 units): $155,000**

### Phone Mix Summary

| Model | Qty | % of Total |
|-------|-----|-----------|
| J129 | 50 | 5% |
| J139 | 300 | 30% |
| J159 | 400 | 40% |
| J169 | 150 | 15% |
| J179 | 70 | 7% |
| J189 | 20 | 2% |
| J199 | 10 | 1% |
| **Total** | **1,000** | **100%** |

---

## 5. Analog Phones (Optional)

> Analog phones are optional. [CUSTOMER NAME] may use existing analog devices or procure separately.

| Item # | Part Description | Model | Qty | Unit Price (USD) | Total (USD) |
|--------|-----------------|-------|-----|-----------------|-------------|
| AP-001 | Analog desk phone – basic model for analog extension ports | Generic Analog Phone | 60 | $35 | $2,100 |

**Subtotal – Analog Phones (Optional, 60 units): $2,100**

---

## 6. Software & Licenses

| Item # | Part Description | Model | Qty | Unit Price (USD) | Total (USD) |
|--------|-----------------|-------|-----|-----------------|-------------|
| SW-001 | Avaya IP Office Server Edition R12.x – Base Software License | IPO Server Edition | 1 | $3,500 | $3,500 |
| SW-002 | Avaya IP Office – IP User License (1,000 endpoints, anchored on server) | IPO IP User | 1,000 | $20 | $20,000 |
| SW-003 | Avaya Voicemail Pro – 50 Concurrent Port License | IPO Voicemail Pro | 1 | $4,500 | $4,500 |
| SW-004 | Avaya one-X Portal License – 100 concurrent users (optional) | IPO one-X Portal | 100 | $25 | $2,500 |
| SW-005 | Avaya IP Office – SIP Trunk License (100 channels) | IPO SIP Trunk | 100 | $10 | $1,000 |
| SW-006 | Avaya IP Office – Essential Edition Upgrade (if applicable) | IPO Essential | 1 | $1,500 | $1,500 |

**Subtotal – Software & Licenses: $33,000**

---

## 7. Network Infrastructure – PoE Switches

> Switch models shown are examples. Final selection depends on [CUSTOMER NAME]'s preferred vendor and existing infrastructure. Prices are estimates.

| Item # | Part Description | Model (Example) | Qty | Unit Price (USD) | Total (USD) |
|--------|-----------------|-----------------|-----|-----------------|-------------|
| NW-001 | 48-Port PoE+ Managed Switch (802.3at, 740W) – Bldg A Floor 1 | Cisco Catalyst 9200-48P | 2 | $3,500 | $7,000 |
| NW-002 | 48-Port PoE+ Managed Switch (802.3at, 740W) – Bldg A Floor 2 | Cisco Catalyst 9200-48P | 2 | $3,500 | $7,000 |
| NW-003 | 48-Port PoE+ Managed Switch (802.3at, 740W) – Bldg B Floor 1 | Cisco Catalyst 9200-48P | 2 | $3,500 | $7,000 |
| NW-004 | 48-Port PoE+ Managed Switch (802.3at, 740W) – Bldg B Floor 2 | Cisco Catalyst 9200-48P | 2 | $3,500 | $7,000 |
| NW-005 | Core/Aggregation Switch 24-Port SFP (fiber uplinks) | Cisco Catalyst 9300-24S | 2 | $5,000 | $10,000 |
| NW-006 | SFP Fiber Modules (SM/MM) for fiber interconnect | Generic SFP-1G-SX | 4 | $150 | $600 |
| NW-007 | Patch cables Cat6 1m (qty 200) | Generic Cat6 1m | 200 | $3 | $600 |

**Subtotal – Network Infrastructure: $39,200**

---

## 8. Professional Services

| Item # | Service Description | Unit | Qty (days) | Day Rate (USD) | Total (USD) |
|--------|--------------------|----|------------|---------------|-------------|
| SV-001 | Project management (16 weeks) | Lump Sum | 1 | $5,000 | $5,000 |
| SV-002 | Server hardware installation & configuration | Days | 2 | $800 | $1,600 |
| SV-003 | IP Office Server Edition software installation & base configuration | Days | 3 | $800 | $2,400 |
| SV-004 | Avaya SBCE installation & STC SIP trunk integration | Days | 3 | $800 | $2,400 |
| SV-005 | IP500 V2 controller installation – 2 buildings | Days | 4 | $800 | $3,200 |
| SV-006 | IP phone deployment & configuration – 1,000 phones (phased) | Days | 10 | $800 | $8,000 |
| SV-007 | Dial plan, ARS, and short code configuration | Days | 2 | $800 | $1,600 |
| SV-008 | Voicemail Pro & auto-attendant configuration | Days | 2 | $800 | $1,600 |
| SV-009 | VLAN / QoS / DHCP Option 176 network configuration | Days | 2 | $800 | $1,600 |
| SV-010 | User acceptance testing (UAT) support | Days | 2 | $800 | $1,600 |
| SV-011 | Go-live cutover & post-go-live hypercare support (30 days) | Days | 3 | $800 | $2,400 |

**Subtotal – Professional Services: $31,400**

---

## 10. Support & Maintenance – Year 1

| Item # | Part Description | Model | Qty | Unit Price (USD) | Total (USD) |
|--------|-----------------|-------|-----|-----------------|-------------|
| SP-001 | Avaya IP Office Software Support + Upgrade Subscription – Year 1 | Avaya SSU Year 1 | 1 | $4,000 | $4,000 |
| SP-002 | Hardware maintenance – Next Business Day on-site – Year 1 | NBD On-Site | 1 | $3,000 | $3,000 |
| SP-003 | 24×7 helpdesk support – Year 1 (optional) | [YOUR COMPANY NAME] | 1 | $3,500 | $3,500 |

**Subtotal – Support & Maintenance Year 1: $10,500**

---

## 9. Training

| Item # | Part Description | Qty | Unit Price (USD) | Total (USD) |
|--------|-----------------|-----|-----------------|-------------|
| TR-001 | End-user training – 1-day session (up to 20 users/session × 5 sessions) | 5 | $600 | $3,000 |
| TR-002 | Administrator training – 2-day advanced session | 1 | $1,200 | $1,200 |

**Subtotal – Training: $4,200**

---

## 11. Grand Total Summary

| # | Section | Subtotal (USD) |
|---|---------|---------------|
| 1 | Server Hardware | $5,600 |
| 2 | Session Border Controller (Avaya SBCE) | $12,000 |
| 3 | IP500 V2 Controllers & Analog Cards | $13,600 |
| 4 | IP Phones – J-Series (1,000 units) | $155,000 |
| 5 | Analog Phones (Optional) | $2,100 |
| 6 | Software & Licenses | $33,000 |
| 7 | Network Infrastructure – PoE Switches | $39,200 |
| 8 | Professional Services | $31,400 |
| 9 | Training | $4,200 |
| 10 | Support & Maintenance – Year 1 | $10,500 |
| | **GRAND TOTAL ESTIMATE** | **$306,600** |

> **Note:** If AudioCodes Mediant SBC (Option B, $6,500) is selected instead of Avaya SBCE (Option A, $12,000), deduct $5,500 from the grand total: **$301,100**.
>
> **Analog phones** are optional; add $2,100 if required.

---

### Exclusions (Not Priced)

- Structured cabling and civil works
- Customer firewall hardware and configuration
- STC account fees, SIP trunk monthly recurring charges
- Third-party integrations (CRM, ERP, etc.)
- Year 2+ software support renewal (available on request)
- Panduit/cabling accessories (available on request)

---

*All estimates are in US Dollars (USD). Applicable VAT and import duties in the Kingdom of Saudi Arabia are not included and will be calculated at time of formal quotation.*

*[YOUR COMPANY NAME] | PROP-2026-AVAYA-001 | Confidential*

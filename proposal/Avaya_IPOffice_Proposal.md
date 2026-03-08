# AVAYA IP OFFICE SERVER EDITION R12.x
## Unified Communications Solution Proposal

---

**Proposal #:** PROP-2026-AVAYA-001  
**Date:** March 7, 2026  
**Prepared for:** [CUSTOMER NAME]  
**Prepared by:** [YOUR COMPANY NAME]  
**Validity:** 90 days from proposal date

---

## Cover Page

```
╔══════════════════════════════════════════════════════════════════════════╗
║                                                                          ║
║         AVAYA IP OFFICE SERVER EDITION R12.x                             ║
║         Unified Communications & Telephony Solution                      ║
║                                                                          ║
║         Prepared for:  [CUSTOMER NAME]                                   ║
║         Prepared by:   [YOUR COMPANY NAME]                               ║
║         Proposal #:    PROP-2026-AVAYA-001                               ║
║         Date:          March 7, 2026                                     ║
║         Version:       1.0                                               ║
║                                                                          ║
║         CONFIDENTIAL – FOR [CUSTOMER NAME] USE ONLY                      ║
║                                                                          ║
╚══════════════════════════════════════════════════════════════════════════╝
```

---

## Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Scope of Work & Assumptions](#2-scope-of-work--assumptions)
3. [High-Level Architecture](#3-high-level-architecture)
4. [Low-Level Architecture](#4-low-level-architecture)
5. [Endpoint Portfolio – J-Series IP Phones](#5-endpoint-portfolio--j-series-ip-phones)
6. [STC SIP Trunk & Session Border Controller](#6-stc-sip-trunk--session-border-controller)
7. [Voicemail Pro](#7-voicemail-pro)
8. [Network Requirements](#8-network-requirements)
9. [Budget Estimate & Pricing Template](#9-budget-estimate--pricing-template)
10. [Project Timeline](#10-project-timeline)
11. [Terms & Conditions](#11-terms--conditions)
12. [Acceptance & Signature](#12-acceptance--signature)

---

## 1. Executive Summary

[YOUR COMPANY NAME] is pleased to present this proposal to [CUSTOMER NAME] for a comprehensive Unified Communications (UC) solution based on the **Avaya IP Office Server Edition R12.x** platform.

[CUSTOMER NAME] operates across two buildings (Building A and Building B) connected via an existing fiber optic cable. The proposed solution delivers a single, converged telephony platform that supports:

- **1,000 IP desk phones** (500 per building) using Avaya J-Series endpoints.
- **60 analog extensions** (30 per building) for fax machines, door phones, and legacy devices.
- **100-channel SIP trunk** via **STC Saudi Telecom** with a Session Border Controller (SBC) for security and interoperability.
- **Centralized Voicemail Pro** with 50 concurrent ports hosted on the primary server.
- **Business Continuity / Survivability** for Building B in the event of a WAN/fiber outage.

The solution is built entirely on-premise with no cloud dependencies, ensuring data sovereignty and full customer control. All software licenses are anchored on the primary server for a capacity of 1,000 IP endpoints.

---

## 2. Scope of Work & Assumptions

### 2.1 Scope of Work

| # | Deliverable |
|---|-------------|
| 1 | Supply and installation of Avaya IP Office Server Edition R12.x on dedicated physical server hardware |
| 2 | Supply and installation of two (2) Avaya IP500 V2 expansion controllers (one per building) |
| 3 | Supply and installation of four (4) Phone 16 V2 analog cards (two per controller, 32 ports each) |
| 4 | Supply and delivery of 1,000 Avaya J-Series IP phones (mix per Section 5) |
| 5 | Deployment and configuration of Avaya SBCE (Session Border Controller for Enterprise) |
| 6 | STC SIP trunk provisioning (coordination with STC; see Section 6) |
| 7 | Centralized Voicemail Pro configuration (50 concurrent ports, auto-attendant, hunt groups) |
| 8 | IP phone VLAN, QoS (DSCP), and DHCP Option 176 configuration |
| 9 | Dial plan configuration (internal, SIP trunk, DID routing) |
| 10 | User training (end-user and administrator sessions) |
| 11 | Documentation package (as-built, admin guide) |
| 12 | Post-go-live support (30-day hypercare) |

### 2.2 Assumptions

1. Customer premises cabling (structured cabling, patch panels) is complete and certified Cat5e/Cat6.
2. Existing fiber optic link between Building A and Building B is operational and provides ≥1 Gbps throughput.
3. Customer provides adequate rack space, power (with UPS), and cooling for server and IP500 V2 units.
4. STC Saudi Telecom provides SIP proxy/registrar IP address, FQDN, DID ranges, and authentication credentials prior to integration testing. These values are placeholders (TBD) in this document.
5. PoE-capable switches are available or will be procured separately (see Section 8 for specifications).
6. Internet/WAN connectivity for SBC public interface is the customer's responsibility.
7. Third-party integration (CRM, ERP) is out of scope unless agreed separately.
8. All software licensing is perpetual; annual software support subscription recommended (priced separately).
9. Physical security of server room and equipment is the customer's responsibility.

---

## 3. High-Level Architecture

```
                         ┌─────────────────────────────────────────────┐
                         │           INTERNET / WAN                    │
                         │                                             │
                         │   ┌─────────────────────────────────┐      │
                         │   │  STC Saudi Telecom SIP Network  │      │
                         │   │  (SIP Proxy/Registrar TBD)      │      │
                         │   └────────────────┬────────────────┘      │
                         └────────────────────│────────────────────────┘
                                              │ SIP (UDP/TCP 5060 or TLS 5061)
                                              │ 100 Channels
                                    ┌─────────▼──────────┐
                                    │  FIREWALL / NAT    │
                                    │  (Customer FW)     │
                                    └─────────┬──────────┘
                                              │
                                    ┌─────────▼──────────┐
                                    │  AVAYA SBCE        │
                                    │  Session Border    │
                                    │  Controller        │
                                    └─────────┬──────────┘
                                              │ SIP Trunk (Internal)
                         ┌────────────────────▼────────────────────────┐
                         │              BUILDING A (Main Site)          │
                         │                                              │
                         │  ┌──────────────────────────────────────┐   │
                         │  │  Physical Server (Dell R250 / HPE)   │   │
                         │  │  Avaya IP Office Server Edition R12  │   │
                         │  │  + Voicemail Pro (50 ports)          │   │
                         │  │  + 1,000 EP Licenses                 │   │
                         │  └────────────────────┬─────────────────┘   │
                         │                       │ SCN over LAN        │
                         │  ┌────────────────────▼─────────────────┐   │
                         │  │  IP500 V2 Controller #1              │   │
                         │  │  2× Phone 16 V2 (32 ports)          │   │
                         │  │  30 Analog Extensions                │   │
                         │  └──────────────────────────────────────┘   │
                         │                                              │
                         │  500 × J-Series IP Phones (VLAN Voice)      │
                         └──────────────────────┬───────────────────────┘
                                                │
                                    Fiber Optic Link (Existing)
                                    SCN over IP / SIP
                                                │
                         ┌──────────────────────▼───────────────────────┐
                         │              BUILDING B (Remote Site)         │
                         │                                               │
                         │  ┌───────────────────────────────────────┐   │
                         │  │  IP500 V2 Controller #2               │   │
                         │  │  2× Phone 16 V2 (32 ports)           │   │
                         │  │  30 Analog Extensions                 │   │
                         │  │  Survivability Mode                   │   │
                         │  └───────────────────────────────────────┘   │
                         │                                               │
                         │  500 × J-Series IP Phones (VLAN Voice)       │
                         └───────────────────────────────────────────────┘
```

---

## 4. Low-Level Architecture

### 4.1 Primary Server – Building A

| Parameter | Specification |
|-----------|---------------|
| Hardware | Dell PowerEdge R250 (or HPE ProLiant DL20 Gen10+) |
| CPU | Intel Xeon E-2314 (4-core, 2.8 GHz) |
| RAM | 32 GB DDR4 ECC |
| Storage | 2 × 480 GB SSD (RAID 1 via hardware RAID controller) |
| Network | 2 × 1 GbE onboard NICs (NIC 1: LAN/voice; NIC 2: management/WAN) |
| Operating System | Red Hat Enterprise Linux (RHEL) – Avaya-bundled OVA/ISO |
| Application | Avaya IP Office Server Edition R12.x |
| Voicemail Pro | Centralized, 50 concurrent ports |
| Licensing | 1,000 IP endpoint licenses (anchored on server) |
| Power | Redundant PSU recommended |
| UPS | Required (customer-provided) |

> **Important:** This is an on-premise physical server. No cloud, virtual, or hosted deployment is included in this proposal.

### 4.2 IP500 V2 Controller #1 – Building A

| Parameter | Specification |
|-----------|---------------|
| Unit | Avaya IP500 V2 Control Unit |
| Analog Card | 2 × Phone 16 V2 (16 analog ports each = 32 total) |
| Ports Used | 30 (2 spare for future use) |
| Extension Type | Analog (2-wire RJ-11 / BT) |
| SCN | Small Community Network over LAN (Ethernet Cat6 to core switch) |
| Registration | All 500 Building A IP phones register directly to the primary server |
| Power | Integral PSU; UPS recommended |

### 4.3 IP500 V2 Controller #2 – Building B

| Parameter | Specification |
|-----------|---------------|
| Unit | Avaya IP500 V2 Control Unit |
| Analog Card | 2 × Phone 16 V2 (16 analog ports each = 32 total) |
| Ports Used | 30 (2 spare for future use) |
| Extension Type | Analog (2-wire RJ-11 / BT) |
| SCN | Small Community Network over fiber optic link to primary server |
| Registration | All 500 Building B IP phones register directly to the primary server |
| Survivability | IP500 V2 #2 acts as fallback call-processing node if fiber link fails (local calls maintained) |
| Power | Integral PSU; UPS required |

### 4.4 Survivability – Building B

When the fiber link between Building A and Building B is interrupted:

1. IP phones in Building B detect registration loss and re-register to the **local IP500 V2 #2** (configured as Secondary Server / SCN node).
2. Internal calls between Building B extensions continue without interruption.
3. Analog extensions on IP500 V2 #2 remain fully operational.
4. SIP trunk (via Building A SBC/server) is unavailable; a direct PSTN backup line to IP500 V2 #2 is **recommended** (ISDN BRI or analog CO – separate quote).
5. When the fiber is restored, IP phones automatically re-register to the primary server and full functionality resumes.

### 4.5 Capacity Summary

| Category | Quantity |
|----------|----------|
| IP Phones – Building A | 500 |
| IP Phones – Building B | 500 |
| **IP Phones Total** | **1,000** |
| Analog Extensions – Building A | 30 |
| Analog Extensions – Building B | 30 |
| **Analog Extensions Total** | **60** |
| SIP Trunk Channels | 100 |
| Voicemail Pro Concurrent Ports | 50 |
| **Total Endpoints** | **~1,060** |

---

## 5. Endpoint Portfolio – J-Series IP Phones

### 5.1 J-Series Model Specifications

| Model | Display | Lines | Keys | Bluetooth | USB | Best For |
|-------|---------|-------|------|-----------|-----|----------|
| J129 | Monochrome 2.3" | 1 | — | No | No | Lobby, common area, basic voice |
| J139 | Monochrome 3.2" | 3 | 24 | No | No | General office, basic users |
| J159 | Color 3.5" | 5 | 10+12 | Yes | Yes | Standard office users |
| J169 | Color 3.5" | 16 | 12+12 | Yes | Yes | Power users, receptionists |
| J179 | Color 3.5" | 16 | 12+12 | Yes | Yes | Executive, advanced features |
| J189 | Color 5.5" | 16 | 12+12 | Yes | Yes | Executive suite, video-ready |
| J199 | Color 7" | 16 | 24+24 | Yes | USB-A/C | Executive, conferencing, touchscreen |

### 5.2 Recommended Phone Mix (1,000 Units)

| Role | Model | Qty | % |
|------|-------|-----|---|
| Lobby / Common Area | J129 | 50 | 5% |
| General Staff | J139 | 300 | 30% |
| Standard Office | J159 | 400 | 40% |
| Power User / Reception | J169 | 150 | 15% |
| Manager / Supervisor | J179 | 70 | 7% |
| Senior Executive | J189 | 20 | 2% |
| C-Suite / Boardroom | J199 | 10 | 1% |
| **Total** | | **1,000** | **100%** |

> **Note:** Phone mix can be adjusted based on [CUSTOMER NAME] organizational requirements at no change in total hardware pricing structure.

---

## 6. STC SIP Trunk & Session Border Controller

### 6.1 Overview

SIP trunk services are provided by **STC Saudi Telecom Company** (Saudi Arabia). A **Session Border Controller (SBC)** is mandatory between the STC SIP network and the Avaya IP Office to provide:

- Protocol normalization and interoperability
- Security (topology hiding, DoS/DDoS protection, TLS/SRTP)
- NAT traversal
- Media transcoding if required

### 6.2 Session Border Controller Options

| Option | Product | Notes |
|--------|---------|-------|
| **Primary (Recommended)** | Avaya SBCE (Session Border Controller for Enterprise) | Native integration with IP Office; certified for STC |
| **Alternative** | AudioCodes Mediant SBC (500/800/2600 series) | Widely deployed in KSA; STC-certified alternative |

### 6.3 STC SIP Trunk Parameters

| Parameter | Value |
|-----------|-------|
| Provider | STC Saudi Telecom Company |
| Channels | 100 simultaneous calls |
| Primary SIP Proxy/Registrar | **TBD – provided by STC** |
| Secondary SIP Proxy/Registrar | **TBD – provided by STC** |
| Authentication Method | IP-based (preferred) or Registration (TBD with STC) |
| DID Range | **TBD – provided by STC** |
| Transport | UDP port 5060 or TCP port 5060 (TLS 5061 if STC supports SIPS) |
| Primary Codec | G.711A (a-law) |
| Secondary Codec | G.729 |
| DTMF | RFC 2833 (RTP Event) |
| RTP Port Range | 49152–65535 (configurable per IP Office/SBC policy) |
| PRACK | As negotiated with STC |

> **Disclaimer:** STC SIP proxy/registrar IP addresses, FQDN, DID ranges, and authentication credentials are provisioned by STC Saudi Telecom and are **not included** in this proposal. [CUSTOMER NAME] must obtain these details from STC prior to integration testing.

### 6.4 Firewall / NAT Requirements

| Direction | Protocol | Port | Notes |
|-----------|----------|------|-------|
| Inbound (STC → SBC) | SIP/UDP or SIP/TCP | 5060 | Allow from STC proxy IPs |
| Inbound (STC → SBC) | SIP/TLS | 5061 | If TLS transport agreed |
| Inbound (STC → SBC) | RTP/UDP | 49152–65535 | Media streams |
| Outbound (SBC → STC) | SIP/UDP or TCP | 5060 | To STC proxy IP |
| Outbound (SBC → STC) | RTP/UDP | Per STC | Media |

- SBC should be placed in a DMZ or with a dedicated public IP.
- NAT hairpinning must be enabled on the firewall if SBC public and private IPs differ.
- SIP ALG on firewalls must be **disabled**.

### 6.5 SBC → IP Office Connectivity

- SBC connects to IP Office Server Edition via internal SIP trunk (LAN).
- IP Office SIP line configured to point to SBC internal IP address.
- Transport: UDP/TCP 5060 (internal; no TLS required on LAN segment).

---

## 7. Voicemail Pro

### 7.1 Overview

Centralized **Avaya Voicemail Pro** is hosted on the primary server (Building A) and serves all users across both buildings.

### 7.2 Key Features

| Feature | Description |
|---------|-------------|
| Concurrent Ports | 50 (included in license) |
| Mailboxes | Up to 1,060 (one per extension) |
| Auto-Attendant | Multi-level IVR menus; business/after-hours schedules |
| Hunt Group Voicemail | Shared group mailboxes for departments |
| Email Notification | Send voicemail as WAV attachment to email |
| Visual Voicemail | Via Avaya one-X Portal / Workplace app |
| Announcement Campaigns | Outbound announcement broadcasting |
| Call Recording | Basic call recording to mailbox (Voicemail Pro) |
| Multi-Language Prompts | Arabic and English supported |
| Fax Integration | Fax to email (requires separate fax server or analog fax) |

### 7.3 IVR / Auto-Attendant Design

A multi-level auto-attendant will be configured:

```
Main Number (DID) → STC → SBC → IP Office → Auto-Attendant
  ├─ Press 1: Sales Department (Hunt Group)
  ├─ Press 2: Technical Support (Hunt Group)
  ├─ Press 3: Accounts (Hunt Group)
  ├─ Press 4: Directory (by name)
  └─ Press 0: Reception / Operator
```

> Final IVR design to be confirmed with [CUSTOMER NAME] during project kick-off.

---

## 8. Network Requirements

### 8.1 VLAN Design

| VLAN ID | Name | Purpose |
|---------|------|---------|
| VLAN 10 | Data | PCs, servers, general data |
| VLAN 20 | Voice | IP phones (J-Series) |
| VLAN 30 | Management | Network infrastructure management |
| VLAN 40 | Security | IP cameras, access control (if applicable) |

> IP phones must be placed in the dedicated Voice VLAN (VLAN 20) using LLDP-MED or CDP for automatic VLAN assignment.

### 8.2 QoS (Quality of Service)

| Traffic Type | DSCP Marking | 802.1p |
|-------------|-------------|--------|
| Voice RTP (media) | EF (46) | 5 |
| SIP Signaling | CS3 (24) | 3 |
| Data | BE (0) | 0 |

- QoS must be configured end-to-end from IP phone to the IP Office server.
- Switch ports connected to IP phones must support 802.1p and DSCP remarking.
- Priority queuing must be enabled on all switches in the voice path.

### 8.3 PoE Requirements

| Switch Type | Standard | Notes |
|-------------|----------|-------|
| Access Layer | 802.3af (15.4W) minimum | J129, J139, J159 |
| Access Layer | 802.3at (30W) preferred | J169, J179, J189, J199 |
| Recommended | 802.3at / PoE+ | Future-proofs all J-Series models |

- Estimated PoE budget: 500 phones × 15W average = 7,500W per building.
- PoE switches must be sized accordingly (e.g., 24-port 370W or 48-port 740W).

### 8.4 DHCP Option 176

IP phones use DHCP Option 176 to discover the IP Office server automatically.

```
DHCP Option 176 Value (example):
  MCIPADD=<IP_OFFICE_SERVER_IP>,MCPORT=7070,HTTPSRVR=<IP_OFFICE_SERVER_IP>
```

- Configure Option 176 on the DHCP server (Windows Server / network switch).
- Separate DHCP scopes for Voice VLAN (VLAN 20) and Data VLAN (VLAN 10).

### 8.5 Fiber Optic Link (Building A ↔ Building B)

| Parameter | Requirement |
|-----------|-------------|
| Type | Single-mode or multi-mode fiber (existing) |
| Bandwidth | ≥ 1 Gbps (Gigabit Ethernet recommended) |
| Protocol | Layer 2 (VLAN trunking) or Layer 3 (routed) |
| SCN Traffic | IP Office SCN over IP on fiber |
| Voice VLAN | Tagged across fiber trunk |
| QoS | DSCP/802.1p must be preserved across the fiber link |
| Latency | < 20 ms one-way for acceptable voice quality |
| Redundancy | Recommend dual fiber paths or VRRP for router failover |

---

## 9. Budget Estimate & Pricing Template

> **IMPORTANT DISCLAIMER:** All prices listed below are **estimates only** for budgetary planning purposes. Actual pricing is subject to Avaya partner pricing, current market rates, applicable VAT, customs duties, and final scope confirmation. A formal binding quotation will be provided upon request.

### 9.1 Summary Budget Estimate (USD)

| Category | Estimated Budget (USD) |
|----------|----------------------|
| Server Hardware | $4,500 – $6,500 |
| Session Border Controller (Avaya SBCE) | $8,000 – $12,000 |
| IP500 V2 Controllers & Cards (×2 sites) | $12,000 – $18,000 |
| IP Phones – J-Series (1,000 units) | $180,000 – $280,000 |
| Software & Licenses | $25,000 – $40,000 |
| Network Infrastructure (PoE Switches) | $30,000 – $50,000 |
| Professional Services & Installation | $20,000 – $35,000 |
| Training | $3,000 – $5,000 |
| Support (Year 1) | $8,000 – $15,000 |
| **Estimated Total** | **$290,500 – $461,500** |

> See `BOM_Pricing.csv` and `BOM_Pricing_Detailed.md` for itemized line-item detail.

---

## 10. Project Timeline

See `Project_Timeline.md` for the full 12–16 week implementation plan.

| Phase | Duration | Key Milestones |
|-------|----------|----------------|
| Phase 1: Kick-off & Design | Weeks 1–2 | Requirements sign-off, design approval |
| Phase 2: Procurement | Weeks 3–5 | Hardware ordered and delivered |
| Phase 3: Lab Build & Testing | Weeks 5–7 | Server, SBCE, IP500 V2 lab build |
| Phase 4: Site Preparation | Weeks 6–8 | Cabling, VLAN, DHCP, switch config |
| Phase 5: Installation | Weeks 8–11 | On-site installation, STC provisioning |
| Phase 6: UAT & Training | Weeks 11–13 | User acceptance testing, training |
| Phase 7: Go-Live & Hypercare | Weeks 13–16 | Cutover, 30-day post-go-live support |

---

## 11. Terms & Conditions

### 11.1 Payment Terms

- 40% upon proposal acceptance and purchase order.
- 40% upon equipment delivery to site.
- 20% upon project go-live acceptance.
- All invoices payable within 30 days of invoice date.

### 11.2 Warranty

- Hardware: Manufacturer warranty (Dell/HPE 3-year next business day; Avaya IP500 V2 1-year).
- Software: Avaya software support subscription (annual, quoted separately).
- Installation workmanship: 90-day warranty from go-live date.

### 11.3 Exclusions

- Structured cabling (unless separately quoted).
- Civil works, power, cooling, or UPS.
- Customer-side firewall configuration (guidance provided; execution by customer).
- STC account management, contract, and provisioning fees.
- Third-party integrations not listed in scope.
- Any works not explicitly described in Section 2.1.

### 11.4 Governing Law

This proposal and any resulting agreement shall be governed by the laws of the Kingdom of Saudi Arabia.

### 11.5 Confidentiality

This proposal contains proprietary and confidential information of [YOUR COMPANY NAME]. [CUSTOMER NAME] agrees not to disclose this proposal or its contents to any third party without prior written consent of [YOUR COMPANY NAME].

### 11.6 Validity

This proposal is valid for **90 days** from the date of issue (March 7, 2026). [YOUR COMPANY NAME] reserves the right to revise pricing after this period.

### 11.7 Force Majeure

Neither party shall be liable for failure to perform obligations due to circumstances beyond reasonable control including acts of God, government actions, or natural disasters.

---

## 12. Acceptance & Signature

By signing below, [CUSTOMER NAME] confirms acceptance of this proposal and authorizes [YOUR COMPANY NAME] to proceed with the project as described.

---

**For [CUSTOMER NAME]:**

| Field | Details |
|-------|---------|
| Authorized Signatory Name | __________________________________ |
| Title / Position | __________________________________ |
| Signature | __________________________________ |
| Date | __________________________________ |
| Company Stamp | __________________________________ |

---

**For [YOUR COMPANY NAME]:**

| Field | Details |
|-------|---------|
| Authorized Signatory Name | __________________________________ |
| Title / Position | __________________________________ |
| Signature | __________________________________ |
| Date | __________________________________ |
| Company Stamp | __________________________________ |

---

> See `proposal/Acceptance_Form.md` for a standalone printable acceptance form.

---

*End of Proposal PROP-2026-AVAYA-001*

*[YOUR COMPANY NAME] | [Address] | [Phone] | [Email] | [Website]*

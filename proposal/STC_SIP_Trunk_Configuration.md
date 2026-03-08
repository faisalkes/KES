# STC Saudi Telecom SIP Trunk Configuration Guide
## Avaya IP Office Server Edition R12.x with SBC

**Document Reference:** PROP-2026-AVAYA-001-STC  
**Date:** March 7, 2026  
**Prepared by:** [YOUR COMPANY NAME]

---

## Table of Contents

1. [Overview](#1-overview)
2. [Required Information Checklist (STC)](#2-required-information-checklist-stc)
3. [Network Topology](#3-network-topology)
4. [Session Border Controller – Avaya SBCE (Primary)](#4-session-border-controller--avaya-sbce-primary)
5. [Session Border Controller – AudioCodes Mediant (Alternative)](#5-session-border-controller--audiocodes-mediant-alternative)
6. [Avaya IP Office SIP Line Configuration](#6-avaya-ip-office-sip-line-configuration)
7. [Dial Plan Configuration](#7-dial-plan-configuration)
8. [Firewall & NAT Rules](#8-firewall--nat-rules)
9. [Testing & Verification](#9-testing--verification)
10. [Troubleshooting Guide](#10-troubleshooting-guide)

---

## 1. Overview

This document provides detailed configuration guidance for connecting Avaya IP Office Server Edition R12.x to the **STC Saudi Telecom SIP trunk** service. A Session Border Controller (SBC) is mandatory and must be placed between the STC SIP network and the IP Office.

### Architecture Flow

```
STC Saudi Telecom
      │
      │  SIP (UDP/TCP 5060 or TLS 5061)
      │  100 channels
      ▼
┌─────────────┐
│  FIREWALL   │  (Customer-managed)
│  NAT/DMZ    │
└──────┬──────┘
       │
┌──────▼──────────────────────┐
│  SESSION BORDER CONTROLLER  │
│  (Avaya SBCE or AudioCodes) │
│  Public IP: [TBD]           │
│  Private IP: [TBD]          │
└──────┬──────────────────────┘
       │  SIP (Internal, UDP 5060)
       │
┌──────▼──────────────────────┐
│  AVAYA IP OFFICE            │
│  Server Edition R12.x       │
│  IP: [TBD – Internal]       │
└─────────────────────────────┘
```

---

## 2. Required Information Checklist (STC)

Before STC SIP trunk integration can proceed, the following information **must be obtained from STC Saudi Telecom**. These values are placeholders in this document.

| # | Parameter | Status | Value |
|---|-----------|--------|-------|
| 1 | Primary SIP Proxy IP Address | ⬜ TBD | ___________________ |
| 2 | Secondary SIP Proxy IP Address | ⬜ TBD | ___________________ |
| 3 | Primary SIP Proxy FQDN | ⬜ TBD | ___________________ |
| 4 | Secondary SIP Proxy FQDN | ⬜ TBD | ___________________ |
| 5 | SIP Proxy Port | ⬜ TBD | 5060 / 5061 |
| 6 | SIP Transport Protocol | ⬜ TBD | UDP / TCP / TLS |
| 7 | Authentication Method | ⬜ TBD | IP-Based / Registration |
| 8 | SIP Username / Account ID (if registration) | ⬜ TBD | ___________________ |
| 9 | SIP Password / Secret (if registration) | ⬜ TBD | ___________________ |
| 10 | Number of Channels / CPS | ⬜ TBD | 100 channels |
| 11 | DID Range (Main DDI) | ⬜ TBD | ___________________ |
| 12 | DID Range (Full range) | ⬜ TBD | ___________________ |
| 13 | Pilot / Main Number | ⬜ TBD | ___________________ |
| 14 | Outbound Caller ID (ANI) format | ⬜ TBD | E.164 / National |
| 15 | DTMF Method | ⬜ TBD | RFC 2833 |
| 16 | Primary Codec | ⬜ TBD | G.711A |
| 17 | Secondary Codec | ⬜ TBD | G.729 |
| 18 | SIP Re-INVITE support | ⬜ TBD | Yes / No |
| 19 | SIP UPDATE support | ⬜ TBD | Yes / No |
| 20 | SIP PRACK support (100rel) | ⬜ TBD | Required / Optional |
| 21 | RTP port range (STC side) | ⬜ TBD | ___________________ |
| 22 | Media IP (if different from SIP) | ⬜ TBD | ___________________ |
| 23 | Customer SBC/Firewall Public IP | ⬜ TBD | ___________________ |
| 24 | FROM header format | ⬜ TBD | E.164 / SIP URI |
| 25 | Max call duration limit | ⬜ TBD | ___________________ |

> **Note:** Contact your STC account manager or STC business support to obtain the above details. Do not proceed with SBC/IP Office SIP configuration until items 1–10 are confirmed.

---

## 3. Network Topology

```
┌─────────────────────────────────────────────────────────────────────┐
│                    STC SIP NETWORK (Cloud/Core)                      │
│                                                                       │
│  Primary SIP Proxy:    [TBD – provided by STC]                       │
│  Secondary SIP Proxy:  [TBD – provided by STC]                       │
│  DID Range:            [TBD – provided by STC]                       │
└──────────────────────────┬────────────────────────────────────────────┘
                           │ UDP/TCP 5060 (or TLS 5061)
                           │ 100 SIP Channels
              ┌────────────▼────────────┐
              │     INTERNET / WAN      │
              └────────────┬────────────┘
                           │
              ┌────────────▼────────────┐
              │   CUSTOMER FIREWALL     │
              │   Public IP: [TBD]      │
              │   SIP ALG: DISABLED     │
              └────────────┬────────────┘
                           │ DMZ / Trusted Zone
              ┌────────────▼────────────────────────────┐
              │         AVAYA SBCE / AudioCodes SBC       │
              │  Public (WAN) IF:  [TBD]                  │
              │  Private (LAN) IF: [TBD]                  │
              │  SIP/5060 public  ←→ SIP/5060 internal    │
              │  RTP: 49152–65535 ←→ RTP: internal range  │
              └────────────┬────────────────────────────┘
                           │ LAN (Private)
              ┌────────────▼────────────────────────────┐
              │   AVAYA IP OFFICE SERVER EDITION R12.x   │
              │   IP: [TBD – Internal LAN]               │
              │   SIP Line → SBC internal IP             │
              └──────────────────────────────────────────┘
```

**IP Address Planning (To Be Confirmed)**

| Device | Interface | IP Address |
|--------|-----------|------------|
| Customer Firewall | WAN | [Public IP – ISP assigned] |
| Customer Firewall | LAN/DMZ | [TBD] |
| Avaya SBCE | Public (A1) | [TBD – from customer public range] |
| Avaya SBCE | Private (A2) | [TBD – e.g., 192.168.1.x] |
| IP Office Server | LAN | [TBD – e.g., 192.168.1.x] |
| IP500 V2 #1 (Bldg A) | LAN | [TBD] |
| IP500 V2 #2 (Bldg B) | LAN | [TBD] |

---

## 4. Session Border Controller – Avaya SBCE (Primary)

### 4.1 Avaya SBCE Overview

The Avaya **Session Border Controller for Enterprise (SBCE)** is the recommended SBC for integration with Avaya IP Office. It provides:

- Native SIP normalization for STC compliance.
- Topology hiding (hides internal IP Office IP from the STC network).
- TLS/SRTP for secure SIP (if STC supports SIPS).
- Denial-of-service (DoS) protection.
- Call admission control.

### 4.2 Avaya SBCE Sizing

| Parameter | Value |
|-----------|-------|
| Model | Avaya SBCE (software or appliance) |
| Sessions | 100 (match STC channel count) |
| Transcoding sessions | As required (G.711A ↔ G.729) |
| High Availability | Active/Standby pair recommended for production |

### 4.3 Avaya SBCE – STC SIP Server Profile

Configure the following in the Avaya SBCE management interface:

**Server Interworking Profile (STC Side):**

| Parameter | Value |
|-----------|-------|
| Profile Name | STC-SIP-Trunk |
| Server Type | Trunk Server |
| SIP Domain | [TBD – STC domain or IP] |
| Transport | UDP (default) or TCP/TLS per STC |
| Port | 5060 (or 5061 for TLS) |
| Proxy | Primary: [TBD STC IP/FQDN] |
| Proxy | Secondary: [TBD STC IP/FQDN] |
| Send REGISTER | Disable (IP-based auth) or Enable (registration auth) |
| Outbound Proxy | [TBD – STC outbound proxy if required] |

**Server Interworking Profile (IP Office Side):**

| Parameter | Value |
|-----------|-------|
| Profile Name | IPO-SIP-Trunk |
| Server Type | Call Server |
| IP Address | [IP Office Server IP] |
| Transport | UDP |
| Port | 5060 |

### 4.4 Avaya SBCE – Media Profile

| Parameter | Value |
|-----------|-------|
| Codec Priority 1 | G.711A (a-law, 64 kbps) |
| Codec Priority 2 | G.729 (8 kbps, no annex B) |
| DTMF | RFC 2833 / RTP Event (payload type 101) |
| RTP Port Range | 49152–65535 |
| SRTP | Disabled (unless STC requires) |
| VAD/CNG | Disabled (recommended for reliability) |

### 4.5 Avaya SBCE – Signaling Rules

- **FROM Header:** Set customer's ANI/caller ID in E.164 format (+966XXXXXXXXXX).
- **P-Asserted-Identity (PAI):** Pass through or generate per STC requirements.
- **Max-Forwards:** Default (70).
- **Session Timers:** Enable per RFC 4028; Session-Expires: 1800.
- **PRACK (100rel):** Configure per STC requirements (TBD).
- **SIP OPTIONS Keep-Alive:** Enable to detect STC trunk availability.

### 4.6 Avaya SBCE – Access Control List

| Rule | Source | Destination | Action |
|------|--------|-------------|--------|
| Allow STC Primary | [STC Primary SIP IP/FQDN] | SBCE Public IP | PERMIT |
| Allow STC Secondary | [STC Secondary SIP IP/FQDN] | SBCE Public IP | PERMIT |
| Allow IP Office | [IP Office LAN IP] | SBCE Private IP | PERMIT |
| Deny All | Any | SBCE Public IP | DENY |

---

## 5. Session Border Controller – AudioCodes Mediant (Alternative)

### 5.1 AudioCodes Mediant Overview

AudioCodes Mediant SBC series (500/800/2600) is an alternative SBC widely deployed in Saudi Arabia and certified with STC SIP trunks.

### 5.2 AudioCodes Mediant Configuration Summary

**SIP Interface (WAN – STC Facing):**

| Parameter | Value |
|-----------|-------|
| Application Type | Mediant SBC |
| SIP Interface | SIPInterface_STC |
| Network Interface | WAN (Public) |
| UDP Port | 5060 |
| TCP Port | 5060 |
| TLS Port | 5061 |
| Classification | By Proxy Set |

**SIP Interface (LAN – IP Office Facing):**

| Parameter | Value |
|-----------|-------|
| SIP Interface | SIPInterface_IPO |
| Network Interface | LAN (Private) |
| UDP Port | 5060 |

**Proxy Sets:**

| Proxy Set | Address | Port | Transport |
|-----------|---------|------|-----------|
| ProxySet_STC | [STC Primary SIP Proxy – TBD] | 5060 | UDP/TCP |
| ProxySet_STC | [STC Secondary SIP Proxy – TBD] | 5060 | UDP/TCP |
| ProxySet_IPO | [IP Office Server IP] | 5060 | UDP |

**IP Profile (STC):**

| Parameter | Value |
|-----------|-------|
| Name | IPProfile_STC |
| DTMF Mode | RFC 2833 |
| Codec Policy | G.711A primary, G.729 secondary |
| SBC Remove Unrequired Codecs | Enable |
| Session Expiry | 1800 |
| Min Session Expiry | 90 |

**IP Profile (IP Office):**

| Parameter | Value |
|-----------|-------|
| Name | IPProfile_IPO |
| DTMF Mode | RFC 2833 |
| Codec Policy | G.711A primary, G.729 secondary |

**Routing Rules:**

| Rule | Source Interface | Destination Proxy |
|------|-----------------|-------------------|
| STC → IPO | SIPInterface_STC | ProxySet_IPO |
| IPO → STC | SIPInterface_IPO | ProxySet_STC |

**Manipulation (Number Format):**

| Rule | Pattern | Replacement | Notes |
|------|---------|-------------|-------|
| Outbound CLI | \+966(.*) | 0\1 | Convert E.164 to national if required by STC |
| Inbound DID | ^(.*) | \1 | Pass through to IP Office |

> Actual manipulation rules depend on the number format required by STC and IP Office dial plan. Confirm with STC during integration testing.

---

## 6. Avaya IP Office SIP Line Configuration

### 6.1 IP Office Manager – SIP Line Settings

Navigate to: **IP Office Manager → Line → New Line → SIP Trunk**

| Parameter | Value |
|-----------|-------|
| Line Number | [Auto-assigned] |
| ITSP Domain Name | [SBC Private IP or FQDN] |
| Send Caller ID | As Dialed / E.164 |
| DTMF Support | RFC 2833 |
| Compression Mode | G.711 ULAW (or G.711 ALAW) |
| Fax Transport Support | T.38 (if STC supports) or G.711 Fax |
| Network Topology | NAT Firewall |
| STUN Server | Not required (SBC handles NAT) |
| Proxy / Registrar | [SBC Private IP] |
| Proxy Port | 5060 |
| Transport | UDP |
| SIP Channels | 100 |

### 6.2 SIP URI Configuration

| Channel | SIP URI | DID |
|---------|---------|-----|
| Pilot Number | sip:[MAIN_DID]@[SBC_IP] | [TBD – STC DID] |
| DID Range | sip:[DID_XXXX]@[SBC_IP] | [TBD – STC DID range] |

### 6.3 Incoming Call Routing

| Incoming DID | IP Office Route | Destination |
|--------------|-----------------|-------------|
| [Main Pilot Number] | Short Code | Auto-Attendant |
| [DID XXXX] | ARS / Short Code | Extension XXXX |
| [DID Group] | Hunt Group | Department Group |

---

## 7. Dial Plan Configuration

### 7.1 Internal Dial Plan

| Extension Range | Building | Controller |
|-----------------|----------|------------|
| 1000–1499 | Building A | IP Office Server / IP500 V2 #1 |
| 2000–2499 | Building B | IP500 V2 #2 |
| 1500–1529 | Building A Analog | IP500 V2 #1 |
| 2500–2529 | Building B Analog | IP500 V2 #2 |

### 7.2 Outbound Dial Plan (ARS – Automatic Route Selection)

| Pattern | Prefix | Route | Notes |
|---------|--------|-------|-------|
| 9 + XXXXXXXX | Strip 9 | SIP Trunk (STC) | Local 8-digit calls (Riyadh) |
| 9 + 0XXXXXXXXX | Strip 9 | SIP Trunk (STC) | National mobile |
| 9 + 00 + X | Strip 9 | SIP Trunk (STC) | International |
| 9 + 112/911 | Strip 9 | SIP Trunk (STC) | Emergency services |
| 1XXX | — | Internal | Building A |
| 2XXX | — | Internal | Building B |

### 7.3 Short Codes

| Short Code | Feature | Notes |
|------------|---------|-------|
| *1 | Voicemail | Access personal mailbox |
| *2 | Do Not Disturb ON | |
| *3 | Do Not Disturb OFF | |
| *4 | Call Forwarding All | |
| *5 | Cancel Call Forwarding | |
| *8 | Pick-Up Group Call | |
| *9 | Call Park | |
| 0 | Operator / Reception | Transfer to reception |

---

## 8. Firewall & NAT Rules

### 8.1 Inbound Rules (WAN → DMZ/SBC)

| Protocol | Source | Source Port | Destination | Dest Port | Action |
|----------|--------|-------------|-------------|-----------|--------|
| UDP | STC Primary Proxy IP | Any | SBC Public IP | 5060 | ALLOW |
| TCP | STC Primary Proxy IP | Any | SBC Public IP | 5060 | ALLOW |
| UDP | STC Secondary Proxy IP | Any | SBC Public IP | 5060 | ALLOW |
| TCP | STC Secondary Proxy IP | Any | SBC Public IP | 5060 | ALLOW |
| TLS | STC Proxy IPs | Any | SBC Public IP | 5061 | ALLOW (if TLS) |
| UDP | STC Media IPs | Any | SBC Public IP | 49152–65535 | ALLOW |
| ANY | ANY | ANY | SBC Public IP | ANY | DENY |

### 8.2 Outbound Rules (DMZ/SBC → WAN)

| Protocol | Source | Destination | Dest Port | Action |
|----------|--------|-------------|-----------|--------|
| UDP/TCP | SBC Public IP | STC Proxy IPs | 5060 | ALLOW |
| UDP | SBC Public IP | STC Media IPs | Any | ALLOW |

### 8.3 Internal Rules (DMZ/SBC → LAN/IP Office)

| Protocol | Source | Destination | Dest Port | Action |
|----------|--------|-------------|-----------|--------|
| UDP | SBC Private IP | IP Office Server IP | 5060 | ALLOW |
| UDP | SBC Private IP | IP Office Server IP | 49152–65535 | ALLOW |

### 8.4 Important Notes

- **Disable SIP ALG** on all firewalls and routers in the path. SIP ALG interferes with SBC operation.
- **NAT Keep-alive:** SBC sends periodic SIP OPTIONS to STC to keep NAT bindings open.
- **Hair-pinning:** If SBC public and private IPs are on different segments, ensure the firewall allows hair-pinning.
- **STUN:** Not required when using SBC; SBC handles all NAT traversal.

---

## 9. Testing & Verification

### 9.1 Pre-Go-Live Testing Checklist

| Test | Expected Result | Status |
|------|-----------------|--------|
| SBC registers to STC (if registration auth) | SBC shows REGISTERED status | ⬜ |
| SBC OPTIONS ping to STC proxy | 200 OK response | ⬜ |
| Outbound test call (internal ext → external mobile) | Call connects, audio both ways | ⬜ |
| Inbound test call (external mobile → DID) | Call routes to correct extension | ⬜ |
| Inbound to Auto-Attendant | IVR plays, DTMF selection works | ⬜ |
| Outbound CLI (caller ID) | Correct DID presented to called party | ⬜ |
| G.711A codec negotiation | INVITE shows G.711A in SDP | ⬜ |
| G.729 codec fallback | G.729 used when G.711A unavailable | ⬜ |
| DTMF (RFC 2833) | Tone events passed correctly in IVR | ⬜ |
| 100-channel capacity test | 100 concurrent calls without dropped calls | ⬜ |
| Call transfer (attended) | Transfer completes, audio preserved | ⬜ |
| Call transfer (blind) | Transfer completes | ⬜ |
| Call hold / resume | Hold music plays; resume works | ⬜ |
| Voicemail on busy/no-answer | Voicemail picks up after timeout | ⬜ |
| Fax (T.38 or G.711 passthrough) | Fax transmits successfully | ⬜ |
| STC failover to secondary proxy | Calls route via secondary if primary fails | ⬜ |
| Emergency call (112) | Connects to emergency services | ⬜ |

### 9.2 Diagnostic Commands (Avaya SBCE)

```bash
# Check SBC status
show status sip-entities

# Monitor SIP messages in real time
traceSBC

# Check active sessions
show sessions

# View trunk status
show sip-entities
```

### 9.3 Diagnostic Commands (AudioCodes Mediant)

```
# Via Web GUI: Monitor → SIP Calls
# Check Proxy Set status: Setup → Signaling & Media → Proxy Sets

# CLI – Check active calls:
show voip calls active

# CLI – SIP trace:
debug record stop
debug record sip
debug record start
```

### 9.4 IP Office Diagnostic

- **IP Office System Status Application (SSA):** Check SIP trunk line state (Idle / Active / Fault).
- **IP Office Monitor:** Enable SIP tracing to capture SIP INVITE/REGISTER messages.

---

## 10. Troubleshooting Guide

### 10.1 No Dial Tone / SIP Registration Failure

| Symptom | Likely Cause | Resolution |
|---------|-------------|------------|
| SBC cannot reach STC proxy | Firewall blocking UDP 5060 | Check FW rule, test with `netcat` or `nmap` |
| 403 Forbidden from STC | Incorrect credentials or source IP not whitelisted by STC | Verify auth details with STC; confirm source IP |
| 407 Proxy Authentication Required | STC requires registration auth; credentials wrong | Update SIP credentials in SBC |
| 408 Request Timeout | Network latency or STC proxy unreachable | Check routing, MTU (1500), and STC proxy status |
| SBC not registering | Wrong proxy IP/port | Recheck STC-provided proxy IP and port |

### 10.2 One-Way Audio

| Symptom | Likely Cause | Resolution |
|---------|-------------|------------|
| Audio from IP Office only | STC cannot send RTP to SBC | Check inbound FW rule for RTP 49152–65535 |
| Audio from STC only | IP Office cannot receive RTP | Check SBCE media interface, IP Office RTP ports |
| No audio at all | SRTP mismatch | Disable SRTP on SBC if STC does not support it |
| SIP ALG interference | SIP ALG modifying SDP | Disable SIP ALG on firewall |

### 10.3 Call Drops After 30/60 Seconds

| Symptom | Likely Cause | Resolution |
|---------|-------------|------------|
| Call drops at ~32s | SBC not handling 200 OK re-INVITE | Enable SIP UPDATE/re-INVITE pass-through |
| Call drops at session timer | Session timer not refreshed | Configure Session-Expires and Min-SE in SBC |
| NAT timeout | NAT mapping expires | Enable SIP OPTIONS keep-alive on SBC |

### 10.4 DTMF Not Working in IVR

| Symptom | Likely Cause | Resolution |
|---------|-------------|------------|
| No DTMF in auto-attendant | Codec mismatch (in-band DTMF vs RFC 2833) | Set DTMF mode to RFC 2833 in SBC and IP Office |
| DTMF garbled | RTP payload type mismatch | Ensure payload type 101 for RFC 2833 on both ends |

### 10.5 Inbound Calls Not Routing Correctly

| Symptom | Likely Cause | Resolution |
|---------|-------------|------------|
| Inbound DID rings wrong extension | IP Office short code/DID mapping wrong | Recheck IP Office incoming call routing table |
| All inbound goes to reception | DID not configured in IP Office | Add DID entry in IP Office Line → SIP Channels |
| No inbound at all | SBC not forwarding to IP Office | Check SBC routing rule from SIPInterface_STC to IP Office |

---

*End of STC SIP Trunk Configuration Guide*

*[YOUR COMPANY NAME] | Confidential | PROP-2026-AVAYA-001-STC*

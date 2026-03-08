# Project Implementation Timeline
## Avaya IP Office Server Edition R12.x Deployment

**Proposal #:** PROP-2026-AVAYA-001  
**Date:** March 7, 2026  
**Project Duration:** 14 Weeks (approx. 3.5 months)  
**Start Date:** [TBD – Upon PO receipt]  
**Estimated Go-Live:** [TBD – ~14 weeks from start]  
**Prepared by:** [YOUR COMPANY NAME]  
**Prepared for:** [CUSTOMER NAME]

---

## Summary

| Phase | Weeks | Description |
|-------|-------|-------------|
| Phase 1 | 1–2 | Project Kick-off & Design |
| Phase 2 | 3–5 | Procurement & Hardware Delivery |
| Phase 3 | 5–7 | Lab Build, Testing & Configuration |
| Phase 4 | 6–8 | Site Preparation |
| Phase 5 | 8–11 | On-Site Installation |
| Phase 6 | 11–13 | User Acceptance Testing & Training |
| Phase 7 | 13–14 | Go-Live, Cutover & Hypercare |
| Hypercare | 14+ | 30-Day Post-Go-Live Support |

---

## Detailed Week-by-Week Plan

| Week | Phase | Activity | Owner | Deliverable |
|------|-------|----------|-------|-------------|
| **Week 1** | Kick-off | Project kick-off meeting | PM + Customer | Meeting minutes, project charter |
| **Week 1** | Kick-off | Appoint customer project sponsor and technical lead | Customer | Named contacts confirmed |
| **Week 1** | Kick-off | Confirm and sign scope of work | PM + Customer | Signed SOW |
| **Week 1** | Design | Site survey – Building A and Building B | Technical Lead | Site survey report |
| **Week 1** | Design | Confirm IP address plan, VLAN design, QoS policy | Network Engineer | IP/VLAN design document |
| **Week 2** | Design | Finalize dial plan and extension numbering scheme | Technical Lead | Dial plan document |
| **Week 2** | Design | Confirm IVR / auto-attendant call flow with customer | Technical Lead + Customer | IVR design sign-off |
| **Week 2** | Design | STC engagement – submit SBC/SIP trunk requirements | PM | STC provisioning request submitted |
| **Week 2** | Design | Design review and customer sign-off | PM + Customer | Design sign-off document |
| **Week 3** | Procurement | Raise purchase order for server hardware | PM | PO issued |
| **Week 3** | Procurement | Raise purchase order for IP500 V2 controllers and cards | PM | PO issued |
| **Week 3** | Procurement | Raise purchase order for IP phones (J-Series) | PM | PO issued |
| **Week 3** | Procurement | Raise purchase order for Avaya SBCE / AudioCodes SBC | PM | PO issued |
| **Week 3** | Procurement | Raise purchase order for PoE switches (if required) | PM | PO issued |
| **Week 4** | Procurement | Server hardware delivered to warehouse | Logistics | Delivery confirmation |
| **Week 4** | Procurement | Avaya SBCE / SBC hardware delivered | Logistics | Delivery confirmation |
| **Week 5** | Procurement | IP500 V2 units and analog cards delivered | Logistics | Delivery confirmation |
| **Week 5** | Procurement | IP phones (J-Series) batch 1 delivered | Logistics | Delivery confirmation |
| **Week 5** | Lab Build | Server RAID, OS, and Avaya IP Office installation in lab | Engineer | Lab server running |
| **Week 6** | Lab Build | Avaya SBCE installation and initial SIP configuration | Engineer | SBC lab build complete |
| **Week 6** | Lab Build | IP500 V2 units configured (expansion, analog cards) | Engineer | IP500 V2 lab build complete |
| **Week 6** | Lab Build | IP phone template configuration (J-Series firmware, DHCP Option 176) | Engineer | Phone template created |
| **Week 6** | Site Prep | VLAN, QoS, DHCP Option 176 configured on switches | Network Engineer | Network ready for phones |
| **Week 7** | Lab Build | End-to-end lab test: IP phone registration, call flow, voicemail | Engineer | Lab test report |
| **Week 7** | Lab Build | STC SIP trunk integration (if STC has provisioned by this time) | Engineer | STC trunk test |
| **Week 7** | Site Prep | Rack installation – Building A server room | Engineer | Rack ready |
| **Week 7** | Site Prep | Rack installation – Building B comms room | Engineer | Rack ready |
| **Week 8** | Site Prep | Confirm fiber link operational and tested (Bldg A ↔ Bldg B) | Network Engineer | Fiber test results |
| **Week 8** | Site Prep | PoE switch installation – Building A access layer | Network Engineer | Switches live |
| **Week 8** | Installation | Server hardware installed in Building A rack | Engineer | Server racked and powered |
| **Week 9** | Installation | Avaya IP Office Server Edition installed and configured on server | Engineer | IP Office server live |
| **Week 9** | Installation | Avaya SBCE installed and connected (firewall/DMZ) | Engineer | SBC live |
| **Week 9** | Installation | IP500 V2 #1 installed – Building A (SCN to server via LAN) | Engineer | IP500 V2 #1 live |
| **Week 9** | Installation | Analog extensions patched to IP500 V2 #1 – Building A (30 ports) | Engineer | Analog extensions live Bldg A |
| **Week 10** | Installation | PoE switch installation – Building B access layer | Network Engineer | Switches live |
| **Week 10** | Installation | IP500 V2 #2 installed – Building B (SCN over fiber) | Engineer | IP500 V2 #2 live |
| **Week 10** | Installation | Analog extensions patched to IP500 V2 #2 – Building B (30 ports) | Engineer | Analog extensions live Bldg B |
| **Week 10** | Installation | IP phone batch 1 deployment – Building A (250 phones) | Field Team | 250 phones registered |
| **Week 11** | Installation | IP phone batch 2 deployment – Building A (250 phones) | Field Team | 500 phones registered Bldg A |
| **Week 11** | Installation | IP phone batch 3 deployment – Building B (250 phones) | Field Team | 250 phones registered |
| **Week 11** | Installation | IP phone batch 4 deployment – Building B (250 phones) | Field Team | 500 phones registered Bldg B |
| **Week 11** | Installation | STC SIP trunk final provisioning and testing | Engineer + STC | STC trunk live |
| **Week 11** | Installation | Voicemail Pro configuration – all mailboxes, auto-attendant | Engineer | Voicemail live |
| **Week 12** | UAT | User acceptance testing – Building A internal calls | Customer + Engineer | UAT sign-off Bldg A |
| **Week 12** | UAT | User acceptance testing – Building B internal calls | Customer + Engineer | UAT sign-off Bldg B |
| **Week 12** | UAT | Inter-building call testing (Bldg A ↔ Bldg B) | Customer + Engineer | Inter-building confirmed |
| **Week 12** | UAT | Outbound/inbound SIP trunk (STC) testing | Customer + Engineer | STC trunk confirmed |
| **Week 12** | UAT | Voicemail, auto-attendant, hunt groups testing | Customer + Engineer | Voicemail confirmed |
| **Week 12** | UAT | Survivability test – Building B fiber disconnect simulation | Customer + Engineer | Survivability confirmed |
| **Week 13** | Training | End-user training – Session 1 (Building A, up to 20 users) | Trainer | Training delivered |
| **Week 13** | Training | End-user training – Session 2 (Building A, up to 20 users) | Trainer | Training delivered |
| **Week 13** | Training | End-user training – Session 3 (Building B, up to 20 users) | Trainer | Training delivered |
| **Week 13** | Training | End-user training – Session 4 (Building B, up to 20 users) | Trainer | Training delivered |
| **Week 13** | Training | End-user training – Session 5 (Mixed/Overflow) | Trainer | Training delivered |
| **Week 13** | Training | Administrator training – 2-day advanced session | Trainer | Admin training delivered |
| **Week 14** | Go-Live | Final pre-cutover checklist review | PM + Customer | Checklist signed off |
| **Week 14** | Go-Live | Weekend cutover – analog and IP phones go live on new system | PM + Engineer | All phones live on Avaya |
| **Week 14** | Go-Live | Day-1 monitoring and issue resolution | Engineer on-site | Issues resolved |
| **Week 14** | Go-Live | As-built documentation handover | Technical Lead | As-built docs delivered |
| **Week 14** | Hypercare | 30-day post-go-live hypercare support begins | Support Team | Hypercare period active |
| **Week 18** | Closure | 30-day hypercare period ends; formal project closure | PM + Customer | Project closure sign-off |

---

## Key Milestones

| Milestone | Target Week | Criteria |
|-----------|------------|---------|
| Design sign-off | Week 2 | Customer approves dial plan, IVR, IP/VLAN design |
| Hardware delivery complete | Week 5 | All equipment received |
| Lab build complete | Week 7 | All components tested in lab |
| Site preparation complete | Week 8 | Racks, cabling, switches ready |
| Building A phones live | Week 11 | All 500 Building A phones registered |
| Building B phones live | Week 11 | All 500 Building B phones registered |
| STC trunk live | Week 11 | 100-channel SIP trunk active |
| UAT complete | Week 12 | Customer signs UAT acceptance |
| Training complete | Week 13 | All training sessions delivered |
| **GO-LIVE** | **Week 14** | **Full system operational** |
| Project closure | Week 18 | Hypercare complete; project signed off |

---

## Risk Register

| # | Risk | Probability | Impact | Mitigation |
|---|------|------------|--------|-----------|
| 1 | STC provisioning delay | Medium | High | Engage STC in Week 2; maintain parallel PSTN backup option |
| 2 | Hardware delivery delay | Low | High | Order early (Week 3); identify alternative suppliers |
| 3 | Fiber link failure between buildings | Low | High | Test fiber in Week 8; implement VRRP/redundant path |
| 4 | IP phone compatibility issues | Low | Medium | Lab test firmware before deployment; use latest certified firmware |
| 5 | Customer-side network not ready (VLAN/QoS) | Medium | High | Include network pre-check in Week 1 site survey |
| 6 | Customer resource unavailability for UAT | Medium | Medium | Agree UAT dates with customer sponsor in Week 2 |
| 7 | SIP ALG on customer firewall causing issues | Medium | Medium | Disable SIP ALG in Week 6 network prep; verify in lab |

---

*[YOUR COMPANY NAME] | Project Timeline | PROP-2026-AVAYA-001 | Confidential*

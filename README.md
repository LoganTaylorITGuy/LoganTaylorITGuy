# Hi, I'm Logan 👋

IT infrastructure and security pro with 12+ years in IT and 15+ years in leadership, who builds the tools his team runs on. Based in the Texas Panhandle (Amarillo / Hereford). U.S. Marine Corps veteran.

Most of my development work lives in private company repos, so here's what I've been building.

## Featured

| Project | What it is | |
|---|---|---|
| **[MSP Operations Dashboard](https://github.com/LoganTaylorITGuy/msp-ops-dashboard)** · [**▶ live demo**](https://logantayloritguy.github.io/msp-ops-dashboard/) | React + TypeScript + Tailwind dashboard with hand-built accessible SVG charts. axe-tested in a real browser (light/dark, desktop/phone), deployed by CI. | Open source |
| **[M365 Admin Toolkit](https://github.com/LoganTaylorITGuy/m365-admin-toolkit)** | PowerShell + Microsoft Graph module for offboarding, stale-account audit, MFA risk, and license waste. 30 Pester tests, CI. | Open source |
| **[SharePoint Report Publisher](https://github.com/LoganTaylorITGuy/sharepoint-report-publisher)** | Python CLI that turns a time-tracking export into a weekly effort report and publishes it to SharePoint via Graph, with least-privilege `Sites.Selected` auth. 63 tests, strict typing, CI. | Open source |
| **[NetSuite ↔ Microsoft 365 Sync](case-studies/netsuite-m365-sync.md)** | Two-way email and calendar sync middleware (Node, Graph change notifications, NetSuite OAuth 2.0). Includes five real incidents I debugged. | Case study |
| **[Pulse: Desktop Time Capture](case-studies/pulse-desktop-time-capture.md)** | Menu-bar macOS app (Tauri / Rust) with idle detection, offline queue, Keychain pairing, and signed auto-updates. 13 releases in two weeks. | Case study |

## What I've built

**Internal operations platform** (Python, Flask, SQLAlchemy, Gunicorn, Jinja)
- Ticketing, timekeeping, and agile dev-cycle tracking for a managed services team
- Integrations with QuickBooks Online, Microsoft Graph/SharePoint, GitHub, Ubiquiti UniFi, and Motive
- RMM abstraction layer with swappable vendor adapters
- Automated weekly reporting to SharePoint via an Azure App Registration and the Graph API ([open-source version](https://github.com/LoganTaylorITGuy/sharepoint-report-publisher))
- pytest suite at 80% coverage, run in GitHub Actions CI

**NetSuite development** (SuiteScript, SDF / SuiteCloud CLI, SuiteTalk REST)
- Custom Center Tab SuiteApp built with SDF, taken through multi-pass code review (permission hardening, credential handling, script ID conventions)
- Outlook and NetSuite integration with Power Automate and SuiteTalk REST: email logging, shared mailbox support, and two-way calendar sync, built in-house to replace a paid SuiteApp

**Security automation** (PowerShell)
- SharePoint phishing hunter script and Microsoft 365 identity and offboarding SOPs

**Desktop and front end** (Rust / Tauri, HTML/CSS/JS, React, Tailwind)
- Accessible operations dashboard with hand-built SVG charts, keyboard navigation and table views ([live demo](https://logantayloritguy.github.io/msp-ops-dashboard/))
- macOS menu-bar time-capture client with signed auto-updates and a CI release pipeline ([case study](case-studies/pulse-desktop-time-capture.md))
- NetSuite ↔ Outlook two-way sync middleware ([case study](case-studies/netsuite-m365-sync.md))

## Tools I work with

`Python` `Flask` `SQLAlchemy` `PowerShell` `Power Automate` `NetSuite SuiteScript` `Node.js` `Rust` `Tauri` `React` `TypeScript` `Tailwind` `Microsoft Graph` `Intune` `Entra ID` `GitHub Actions`

## Certifications

CompTIA Security+, Network+, A+ · ISC2 Certified in Cybersecurity (CC)

## Get in touch

Open to IT infrastructure, systems, and developer roles, remote or in the Amarillo / Hereford area.
[LinkedIn](https://www.linkedin.com/in/logantheitguy/)

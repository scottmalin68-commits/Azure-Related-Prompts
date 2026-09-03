<p align="center">
  <img src="BANNER_Azure-Related-Prompts.png" width="85%" alt="Azure Related Prompts Banner">
</p>

<h1 align="center">Azure‑Related Prompt Library</h1>
<h3 align="center">By Scott Malin — Cybersecurity & Automation Architect</h3>

<p align="center">
Deterministic, audit‑ready AI prompt frameworks for Entra ID Conditional Access, Azure Policy, Group Policy, and enterprise identity governance.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Last_Updated-2026--09--03-blue?style=for-the-badge">
  <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge">
  <img src="https://img.shields.io/badge/Category-Azure_Identity-purple?style=for-the-badge">
  <img src="https://img.shields.io/badge/Type-AI_Frameworks-orange?style=for-the-badge">
  <img src="https://img.shields.io/badge/Prompts-7-lightgrey?style=for-the-badge">
</p>

---

# ⭐ Featured Prompt

### **Conditional Access Policy Analyzer (Deep‑Dive Audit + Simulation Suite).md** — v3.0.1

**Goal:** Run a deterministic, evidence‑based audit of Azure AD / Entra ID Conditional Access policies — conflicts, gaps, redundancies, precedence, coverage metrics, and optional what‑if simulation — without inventing settings or organizational context.

This is the repo’s deepest CA engine: Audit / Architect / Hardening / Simulation modes, Azure‑accurate evaluation order, and locked 11‑section output.

---

# 📘 Overview

This repository contains **Azure‑ and Active Directory‑focused AI prompt frameworks** designed for:

- Conditional Access design, auditing, hardening, and what‑if simulation
- Azure Policy and Initiative documentation from raw JSON
- Group Policy Object documentation from `Get-GPOReport` XML
- Identity governance, compliance mapping, and risk scoring
- Deterministic, repeatable reasoning for enterprise IAM workflows

These prompts support:
- Cloud security engineers
- IAM / Zero Trust architects
- Identity governance and GRC teams
- Azure and Active Directory administrators
- Audit and compliance functions

All frameworks are built for **evidence‑only reasoning**, **explicit mode triggers**, **fail‑fast input validation**, and **state‑decay protection** across long conversations.

---

# 📁 Repository Catalog

Exact filenames below. Versions reflect the 2026‑09‑03 hardening pass.

### 🔐 Conditional Access Design & Architecture

- **[Access Policy Architect — Design Generator.md](Access%20Policy%20Architect%20%E2%80%94%20Design%20Generator.md)** — v1.2.1  
  *Goal:* Generate a Zero Trust‑aligned Conditional Access architecture strictly from user‑provided facts. Question‑first gating. Architect / Auditor / CISO modes.

### 🔍 Analysis & Deep‑Dive Auditing

- **[Conditional Access Policy Analyzer (Deep‑Dive Audit + Simulation Suite).md](Conditional%20Access%20Policy%20Analyzer%20(Deep%E2%80%91Dive%20Audit%20%2B%20Simulation%20Suite).md)** — v3.0.1  
  *Goal:* Evidence‑bound CA audit with overlap/conflict detection, precedence simulation, quantitative coverage metrics, ecosystem dependency flags, and optional what‑if modeling.

### 🎛️ Simulation & What‑If Modeling

- **[Conditional Access Policy Simulator.md](Conditional%20Access%20Policy%20Simulator.md)** — v2.0.1  
  *Goal:* Simulate a specific sign‑in scenario against a CA policy set. Show match/fail path, effective controls, intended vs simulated outcome, and minimal safe adjustments.

### 🛡️ Hardening & Risk Reduction

- **[Conditional Access Hardening Advisor.md](Conditional%20Access%20Hardening%20Advisor.md)** — v1.4.1  
  *Goal:* Compare an existing CA estate to Microsoft Zero Trust / identity baselines. Gap analysis, conflict and naming hygiene, exclusion risk, break‑glass review, maturity score, and a 30‑60‑90 roadmap.

### 📝 Documentation & Governance

- **[Conditional Access Documentation Generator.md](Conditional%20Access%20Documentation%20Generator.md)** — v1.0.1  
  *Goal:* Convert one or more Entra ID CA policies into audit‑ready documentation: purpose, scope, IF/THEN logic, diagrams, risk, exceptions, ownership, and change history.

- **[Azure Policy Documentation Generator.md](Azure%20Policy%20Documentation%20Generator.md)** — v1.3.1  
  *Goal:* Transform Azure Policy or Initiative JSON into governance‑grade docs with parameter/effect breakdown, compliance mapping, complexity/risk scoring, initiative aggregation, DIFF, and REWRITE modes.

- **[Group Policy Object (GPO) Documentation Generator.md](Group%20Policy%20Object%20(GPO)%20Documentation%20Generator.md)** — v1.1.1  
  *Goal:* Transform `Get-GPOReport` XML into auditable GPO documentation: links, filters, Computer/User settings, preferences, delegation, compliance mapping, and deterministic risk/complexity scores.

### 📄 Repo Files

- **LICENSE**
- **README.md** (this file)
- **BANNER_Azure-Related-Prompts.png**

---

# 🛠️ Shared Operating Rules (All Prompts)

Every prompt in this library now shares the same governance layer:

| Control | Behavior |
|---|---|
| Evidence only | No invented policies, owners, settings, frameworks, or org details |
| Input validation | Fail fast on garbage, malformed JSON/XML, or missing required fields |
| Scope lock | Jailbreak / off‑topic requests are refused with a fixed error string |
| Mode triggers | Explicit tags or defaults (never silent mode mixing) |
| State‑decay lock | Mandatory header and fixed output template on every turn |
| Format fallback | Markdown tables/headers required; fall back to structured bullets, never unstructured prose |
| Scoring | Where scoring exists, formulas and bands are explicit and capped |

Use these as drop‑in system prompts. Paste the file, then supply the policy JSON, CA export, sign‑in scenario, or GPO XML.

---

# 📅 Version History / Changelog

### **v1.4 — 2026‑09‑03**
- Hardened all seven prompt frameworks for anti‑hallucination, jailbreak/garbage handling, mode triggers, and multi‑turn state lock
- **Access Policy Architect** → v1.2.1 (platform matrix, persona trigger lock, state‑preservation header)
- **CA Policy Analyzer** → v3.0.1 (tooling inventory, conflict‑resolution hierarchy, simulation trigger math, template lock)
- **CA Policy Simulator** → v2.0.1 (engine list, precedence math, 8‑section rigid template)
- **CA Hardening Advisor** → v1.4.1 (engine ranking refresh, Strict/Verbose/Training triggers, 12‑section lock)
- **CA Documentation Generator** → v1.0.1 (single vs multi‑policy triggers, TBD/open‑items discipline)
- **Azure Policy Documentation Generator** → v1.3.1 (JSON validation, initiative rules, scoring anchors)
- **GPO Documentation Generator** → v1.1.1 (XML validation, large‑GPO grouping, separate GPO vs doc changelogs)
- README catalog expanded to include Azure Policy and GPO generators; featured prompt filename corrected

### **v1.3 — January 2026**
- Added Cyber Blue banner
- Unified README structure
- Added goal statements for listed prompts
- Added featured prompt
- Standardized cross‑repo navigation

---

# 🔗 Cross‑Repo Navigation

- 🛡️ **Cybersecurity Prompts**  
  https://github.com/scottmalin68-commits/Cybersecurity-Prompts

- 🧰 **PowerShell Security & Automation Toolkit**  
  https://github.com/scottmalin68-commits/Powershell_Scripts

- 🧩 **Misc AI Prompt Library**  
  https://github.com/scottmalin68-commits/Misc-AI-Prompts

- 🎮 **Cybersecurity Learning Prompts**  
  https://github.com/scottmalin68-commits/Cybersecurity-Learning-Prompts

- 🧭 **GitHub Profile**  
  https://github.com/scottmalin68-commits

---

# 📜 License
MIT License — see `LICENSE` for details.

TITLE: Group Policy Object (GPO) Documentation Generator
VERSION: 1.1
AUTHOR: Scott M
LAST UPDATED: 2026-01-29
============================================================
SECTION 1 — GOAL
============================================================
Your goal is to generate governance-grade, auditable documentation for a Windows Group Policy Object (GPO) from its exported report XML. Transform the raw GPO report XML into structured, deterministic documentation suitable for AD admins, security teams, compliance auditors, and governance boards.

You must:
- Explain GPO purpose, settings, linking, and enforcement intent
- Break down Computer/User configurations, preferences, links, filters, and security
- Document operational considerations, inheritance, delegation, and change management
- Map to compliance frameworks where clearly aligned
- Score documentation quality, risk, and complexity
- Support DIFF and REWRITE modes
- Include metadata, versioning, and changelog

You must not:
- Modify the GPO XML or infer settings not present
- Generate documentation without a GPO owner/author
============================================================
SECTION 2 — MODES & INPUT
============================================================
Modes: FULL (default), SUMMARY, TECHNICAL, DIFF, REWRITE (same rules as previous generators; DIFF compares settings, links, filters, permissions, etc.)

REQUIRED INPUT
- GPO_REPORT_XML (full XML from Get-GPOReport -ReportType Xml; or OLD/NEW for DIFF)
- GPO_AUTHOR (required — e.g., admin who owns/maintains it)
Optional:
- EXISTING_DOC
- OUTPUT_FORMAT ("markdown" default, "html" allowed)
- USER_COMPLIANCE_MAPPINGS (table/list of known mappings, e.g., to CIS Windows, NIST)
- GPO_LINK_CONTEXT (optional: additional notes on linked OUs/sites/domain or effective precedence)

If GPO_AUTHOR missing → stop and request it.
If GPO_REPORT_XML invalid/malformed/not a GPO report → stop with error.
============================================================
SECTION 2.1 — INPUT VALIDATION (MUST BE FIRST STEP)
============================================================
1. Confirm XML is well-formed and has root <GPO> element.
2. Check for expected children: <Name>, <GUID>, <Domain>, <CreatedTime>, <ModifiedTime>, <Computer> and/or <User>, <LinksTo>, <SecurityDescriptor>, <WMIFilter> (optional), <ExtensionData> for settings.
3. Note common namespace: xmlns="http://www.microsoft.com/GroupPolicy/Settings" (default); extensions often use dynamic q1/q2/... namespaces (e.g., for Security, Registry, Preferences).
If invalid, missing core elements, or not recognizable as GPO report → respond ONLY with:
"Invalid GPO report XML provided. Ensure it's from Get-GPOReport -Name 'YourGPO' -ReportType Xml (or -All). Provide valid XML and try again."
Do not generate documentation from invalid input.
============================================================
SECTION 3 — DOCUMENTATION STRUCTURE (STRICT)
============================================================
For large/bloated GPOs (>50 enabled settings, many ExtensionData entries, complex Preferences, or heavy WMI targeting):
- Include this note after title/version:
  **Recommendation:** For complex or bloated GPOs (>50 settings or many extensions/preferences), consider using MODE: SUMMARY first for an executive overview before generating the full detailed documentation.

1. GPO Overview (Name, GUID, Domain, Created/Modified Times, Version, Status)
2. Purpose & Intent
3. Scope & Linking
   - List all <LinksTo> with SOMPath, Order, Enforced (Yes/No)
   - Note inheritance/blocking status if known from context
   - Potential precedence/conflicts (e.g., higher-linked GPOs may override)
4. WMI Filters & Security Filtering
   - WMI filter query if present
   - Security filtering groups/users/computers (flag broad ones)
5. Computer Configuration Settings
   - Summarize enabled policies by category (Security, Administrative Templates, etc.)
   - Highlight key/risky settings
6. User Configuration Settings
   - Same as above for User section
7. Preferences & Extensions
   - Item-level targeting details (grouping, conditions)
   - Extensions (e.g., Drive Maps, Shortcuts, Registry, Files/Folders)
   - Flag legacy (e.g., IEM) or complex targeting
8. Delegation & Permissions
   - Who has Edit/Create/Delete/Apply permissions
   - Flag excessive/broad delegation
9. Operational Guidance
   - Refresh interval considerations, gpupdate behavior
   - Troubleshooting tips (e.g., why settings may not apply)
10. Known Limitations & Conflicts
    - Potential inheritance issues, filter performance impact
11. Compliance Mapping
    - Table: Framework | Control ID | Control Name | Rationale
12. Risk Scoring
13. GPO Complexity Scoring
14. Versioning & GPO Changelog
    - Cross-reference GPO's internal <Version>, <CreatedTime>, <ModifiedTime>
15. Appendix (Sample RSOP notes, related GPOs, raw snippets if helpful)
16. Documentation Metadata
17. Documentation Changelog
============================================================
SECTION 4–6 — SCORING MODELS
============================================================
Documentation Quality: (Unchanged — weighted Completeness/Clarity/Readiness)

Severity Model — GPO-specific additions:
Critical:
- Missing purpose/intent
- Broad security filtering (e.g., "Authenticated Users", "Everyone", "Domain Users" without restriction)
- Excessive delegation (e.g., non-admins with Edit/Delete)
- Modified "Default Domain Policy" or "Default Domain Controllers Policy"
High:
- WMI filters on high-volume OUs (performance risk)
- Legacy extensions (IEM, old Preferences vulnerable to elevation)
- Unenforced critical security settings
- Many broad permissions/groups in filtering
Medium/Low/Informational: (Unchanged, plus notes on minor conflicts)

Risk Scoring: (Unchanged weights, cap 100; now factors GPO-specific severity)

GPO Complexity Scoring (0–10):
Objective anchors (additive, ±1 nuance):
- Base: 0
- Number of enabled settings/policies: +1 per major category (Security, Admin Templates, Preferences, etc.); 10+ = +2–3
- Links/SOMs: 1–2 = +0, 3–5 = +1, 6+ = +2
- WMI filter present/complex: +2 (simple) to +3 (complex query)
- Preferences item-level targeting: +1 per layer/grouping (max +3)
- Multiple scripts/preferences/extensions: +1–2
- Security filtering groups >5 or complex: +1–2
- Legacy elements (IEM, old CSEs): +2
Bands: 0–2 Simple, 3–5 Moderate, 6–8 Complex, 9–10 Highly Complex
============================================================
SECTION 7 — COMPLIANCE MAPPING
============================================================
Supported frameworks: NIST 800-53, CIS Windows Benchmarks, ISO 27001, PCI-DSS, etc.
Only map if settings clearly align (e.g., password policy → AC-7, audit → AU family)
Use table format.
Incorporate USER_COMPLIANCE_MAPPINGS if provided; note "User-provided mapping included".
============================================================
SECTION 8 — RULES
============================================================
- Validate XML first (Section 2.1 — fail fast)
- Handle namespaces: Use default "http://www.microsoft.com/GroupPolicy/Settings"; for extensions, account for dynamic q1/q2/... (e.g., via namespace manager in mental model); if extraction unclear due to ns, mark as “Unknown (namespace issue)” and suggest user provide simplified XML or details.
- Do NOT modify XML or infer undocumented settings
- Mark unclear/incomplete as “Unknown”
- Documentation must always include: GPO author, doc version, changelog
- Security flagging: Explicitly call out:
  - Broad/insecure filtering (Authenticated Users/Everyone without deny overrides)
  - Legacy Preferences/IEM (vulnerable)
  - WMI performance risks
  - Delegation allowing non-admins Edit/Delete
  - Modified default policies
  - Unenforced high-impact settings (e.g., no password complexity enforced)
- For large/complex GPOs: Prioritize key/risky settings in summaries; use recommendation note
- GPO Changelog: Document changes to GPO itself (from XML metadata); separate from Documentation Changelog
============================================================
SECTION 9 — VERSIONING & CHANGELOG
============================================================
(Unchanged independent rules; bump minor if GPO XML changed, e.g., settings/links modified)

CHANGELOG:
- 1.1 — Hardened for real-world GPOs: Added namespace handling guidance, large-GPO recommendation (>50 settings), GPO-specific severity/risk additions (broad filtering, WMI perf, legacy prefs, default policy mods), refined complexity anchors (Preferences targeting, filtering groups), improved linking precedence notes, explicit security flagging rules
- 1.0 — Initial creation, modeled after Azure Policy v1.3 & Script v1.2
STATUS: Hardened, governance-ready for enterprise AD environments
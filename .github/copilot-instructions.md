# Copilot instructions for Microsoft Root Program requirements repository

Purpose
- This repository is the single source-of-truth for the Microsoft Trusted Root Program requirements. The authoritative policy text lives in `Requirements.md`; `README.md` explains the repo structure and `Changelog.md` tracks published versions.

Quick orientation (what to read first)
1. Read `README.md` to understand the project intent and update process.  
2. Read `Requirements.md` top-to-bottom to understand the policy language, sectioning, and normative statements.  
3. Inspect `Changelog.md` for how versions are recorded and sample entries.

Primary workflows an agent should follow
- Changes are made via GitHub pull requests. Create a single PR that updates the policy text and any supporting artifacts (changelog, templates).  
- Every normative change must include: the exact text change, a short rationale, relevant external references (links to CAB Forum, WebTrust/ETSI, CCADB pages, or aka.ms docs), and a changelog entry.
- For policy changes that affect audit or program behavior, add the Program contact in the PR description and include a request for explicit Program-team sign-off: msroot@microsoft.com.

Repository conventions and style (concrete, discoverable rules)
- Maintain the existing numbered section style (e.g., 3.1.1, 3.1.2). Insert new clauses by appending the next number in the same subsection.
- Preserve the `[TOC]` placeholder at the top of `Requirements.md` and keep the main headings (Introduction, Program Participation, Program Technical Requirements, Audit requirements).
- Use Markdown tables for enumerations (e.g., OID lists, key size tables). When adding a new row, match the existing header and column alignment.
- Write normative statements succinctly and in active voice. Avoid speculative or aspirational wording; the repo contains discoverable, enforceable rules.

Examples (copy/paste-ready)
- Add a new OID row to the OID table in `Requirements.md`:

  | Policy | OID | 
  | --- | --- |
  | New Policy Example | 1.2.3.4.5.6 |

- Changelog entry example (append to `Changelog.md`):
  | 1.1 | YYYY-MM-DD | Short summary: "Added requirement X to Section 3.1" |

PR checklist (what must be present before merging)
- [ ] Updated `Requirements.md` with the final wording and section number(s)
- [ ] Added or updated `Changelog.md` with version, date, and short summary
- [ ] Provided a short rationale and authoritative reference link(s) in the PR body
- [ ] Marked Program-team reviewers and, for program-affecting changes, requested msroot@microsoft.com sign-off
- [ ] Verified Markdown renders correctly locally (preview links and tables)

Integration points and external systems to be aware of
- CCADB: audit attestations and PKI disclosures live outside this repo. Changes that affect CCADB-related processes should include instructions / links pointing to CCADB guidance (https://ccadb.org).
- Audit references (WebTrust / ETSI) and `aka.ms` link targets should be kept current; update links when authoritative URLs change.

Compliance & Audit (mandatory steps for audit-related changes)
- If a change affects Audit Requirements, include a clear summary of the **audit impact** in the PR body and the proposed text change in `Requirements.md`.
- Required attachments and checks for audit-affecting PRs:
  - State whether the change requires a new or updated Qualifying Audit and which standard applies (WebTrust, ETSI, or Equivalent Audit).
  - If CCADB actions are required, describe the exact CCADB updates (audit upload, attestation entries) and the responsible party.
  - Provide exact attestation wording examples (e.g., "This change updates the Audit Requirements in Section 4.1 to require [X]. Rationale: aligns with EN 319 411-2 updates. Reference: https://aka.ms/auditreqs.")
  - Add explicit next steps and timelines (who will contact CCADB/auditor and expected timing).
- Program-team sign-off: **msroot@microsoft.com** must be included as a reviewer for all audit-affecting PRs.
- Use the **Audit submission** issue template (`.github/ISSUE_TEMPLATE/audit-submission.md`) to notify the Program team, capture attestation wording and CCADB actions, and link the resulting issue number in your PR. See example workflow in `.github/examples/example-audit-issue.md` and `.github/examples/example-audit-pr.md` for a filled sample of the issue + PR flow.

What NOT to do (discovered constraints)
- Do not add operational or private audit artifacts (PDFs, attestations) into this repo — audit artifacts are managed externally via CCADB or the CA/auditor workflows.
- Do not change contact email addresses or contract-level language without Program-team approval.

When in doubt
- If a change could materially affect how CAs operate or how Microsoft products trust certificates, flag the PR as requiring Program-team sign-off and include msroot@microsoft.com in the request.

Feedback
- If anything here is unclear or missing, leave a comment on this PR or open an issue and tag the repository owners so we can iterate on these instructions.

PR templates & examples
- **Sample PR titles**:
  - `REQ: Update Section 3.1.6 Key Usage wording — rationale: clarify OCSP signing`
  - `ADD: New OID 1.2.3.4.5.6 — Section 3.1.15`
  - `CHG: Relax RSA key-size wording in Section 3.1.20 (audit: WebTrust change)`

- **PR body template (copy/paste)**:
  ```
  Summary:
  - Short summary of change and the exact section(s) modified (e.g., 3.1.20).

  Rationale:
  - One or two sentences explaining why this change is required.

  References:
  - Links to authoritative sources (CABForum, WebTrust, ETSI, CCADB, aka.ms links).

  Changelog:
  - Proposed Changelog.md entry line (version | YYYY-MM-DD | Short summary).

  Program reviewers:
  - List Program-team contacts (e.g., msroot@microsoft.com) if the change affects audit, trust, or operations.
  ```

- **Audit-update wording example**:
  - `This change updates the Audit Requirements in Section 4.1 to require [X]. Rationale: aligns with EN 319 411-2 updates. Reference: https://aka.ms/auditreqs.`

- **Changelog example (append exactly as a table row)**:
  | 1.1 | YYYY-MM-DD | Short summary: "Added requirement X to Section 3.1" |

Notes & verification
- Always preview Markdown locally (GitHub rendering) and verify table alignment.
- If the change affects external systems (CCADB, WebTrust filings), include explicit next-steps in PR (who will contact CCADB/auditor, expected timing).

---
(Generated: guidance to help AI agents be productive in this docs-first repository)
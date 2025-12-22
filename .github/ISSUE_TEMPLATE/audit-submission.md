---
name: Audit submission
about: Use this template to notify the Program team of an audit update, provide attestation wording and CCADB actions, and link the related PR.
title: "[Audit] {CA name} - Audit submission - {YYYY-MM-DD}"
labels: audit, triage
assignees: msroot@microsoft.com
---

## Summary
- Short summary of the audit update and the certificates/roots affected (e.g., "Annual WebTrust update for Root CA X").

## Affected sections / files
- Which `Requirements.md` section(s) or other files are affected (e.g., `Requirements.md` Section 4.1).

## Audit type
- [ ] WebTrust
- [ ] ETSI
- [ ] Equivalent (describe)

## Attestation wording (required)
- Provide exact wording for the attestation or the attestation letter text you expect auditors to provide. Example:
  > "This change updates the Audit Requirements in Section 4.1 to require [X]. Rationale: aligns with EN 319 411-2 updates. Reference: https://aka.ms/auditreqs."

## Attachments / Public URLs
- Attach or link to a **searchable PDF** attestation letter hosted on a public site (do NOT upload private audit PDFs into this repo). Provide the URL(s) and the auditor's published page if available.

## CCADB actions required
- Describe required CCADB updates (audit upload, attestation metadata, which fields to set) and who will perform them.

## Auditor contact
- Auditor name, organization, and email (for Microsoft verification contact).

## Changelog entry (proposed)
- Proposed `Changelog.md` line (version | YYYY-MM-DD | Short summary):
  | 1.x | YYYY-MM-DD | Short summary: "Updated Audit Requirements in Section 4.1" |

## Timelines
- Expected dates for auditor confirmation, CCADB upload, and Program sign-off.

## Related PR / Issue
- Link the PR that implements the text change and any related issues here (include PR number once created).

## Checklist
- [ ] Exact attestation wording is provided
- [ ] Searchable attestation PDF is publicly accessible and linked above
- [ ] CCADB actions are documented and an owner is named
- [ ] Program team (`msroot@microsoft.com`) is requested for sign-off
- [ ] A PR is opened and linked to this issue and includes the proposed changelog line

## Additional notes
- Any other context, roll-forward plans, or follow-up tasks.

---
*Note: This template collects public attestation metadata only. For private correspondence or files, contact the Program team via email (msroot@microsoft.com).*
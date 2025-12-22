# Example PR: Update Audit Requirements (filled)

**Title:** REQ: Update Section 4.1 Audit Requirements — require explicit WebTrust attestation for server authentication EKU

## Summary
- Updated `Requirements.md` Section 4.1 to require explicit WebTrust attestation language for server authentication EKU.

## Rationale
- Aligns Microsoft Audit Requirements with recent clarifications in EN 319 411-2 and ensures consistency with CCADB automation parsing requirements.

## Changes
- `Requirements.md`: Section 4.1 — added clause that specifies the required attestation wording and upload process.
- `Changelog.md`: appended a row proposing the change.

## References
- EN 319 411-2: https://www.etsi.org
- https://aka.ms/auditreqs

## Changelog entry
| 1.1 | 2025-12-22 | Updated Audit Requirements in Section 4.1 to require WebTrust attestation for server authentication EKU |

## Program reviewers & sign-off
- Added `msroot@microsoft.com` as a reviewer and requested explicit sign-off.

## Compliance checklist
- [x] This change affects Audit Requirements; WebTrust selected
- [x] Proposed attestation wording included in the PR body
- [x] CCADB actions documented in related issue #456 (example)
- [x] Timelines added and owner named
- [x] Audit submission issue opened: #456

## Checklist
- [x] Updated `Requirements.md` with the final wording and section number(s)
- [x] Added or updated `Changelog.md` with version, date, and short summary
- [x] Provided a short rationale and authoritative reference link(s) in the PR body
- [x] Marked Program-team reviewers and requested `msroot@microsoft.com` sign-off
- [x] Verified Markdown renders correctly (preview) and tables align

---
*This PR is an example to demonstrate the expected fields and approach for audit-related changes.*
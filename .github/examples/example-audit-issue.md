# Example: Audit submission (filled)

Title: [Audit] Contoso CA - Audit submission - 2025-12-22

## Summary
- Annual WebTrust audit update for Contoso Root CA (SHA256: ABCDEF...)

## Affected sections / files
- `Requirements.md`: Section 4.1 (Audit Requirements)

## Audit type
- [x] WebTrust

## Attestation wording (required)
- "This change updates the Audit Requirements in Section 4.1 to require explicit WebTrust attestations for server authentication EKUs. Rationale: aligns with EN 319 411-2 updates. Reference: https://aka.ms/auditreqs."

## Attachments / Public URLs
- Public attestation: https://auditor.example.org/contoso-audit-2025.pdf

## CCADB actions required
- Upload attestation to CCADB under Contoso CA entry; add SHA256 thumbprint and date. Owner: Contoso PKI team (pki@contoso.com).

## Auditor contact
- Jane Doe, AuditorOrg, jane.doe@auditor.example.org

## Changelog entry (proposed)
| 1.1 | 2025-12-22 | Updated Audit Requirements in Section 4.1 to require WebTrust attestation for server authentication EKU |

## Timelines
- Auditor confirmation: 2025-12-24
- CCADB upload: 2025-12-26
- Program sign-off requested: 2026-01-02

## Related PR / Issue
- PR: #123 (link once PR is created)

## Checklist
- [x] Exact attestation wording is provided
- [x] Searchable attestation PDF is publicly accessible and linked above
- [x] CCADB actions are documented and an owner is named
- [x] Program team (`msroot@microsoft.com`) is requested for sign-off
- [ ] A PR is opened and linked to this issue and includes the proposed changelog line

---
*This is a sample to illustrate required fields; do not upload private documents to the repo.*
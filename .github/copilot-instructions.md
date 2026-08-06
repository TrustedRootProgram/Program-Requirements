# Copilot / AI Agent Instructions — Microsoft Root Program Requirements

Purpose: give AI coding agents a compact, actionable summary so they can safely and productively edit this repository's policy documents.

Notes about the repository
- This repo is documentation-first: core content lives under `requirements/`, templates under `templates/`, and historical updates under `changelog/` (see `README.md`).
- Changes are authoritative and public: edits are published via pull requests and represent official program requirements. Preserve legal headers and contact metadata.

What you're allowed/expected to do
- Improve clarity, fix formatting, correct broken links, and update internal cross-references across markdown files.
- Propose changes to requirement wording only when you preserve the original meaning and numbering (e.g., `3.1.1.` style). When you modify substantive requirements, add a clear changelog entry in `changelog/` and a PR description summarizing intent.

What to avoid or escalate
- Do NOT alter legal or copyright statements, the program contact email, or the official external anchors (aka.ms, ccadb links) without human approval.
- Do NOT unilaterally change normative requirement thresholds (cryptographic sizes, timelines, audit rules). For any normative change, add a draft proposal PR and request human review.

Style & structural patterns (examples)
- Numbered clauses: follow the existing numbered + subsection pattern (e.g., `3.1.1. Root certificates must be x.509 v3 certificates.`). Keep numbering stable when editing.
- Tables: preserve column order and headers when editing tables (see `Requirements.md` sections with algorithm/key-size tables).
- TOC & anchors: files use a top-level TOC; update links when you add/remove section headings.

Developer workflows (discovered)
- Updates are performed through pull requests. Include a short changelog item under `changelog/` describing the change, the rationale, and the date.
- There are no build/test scripts in-repo — run local markdown linting/preview if desired, but do not add tooling without a PR explaining its purpose.

Integration & external references
- This project links to external services and authoritative resources: `https://aka.ms/rootupdates`, `https://ccadb.org`, WebTrust and ETSI references. Do not replace these with alternate URLs.

PR requirements (recommended minimal checklist for PRs)
- Title: concise + section reference (e.g., "Update 3.1.10 OCSP/CRL wording")
- Body: describe WHAT changed, WHY, and the corresponding `changelog/` entry path.
- Changelog: add a markdown file under `changelog/` following the repository's existing naming pattern (date-prefixed or section-ref).

Examples (how to edit safely)
- Small clarity fix: adjust wording inside a numbered clause but keep the clause number and technical values identical.
  - Example: change "Certificates to be added... MUST be self-signed root certificates." -> "Certificates submitted for inclusion MUST be self-signed root certificates." (keep MUST and meaning)
- Cross-reference fix: update a broken internal anchor from `#government-ca-requirements` to the exact heading text found in `Requirements.md`.

When in doubt
- Open a draft PR and request review from a human maintainer. Flag any change that affects normative text (algorithm sizes, timeframes, audit acceptance criteria) for review.

If you find other agent instruction files in the workspace, prefer merging their non-conflicting guidance here and notify maintainers in the PR.

— End of instructions —

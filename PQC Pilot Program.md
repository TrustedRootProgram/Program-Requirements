# Post-Quantum Cryptography (PQC) TLS Pilot Program Requirements V1.0

## Overview

Microsoft’s Trusted Root Program (TRP) is establishing a Post-Quantum Cryptography (PQC) TLS Pilot Program to support testing and evaluation of PQC-enabled certificate hierarchies within the Microsoft Root Program. This pilot is strictly scoped to closed testing environments, custom applications, and enterprise testbeds. Its purpose is to evaluate the impact of PQC in those environments, not to establish a standard for publicly-accessible web connections.

> [!IMPORTANT]
> Certificates issued under this pilot program:
>
> - Are **NOT** publicly trusted.
> - Are **NOT** intended for production trust scenarios.
> - Are **NOT** intended to secure public-facing web connections.
> - Will **NOT** be added to the Common CA Database (CCADB).
> - Will **NOT** be considered for public trust inclusion by Microsoft.
> - Will **NOT** be added to Certificate Transparency Logs.
> - Exist solely for interoperability testing and ecosystem-readiness purposes.

ML-DSA is currently in a limited and evolving support state with no expectation of full implementation or complete functionality across Microsoft products and libraries during this pilot. Behavior may be unstable, compatibility may change without notice, and support is not guaranteed. These capabilities should not be relied upon for production or publicly trusted scenarios.

The purpose of this pilot is to:

- Advance cryptographic agility across the ecosystem.
- Enable participating Certificate Authorities (CAs) to test PQC TLS roots and certificate issuance in a non-publicly trusted pilot environment.
- Validate interoperability with Microsoft platforms and trust infrastructure.
- Support ecosystem readiness for post-quantum cryptography adoption.

This pilot currently focuses on server authentication and client authentication scenarios only.

## Participation Requirements

To participate in the PQC TLS Pilot Program, Certificate Authorities:

- MUST be participants of and in good standing with the Microsoft Trusted Root Program.
- MAY only participate upon approval by Microsoft.

Microsoft reserves the right to deny, suspend, or remove participation at any time.

## Breakage and Compatibility Reporting Requirements

Participating CAs MUST document and report instances where PQC certificates, hierarchies, tooling, or workflows are incompatible with existing ecosystem requirements, policies, or operational processes. CAs should email msroot@microsoft.com with noted incompatibilities.

Examples MAY include:

- Common CA Database (CCADB) policy or process incompatibilities
- Baseline Requirements limitations
- Certificate Transparency logging issues
- CA software or HSM compatibility limitations
- Validation or linting failures
- TLS interoperability issues
- Root store ingestion or distribution issues
- Encoding or parsing failures in dependent systems

When incompatibilities are identified:

- Participating CAs MAY continue pilot issuance activities unless otherwise directed by Microsoft.
- Participating CAs MUST notify Microsoft of the issue.
- Participating CAs MUST provide sufficient detail for Microsoft to evaluate potential standards, policy, or process updates.
- Participating CAs SHOULD include reproducible examples, impacted systems, error conditions, and relevant requirement references when available.

The purpose of this reporting requirement is to enable Microsoft and ecosystem participants to identify areas requiring future modernization or clarification for PQC readiness.

## Supported Algorithms

### Required Algorithm

Participating CAs MUST support the following algorithm for PQC root certificates:

- **ML-DSA-87**

Algorithm implementations:

- MUST conform to published specifications.
- MUST validate successfully against applicable reference test vectors.

### Algorithm Restrictions

For this pilot:

- Root certificates MUST use ML-DSA-87.
- ML-DSA-44 and ML-DSA-65 MUST NOT be used for root certificates.
- ML-DSA-44 and ML-DSA-65 MAY be used for Subordinate CA or leaf certificates.

## Certificate Requirements

### X.509 Requirements

Certificates:

- MUST conform to applicable X.509 standards.
- MUST use proper encoding and field population.
- MUST conform to RFC 5280 requirements where applicable.

Each certificate MUST include:

- Subject distinguished name.
- Issuer distinguished name.
- Unique serial number within the PQC hierarchy.
- Public key information encoded for ML-DSA-87.

## Extended Key Usage (EKU)

PQC root certificates may be issued only for the following TLS authentication uses:

- Server Authentication
- Client Authentication
- Server Authentication combined with Client Authentication

PQC root certificates MUST include the EKU extension and MUST mark the EKU extension as critical.

The EKU extension MUST contain only the EKU OID or OIDs corresponding to the approved TLS authentication use case for that root:

- Server Authentication only: `serverAuth` (`1.3.6.1.5.5.7.3.1`)
- Client Authentication only: `clientAuth` (`1.3.6.1.5.5.7.3.2`)
- Server Authentication combined with Client Authentication:
  - `serverAuth` (`1.3.6.1.5.5.7.3.1`)
  - `clientAuth` (`1.3.6.1.5.5.7.3.2`)

The PQC TLS Pilot Program:

- MUST NOT be used for Code Signing certificates.
- MUST NOT be used for Document Signing or S/MIME certificates.
- MUST NOT be used for other non-TLS EKU use cases.

## Validity Period Requirements

The following maximum validity periods apply:

| Certificate Type | Maximum Validity |
|---|---|
| Root Certificates | 1 year |
| Subordinate CA Certificates | 1 year |
| Leaf Certificates | 90 days |

When a PQC pilot root certificate expires:

- Microsoft will remove the certificate from the Microsoft Trusted Root Program CTL.

## Compromise Procedures

If a compromise or material weakness is identified that may impact the security, integrity, or intended use of a PQC pilot certificate, hierarchy, key, algorithm, or related implementation:

- Participating CAs MUST notify affected parties as required.
- Microsoft MAY add impacted roots to the Microsoft Disallowed CTL.
- Roots added to the Microsoft Disallowed CTL MAY be removed after expiration.
- Replacement certificates MAY be required using alternate approved algorithms.

## Program Limitations

Unless otherwise approved by Microsoft:

- Participating CAs are limited to one PQC pilot root.
- Windows is the intended PQC testing platform for participating CAs.
- Additional operational, telemetry, CT logging, or reporting requirements MAY be communicated separately.

## Disclaimer
This pilot program is experimental and intended to support ecosystem readiness for PQC adoption. Participation does not guarantee future production inclusion or long-term support within the Microsoft Trusted Root Program.

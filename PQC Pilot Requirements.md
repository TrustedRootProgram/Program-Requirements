
# Post-Quantum Cryptography (PQC) TLS Pilot Program Requirements

## Overview

Microsoft’s Trusted Root Program (TRP) is establishing a Post-Quantum Cryptography (PQC) TLS Pilot Program to support testing and evaluation of PQC-enabled certificate hierarchies within the Microsoft Root Program.

> [!IMPORTANT]
> Certificates issued under this pilot program:
> - Are **NOT** publicly trusted.
> - Are **NOT** intended for production trust scenarios.
> - Will **NOT** be added to the Common CA Database (CCADB).
> - Will **NOT** be considered for public trust inclusion by Microsoft.
> - Exist solely for interoperability testing, and ecosystem-readiness purposes.

The purpose of this pilot is to:

- Advance cryptographic agility across the ecosystem.
- Enable participating Certificate Authorities (CAs) to test PQC TLS roots and certificate issuance in a non-publicly trusted pilot environment.
- Validate interoperability with Microsoft platforms and trust infrastructure.
- Support ecosystem readiness for post-quantum cryptography adoption.

This pilot currently focuses on TLS server authentication scenarios only.


## Participation Requirements

To participate in the PQC TLS Pilot Program, Certificate Authorities:

- MUST be participants of and in good standing with in the Microsoft Trusted Root Program.
- MUST remain compliant with all applicable Microsoft Trusted Root Program requirements.
- MUST maintain current audit status and responsiveness to program requirements.
- MAY only participate upon approval by Microsoft.

Microsoft reserves the right to deny, suspend, or remove participation at any time.

## Breakage and Compatibility Reporting Requirements

Participating CAs MUST document and report instances where PQC certificates, hierarchies, tooling, or workflows are incompatible with existing ecosystem requirements, policies, or operational processes. CAs should email msroot@microsoft.com with noted incompatibilities.

Examples MAY include:

- CCADB policy or process incompatibilities
- Baseline Requirements limitations
- Certificate Transparency logging issues
- CA software or HSM compatibility limitations
- Validation or linting failures
- TLS interoperability issues
- Root store ingestion or distribution issues
- Encoding or parsing failures in dependent systems

Where incompatibilities are identified:

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
- ML-DSA-44 and ML-DSA-65 MAY be used for leaf certificates.

### Reference Parameters

| Algorithm | Public Key Size | Private Key Size | Signature Size | NIST Security Level |
| --- | --- | --- | --- | --- |
| ML-DSA-44 | 1312 bytes | 2560 bytes | 2420 bytes | Level 2 |
| ML-DSA-65 | 1952 bytes | 4032 bytes | 3309 bytes | Level 3 |
| ML-DSA-87 | 2592 bytes | 4896 bytes | 4627 bytes | Level 5 |

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

PQC root certificates:

- MUST include the EKU extension.
- MUST include the following EKU:
  - Server Authentication (`1.3.6.1.5.5.7.3.1`)
- MUST mark the EKU extension as critical.

The PQC TLS Pilot Program:

- MUST NOT be used for non-server authentication scenarios.
- MUST NOT be used for Code Signing certificates.
- MUST NOT be used for Document Signing certificates.
- MUST NOT be used for Client Authentication certificates.
- MUST NOT be used for other non-TLS EKU use cases.


## Validity Period Requirements

The following maximum validity periods apply:

| Certificate Type | Maximum Validity |
| --- | --- |
| Root Certificates | 1 year |
| Subordinate CA Certificates | 1 year |
| Leaf Certificates | 1 year |

When a PQC pilot root certificate expires:

- Microsoft will remove the certificate from the Microsoft Trusted Root Program CTL.

## Compromised Algorithm Procedures

If a compromise or material weakness is identified in an approved PQC algorithm:

- Participating CAs MUST notify affected parties as required.
- Microsoft MAY add impacted roots to the Microsoft Disallowed CTL.
- Roots added to the Microsoft Disallowed CTL MAY be removed after expiration.
- Replacement certificates MAY be required using alternate approved algorithms.


## Program Limitations

Unless otherwise approved by Microsoft:

- Participating CAs are limited to one PQC pilot root.
- Windows is the intended PQC testing platform for participating CAs.
- Additional operational, telemetry, CT logging, or reporting requirements MAY be communicated separately.


### Disclaimer

This pilot program is experimental and intended to support ecosystem readiness for PQC adoption. Participation does not guarantee future production inclusion or long-term support within the Microsoft Trusted Root Program.

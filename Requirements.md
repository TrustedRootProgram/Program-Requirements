# Microsoft Root Program Requirements v1.0
 > [!NOTE]
 > * For information on the most-recent updates shipped, please see <https://aka.ms/rootupdates> 
 > * Bookmark this page as: <https://aka.ms/RootCert>

[TOC]

## 1. Introduction

The Microsoft Trusted Root Program enables customers to trust Windows products by distributing root certificates. This document outlines the **general**, **technical**, and **audit** requirements for participation.


## 2. Program Participation Requirements
### 2.1 General Obligations
**2.1.1.** Commercial CAs may not enroll a root CA into the Program that is intended to be primarily trusted internally within an organization (i.e. Enterprise CAs).

**2.1.2.** Program Participants must provide Microsoft the identities and emails of at least two "Trusted Agents" to serve as representatives to the Program and one general email alias. Program Participants must inform Microsoft upon the removal or addition of personnel as a Trusted Agent. Program Participants must agree that notice is effective when Microsoft sends an email or official letter. 

**2.1.3.** At least one of the contacts or aliases provided should be a 24/7 monitored communications channel for revocation requests or other incident management situations.

**2.1.4.** The Program Participant must disclose its full PKI hierarchy (nonlimited subordinate CA, cross-signed nonenrolled root CAs, subordinate CAs, EKUs, certificate constraints) to Microsoft on an annual basis, including certificates issued to CAs operated by external third parties.  Program Participants must keep this information accurate in the CCADB when changes occur. 

**2.1.5.** If a subordinate CA isn't publicly disclosed or audited, it must be domain-constrained. 

**2.1.6.** Program Participants must inform Microsoft via email at least 120 days before transferring ownership of enrolled root or subordinate CA that chains to an enrolled root to another entity or person.

**2.1.7.** Reason Code must be included in revocations for intermediate certificates. CAs must update the CCADB when revoking any intermediate certificates within 30 days. 

**2.1.8.** If a CA uses a subcontractor to operate any aspect of its business, the CA will assume responsibility for the subcontractor's business operations.

**2.1.9.** Program Participants must provide to Microsoft evidence of a Qualifying Audit for each root, unconstrained subordinate CA, and cross-signed certificate before conducting commercial operations and thereafter on an annual basis. See Section 4 for more details. 

**2.1.10.** Program Participants must assume responsibility to ensure that all unconstrained subordinate CAs and cross-signed certificates meet the Program Audit Requirements.

**2.1.11.** CAs must publicly disclose all audit reports for unconstrained subordinate CAs.

**2.1.12.** Program Participants agree that Microsoft may contact customers that Microsoft believes may be substantially impacted by the pending removal of a root CA from the Program. 

**2.1.13.** If Microsoft, in its sole discretion, identifies a certificate whose usage or attributes are determined to be contrary to the objectives of the Trusted Root Program or the Baseline Requirements, Microsoft will notify the responsible CA and request that it revokes the certificate. The CA must revoke the certificate within 24 hours of receiving Microsoft's notice. 

**2.1.14.**  CAs trusted by Microsoft products must comply with the most recent and applicable Baseline Requirements (BRs) for the type of certificate they issue, as defined by the CA/Browser Forum and other relevant industry bodies. This includes, but is not limited to: TLS Server Authentication Certificates – CA/Browser Forum Baseline Requirements for TLS, Code Signing Certificates – CA/Browser Forum Code Signing Baseline Requirements, S/MIME Certificates – CA/Browser Forum S/MIME Baseline Requirements. Where Microsoft policy imposes stricter requirements than the applicable BRs, CAs are expected to adhere to Microsoft’s requirements.

**2.1.15.**  No single organization, including Microsoft, has the authority to grant exceptions to the Baseline Requirements. Microsoft will not grant exceptions under any circumstances.

**2.1.16.**  TRP Participants MUST adhere to the latest version of the CCADB Policy.

**2.1.17.**  All publicly-trusted subscriber TLS certificates must be logged within 24 hours to a Certificate Transparency (CT) Log that complies with RFC 6962, "Certificate Transparency." Certificates issued must include at least two SCTs (Signed Certificate Timestamp) from distinct CT Logs that were Qualified, Usable, or ReadOnly at the time of check.  

**2.1.18.** Certificate Authorities must update their Certificate Policy (CP) and Certification Practice Statement (CPS) documents before applying any change in operations. The updated documents must be made publicly available and communicated to Microsoft. CAs should provide these updates by updating the CCADB. CAs MUST update the changelog in their CP/CPS documents with what changes were made. 



## 3. Program Technical Requirements
### 3.1. Root Requirements

**3.1.1.** Root certificates must be x.509 v3 certificates.

**3.1.2.** Certificates to be added to the Trusted Root Store MUST be self-signed root certificates. 

**3.1.3.** The CN attribute must identify the publisher and must be unique.

**3.1.4.** The CN attribute must be in a language that is appropriate for the CA's market and readable by a typical customer in that market.

**3.1.5.** Basic Constraints extension: must be cA=true.

**3.1.6.** Key Usage extension MUST be present and MUST be marked critical. Bit positions for KeyCertSign and cRLSign MUST be set. If the Root CA Private Key is used for signing OCSP responses, then the digitalSignature bit MUST be set.

**3.1.7.** Root Key Sizes must meet the requirements detailed in "Signature Requirements" below.

**3.1.8.** Newly minted Root CAs must be valid for a minimum of eight years, and a maximum of 25 years, from the date of submission.

**3.1.9.** Participating Root CAs may not issue new 1024-bit RSA certificates from roots covered by these requirements.

**3.1.10.** All issuing CA certificates must contain either a CDP extension with a valid CRL and/or an AIA extension to an OCSP responder. An end-entity certificate may contain either an AIA extension with a valid OCSP URL and/or a CDP extension pointing to a valid HTTP endpoint containing the CRL. If an AIA extension with a valid OCSP URL is NOT included, then the resulting CRL File should be <10MB. 

**3.1.11.** Private Keys and subject names must be unique per root certificate; reuse of private keys or subject names in subsequent root certificates by the same CA may result in unexpected certificate chaining issues. CAs must generate a new key and apply a new subject name when generating a new root certificate prior to distribution by Microsoft.

**3.1.12.** Government CAs must restrict server authentication to government-issued top level domains and may only issue other certificates to the ISO3166 country codes that the country has sovereign control over (see  <https://aka.ms/auditreqs> section III for the definition of a "Government CA"). These government-issued TLDs are referred to in each CA's respective contract. 

**3.1.13.** Issuing CA certificates that chain to a participating Root CA must separate Server Authentication, S/MIME, Code Signing, and Time Stamping uses. This means that a single Issuing CA must not combine server authentication with S/MIME, code signing, or time stamping EKU. A separate intermediate must be used for each use case. 

**3.1.14.** End-entity certificates must meet the requirements for algorithm type and key size for Subscriber certificates listed in Appendix A of the CAB Forum Baseline Requirements located at   https://cabforum.org/baseline-requirements-documents/.

**3.1.15.** CAs must declare one of the following policy OIDs in its Certificate Policy extension end-entity certificate: 
| Policy | OID | 
| --- | --- |
| Digest Algorithms |SHA2 (SHA256, SHA384, SHA512) | 
| DV | 2.23.140.1.2.1. |
| OV | 2.23.140.1.2.2. |
| EV | 2.23.140.1.1. |
| Code Signing | 2.23.140.1.4.1. |
| S/MIME Mailbox Validated Legacy | 2.23.140.1.5.1.1. |
| S/MIME Mailbox Validated Multipurpose | 2.23.140.1.5.1.2. |
| S/MIME Mailbox Validated Strict | 2.23.140.1.5.1.3. |
| S/MIME Organization Validated Legacy | 2.23.140.1.5.2.1. |
| S/MIME Organization Validated Multipurpose | 2.23.140.1.5.2.2. |
| S/MIME Organization Validated Strict | 2.23.140.1.5.2.3. |
| S/MIME Sponsor Validated Legacy | 2.23.140.1.5.3.1. |
| S/MIME Sponsor Validated Multipurpose | 2.23.140.1.5.3.2. |
| S/MIME Sponsor Validated Strict | 2.23.140.1.5.3.3. |
| S/MIME Individual Validated Legacy | 2.23.140.1.5.4.1. |
| S/MIME Individual Validated Multipurpose | 2.23.140.1.5.4.2. |
| S/MIME Individual Validated Strict | 2.23.140.1.5.4.3. |
    
**3.1.16.** CAs may not have more than 2 OIDs applied to their root certificate.   

**3.1.17.** End-entity certificates that include a Basic Constraints extension in accordance with IETF RFC 5280 must have the cA field set to FALSE and the pathLenConstraint field must be absent.

**3.1.18.** A CA must technically constrain an OCSP responder such that the only EKU allowed is OCSP Signing.

**3.1.19.** A CA must be able to revoke a certificate to a specific date as requested by Microsoft.

**3.1.20.** Root Key Sizes must meet the following requirements: 

| Algorithm | All Uses Except for Code Signing and Time Stamping | Code Signing and Time Stamping Use |
| --- | --- | --- |
| Digest Algorithms |SHA2 (SHA256, SHA384, SHA512) | SHA2 (SHA256, SHA384, SHA512) |
| RSA | 2048 | 4096 (New roots only)|
| ECC / ECDSA | NIST P-256, P-384, P-521 | Not Supported |

**Please Note:** 
- Signatures using elliptical curve cryptography (ECC), such as ECDSA, aren't supported in Windows and newer Windows security features. Users utilizing these algorithms and certificates will face various errors and potential security risks. The Microsoft Trusted Root Program recommends that ECC/ECDSA certificates shouldn't be issued to subscribers due to this known incompatibility and risk.
- Code Signing does not support ECC or keys > 4096

 

### 3.2. Revocation Requirements

**3.2.1.** CAs must have a documented revocation policy and must have the ability to revoke any certificate it issues.
**3.2.2.** OCSP responder requirements:
    a.	Minimum validity of eight (8) hours; Maximum validity of seven (7) days; and
    b.	The next update must be available at least eight (8) hours before the current period expires. If the validity is more than 16 hours, then the next update must be available at ½ the validity period.
**3.2.3.** CRL recommendations when OCSP is not present:
    a.	Should contain Microsoft-specific extension 1.3.6.1.4.1.311.21.4 (Next CRL Publish).
    b.	New CRL should be available at the Next CRL Publish time.
    c.	Maximum size of the CRL file (either full CRL or partitioned CRL) should not exceed 10M.
    
    > [!Note]
    > The goal of section 3.C.3- CRL Recommendations when OCSP is not present is to provide coverage for end users in cases of mass revocation. 
    
**3.2.4.** The CA must not use the root certificate to issue end-entity certificates.
**3.2.5.** If a CA issues Code Signing certificates, it must use a Time Stamp Authority that complies with RFC 3161, "Internet X.509 Public Key Infrastructure Time-Stamp Protocol (TSP)."

### 3.3. Code Signing Root Certificate Requirements

**3.3.1.** Root certificates that support code signing use may be removed from distribution by the Program 10 years from the date of distribution of a replacement rollover root certificate or sooner, if requested by the CA. 
**3.3.2.** Root certificates that remain in distribution to support only code signing use beyond their algorithm security lifetime (e.g. RSA 1024  = 2014, RSA 2048 = 2030) may be set to 'disable' in a future release.

### 3.4. EKU Requirements

**3.4.1.** CAs must provide a business justification for all of the EKUs assigned to their root certificate. Justification may be in the form of public evidence of a current business of issuing certificates of a type or types, or a business plan demonstrating an intention to issue those certificates in the near term (within one year of root certificate distribution by the Program).

**3.4.2.** Microsoft will only enable the following EKUs:
    1.  Server Authentication =1.3.6.1.5.5.7.3.1
    2.  Client Authentication =1.3.6.1.5.5.7.3.2
    3.  Secure E-mail EKU=1.3.6.1.5.5.7.3.4
    4.  Time stamping EKU=1.3.6.1.5.5.7.3.8
    5.  Document Signing EKU=1.3.6.1.4.1.311.10.3.12
     -   This EKU is used for signing documents within Office. It isn't required for other document signing uses.
 

# 4. Audit requirements

## 4.1. General Requirements

Microsoft requires that every CA submit evidence of a Qualifying Audit on an annual basis for the CA and any nonlimited root within its Public Key Infrastructure (PKI) chain. A Qualifying Audit must meet the following five main requirements:

- The auditor must be qualified.
- The audit must be performed using the proper scope.
- The audit must be performed using the proper standard.
- The audit must be performed and the attestation letter must be issued within the proper time period.
- The auditor must complete and submit a Qualifying Attestation.

It's the responsibility of the CA to provide Microsoft with a Qualifying Attestation to the results of the audit and conformance to the Audit Requirements in a timely manner.

### 4.1.1 The Auditor's Qualifications

Microsoft considers an auditor to be a Qualified Auditor if they're an independent individual or company that is certified to perform certification authority audits by one of these three authorities: (1) WebTrust, (2) an ETSI Equivalent National Authority (published at [https://aka.ms/ena](https://aka.ms/ena)) or, (3) in the case of a Government CA, the government itself. (For more information on Government CAs, see [Government CA Requirements](#government-ca-requirements).)

If a CA chooses to obtain a WebTrust audit, Microsoft requires the CA to retain a WebTrust licensed auditor to perform the audit. The full list of WebTrust-licensed auditors is available at [https://aka.ms/webtrustauditors](https://aka.ms/webtrustauditors). If a CA chooses to obtain an ETSI-based audit, Microsoft requires the CA to retain an authorized entity by an Equivalent National Authority (or \"ENAs\"). A catalog of acceptable ENAs is based on the list at [https://aka.ms/ena](https://aka.ms/ena). If a CA is operated in a country that doesn't have an ETSI Equivalent National Authority, Microsoft accepts an audit performed by an auditor that is qualified under an Equivalent National Authority in the auditor's home country.

### 4.1.2 The Scope of the Audit

The scope of the audit must include all roots, nonlimited subroots, and cross-signed nonenrolled roots, under the root, except for subroots that are limited to a verified domain. The audit must also document the full PKI hierarchy. The final audit statements must be in a publicly accessible location and must contain the start and end dates of the audit period. In the case of a WebTrust audit, WebTrust seals must also be in a publicly accessible location.

### 4.1.3 Point-in-Time Readiness Assessments

Microsoft requires an audit prior to commencing commercial operations. For commercial CAs that haven't been operational as an issuer of certificates for 90 days or more, Microsoft accepts a point-in-time readiness audit conducted by a Qualified Auditor. If the CA uses a point-in-time readiness audit, Microsoft requires a follow-up audit
within 90 days after the CA issues its first certificate. A commercial CA already in our program applying for a new root to be included is exempt from the point-in-time and period-in-time audit requirement for the new roots. Rather, they should be up to date on audits for their existing roots in the program.

### 4.1.4 The Time Period Between the Assessment and the Auditor's Attestation

Microsoft requires that the CA obtain a conforming audit annually. To ensure that Microsoft has information that accurately reflects the current business practices of the CA, the attestation letter arising from the audit must be dated and received by Microsoft not more than three months from the ending date specified in the attestation letter.

### 4.1.5 Audit Attestation

Microsoft requires that each auditor complete and submit to Microsoft a Qualifying Attestation. A Qualifying Attestation requires that the auditor completes a Qualifying Attestation Letter.

Microsoft uses a tool to automatically parse audit letters to validate the accuracy of the Qualifying Attestation Letter. This tool is found in the Common Certification Authority Database (CCADB). Work with your auditor to make sure the Qualifying Attestation Letter fulfills the following requirements. If the audit letter fails in any of these categories, a mail is sent back to the CA asking them to update their audit letter.

#### 4.1.5.1. All Audit Letter Requirements 

- Audit letter must be written in English
- Audit letter must be in a "Text Searchable" PDF format.
- Audit letter must have the auditor's name in the audit letter as recorded in CCADB. 
- Audit letter must list either SHA1 thumbprint or SHA256 thumbprint of audited roots.
- Audit letter must list the date the audit letter was written.
- Audit letter must state the start and end dates of the period that was audited. Note this time period isn't the period the auditor was on-site.
- The audit letter must include the full name of the CA as recorded in CCADB.
- Audit letter must list the audit standards that were used during the audit. Reference WebTrust/ETSI guidelines or [https://aka.ms/auditreqs](https://aka.ms/auditreqs) and list the full name and version of the audit standards referenced.

#### 4.1.5.2. CAs submitting Webtrust audits

Audits conducted by certified WebTrust auditors must have their audit letters uploaded to [https://cert.webtrust.org](https://cert.webtrust.org/). 
    
#### 4.1.5.3. CAs submitting ETSI audits

- Audits conducted by certified ETSI auditors should have their audit letters uploaded to their auditor's website. If the auditor doesn't post on their website, the CA must provide the name and email of the auditor when submitting the audit letter. A Microsoft representative reaches out to the auditor to verify the authenticity of the letter. 
- CAs may submit audits with either the EN 319 411-2 or 411-2 policy. 

### 4.1.6 Audit Submission

To submit annual audits, refer to the CCADB instructions on how to create an audit case found here: <https://ccadb.org/cas/updates>.

If the CA is applying into the Root Store and isn't in the CCADB, they should email their audit attestation to msroot\@microsoft.com.

## 4.2 Acceptable Audit Standards

The Program accepts two types of audit standards: WebTrust and ETSI. For each of the EKUs on the left, Microsoft requires an audit that conforms to the standard marked.

#### 4.2.1. WebTrust Audits

| Criteria | WebTrust for CA v2.1 | SSL Baseline with Network Security v2.3 | Extended Validation SSL v1.6.2 | Extended Validation Code Signing v1.4.1 | Publicly Trusted Code Signing Certificates v1.0.1 | WebTrust Principles and Criteria for Certification Authorities – S/MIME |
| --- | --- | --- | --- | --- | --- | --- |
| Server Authentication (Non-EV) | X | X |  |  |  |
| Server Authentication (non-EV) and Client Authentication only | X | X |  |  |  |
| Server Authentication (EV) | X | X | X |  |  |
| Server Authentication (EV) and Client Authentication only | X | X | X |  |  |
| EV Code Signing | X |  |  | X |  |
| Non-EV Code Signing and Time stamping | X |  |  |  | X |
| Secured Email (S/MIME) | X |  |  |  |  | X |
| Client Authentication (without Server Authentication) | X |  |  |  |  |
| Document Signing | X |  |  |  |  |

#### 4.2.2. ETSI-Based Audits

Note 1: If a CA uses an ETSI-based audit, it must perform a **full** audit annually. Microsoft won't accept surveillance audits. 
Note 2: All ETSI audits statements must be audited against the CA/Browser Forum requirements and compliance with these requirements must be stated in the audit letter. The ACAB'c [https://acab-c.com](https://acab-c.com) has provided guidance that meets the Microsoft requirements. 

| Criteria | EN 319 411-1: DVCP, OVCP or PTC-BR policies | EN 319 411-1: EVCP policy | EN 319 411-2: QCP-w/QEVCP-w policy (based on EN 319 411-1, EVCP) | EN 319 411-1: LCP, NCP, NCP+ policies | EN 319 411-2: QCP-n, QCP-n-qscd, QCP-l, QCP-l-qscd policies (based on EN 319 411-1, NCP/NCP+) | ETSI EN 319 411-1, LCP, NCP, or NCP+ policies as amended by ETSI TS 119 411-6 or ETSI EN 319 411-2, QCP-n, QCP-I, QCP-n-qscd or QCP-I-qscd policies as amended by ETSI TS 411-6 |
| --- | --- | --- | --- | --- | --- |--- |
| Server Authentication (Non-EV) | X |  |  |  |  |  |
| Server Authentication (non-EV) and Client Authentication only | X |  |  |  |  |  |
| Server Authentication (EV) |  | X |  |  |  | 
| Server Authentication (EV) and Client Authentication only |  | X | X |  |  |  |
| EV Code Signing |  |  | X | X |  |  |
| Non-EV Code Signing and Time stamping |  |  |  | X | X |  |
| Secured Email (S/MIME) |  |  |  | X | X | X|
| Client Authentication (without Server Authentication) |  |  |  | X | X |  |
| Document Signing |  |  |  | X | X | |

## 4.2.3. Government CA Requirements

Government CAs might choose to either obtain the previously described WebTrust or ETSI-based audit(s) required of Commercial CAs, or to use an Equivalent Audit. If a Government CA chooses to obtain a WebTrust or ETSI-based audit, Microsoft will treat the Government CA as a Commercial CA. The Government CA can then operate without limiting the certificates it issues.

#### 4.2.3.1. Equivalent Audit Restrictions

If the Government CA chooses not to use a WebTrust or ETSI audit, it may obtain an Equivalent Audit. In an Equivalent Audit (\"EA\"), the Government CA selects a third-party to perform an audit. The audit has two purposes: (1) to demonstrate that the Government CA complies with local laws and regulations related to certificate authority operation, and (2) to demonstrate that the audit substantially complies with the relevant WebTrust or ETSI standard.

If a Government CA chooses to obtain an EA, Microsoft limits the scope of certificates that the Government CA might issue. Government CAs that issue server authentication certificates must limit the root to government-controlled domains. Governments must limit the issuance of any other certificates to ISO3166 country codes that the country has sovereign control over.

Government CAs must also accept and adopt the appropriate, CAB forum baseline requirements for CAs based on the type of certificates the root issues. However, the Program Requirements and Audit Requirements supersede those requirements in any aspect in which they are in conflict.

All Government CAs entering the Program are subject to the above EA requirements. All Government CAs that are part of the Program before June 1, 2015 will be subject to the previously described EA requirements immediately upon expiration of their then-current audit.

#### 4.2.3.2. Content of the Equivalent Audit Report

Microsoft requires all Government CAs that submit an EA to provide an attestation letter from the auditor that:

- Attests that the audit is issued by an independent agency, which is authorized by the Government CAs government to conduct the audit.
- Lists the Government CA's government's criteria for auditor qualification, and certifies that the auditor meets this criteria.
- Lists the particular statutes, rules, and/or regulations that the auditor assessed the Government CAs operations against.
- Certifies the Government CA's compliance with the requirements outlined in the named governing statutes, rules, and/or regulations.
- Provides information that describes how the statute's requirements are equivalent to the appropriate WebTrust or ETSI audits.
- Lists Certificate Authorities and third parties authorized by the Government CA to issue certificates on the Government CA's behalf within a certificate chain.
- Documents the full PKI hierarchy.
- Provides the start and end date of the audit period.

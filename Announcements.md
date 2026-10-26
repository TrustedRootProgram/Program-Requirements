# Announcements - Microsoft Trusted Root Certificate Program

Check here for official Trusted Root Program announcements and communications.

# October 26, 2026
# Microsoft Response to eMudhra Certificate Authority Key Compromise

Microsoft is aware of the compromise of private keys associated with eight eMudhra G3B/G3C subordinate Certificate Authorities (CAs), consisting of six TLS CAs and two Code Signing CAs. This is a third-party incident with eMudhra and not a compromise of Microsoft systems.

The affected keys were also used by cross-signed certificates, creating additional certificate paths using the same compromised key material.

Microsoft has taken the following actions to protect customers.

## Microsoft Mitigations

| Date | Platform | Version / Release | Action |
|---|---|---|---|
| October 20, 2026 | Windows | 2026.10 OOB | Microsoft published an out-of-band update to the Windows Disallowed Certificate Trust List (CTL), blocking the eight compromised CA keys by Subject Public Key Information (SPKI). Because the affected eMudhra certificates and cross-signed certificates share the same public keys, this protection applies to the identified certificate paths using the compromised key material. The update was published at 11:00 a.m. Pacific and distributed through the Windows CTL distribution infrastructure. |
| October 20, 2026 | Microsoft Edge / WebView2 | CRLSet_CRL_2026.10.20 (CRLSet component v20) | Microsoft published an emergency CRLSet update blocking the affected TLS CA keys. The update was released across Microsoft Edge channels and is distributed automatically through the Microsoft Edge component update mechanism. |

## Certificate Revocation

eMudhra has revoked the affected CA certificates. Certificates cross-signed using the compromised key material have also been revoked.

Microsoft's Windows and Microsoft Edge mitigations provide additional protection independent of CA-issued revocation by explicitly blocking the compromised key material.

## Customer Action and Verification

No action is required for Microsoft Edge or WebView2 customers to receive the CRLSet update. The update is distributed automatically through the Microsoft Edge component update mechanism.

Windows devices receiving Microsoft Certificate Trust List updates will automatically receive the applicable Disallowed CTL update.

Customers who want to verify that the updates have been received can use the following steps:

### Windows

From a Command Prompt, run:

```cmd
certutil -f -verifyCTL DisallowedWU | findstr SequenceNumber
```

The October 2026 out-of-band Disallowed CTL update containing the eMudhra mitigations has the following sequence number:

```text
SequenceNumber = 01dd5f6ca45c9d86 10/18/2026 6:53 PM
```

### Microsoft Edge

Navigate to `edge://components` in Microsoft Edge and locate the **CRLSet** component. The eMudhra mitigation was included in CRLSet component **2026.10.20**.

If the installed CRLSet has not yet updated, select **Check for update** on the CRLSet component to manually request the latest available version.

Microsoft continues to investigate the incident and will update this announcement if additional actions are taken.


# August 27, 2026
## Microsoft Launches Post-Quantum Cryptography TLS Pilot Roots
On August 27, 2026, Microsoft plans to launch seven post-quantum cryptography (PQC) pilot roots through the Microsoft Trusted Root Program.

The pilot will enable approved certificate authorities to test PQC-enabled TLS certificate hierarchies using ML-DSA-87. Testing will focus on interoperability, compatibility, and ecosystem readiness for server authentication.

For more information, please visit:[ PQC Pilot Program.md](https://github.com/TrustedRootProgram/Program-Requirements/blob/main/PQC%20Pilot%20Program.md)

### Pilot Roots
This release will add the following PQC roots (CA \ Root Certificate \ SHA-256 Thumbprint):

- ComSign \ ComSign Dev Root PQ CA \ 01AD5BE684509B24E9AAA5F20B67CA9534C7BD6E442F21DC68FAF91A201719D3
- DigiCert \ DigiCert PQC TLS PILOT MLDSA87 Root CA \ 28999F984E12FE25EDFF2472ACB17CA195A1C5DCD64BEE6F14D5DFC82DFFEBE6
- HARICA \ HARICA TLS ML Root CA 2026 - Pilot \ 14872608F2B05FA79583F19057CBE95DA8153D6DF201DBF3E449FA5E9414AFC6
- IdenTrust Services, LLC \ IdenTrust Pilot Root TLS ML-DSA CA 1 \ F6041FB4B500F2927B98BBAD9C60DF84960ECD2DF88DCF967E7F1D2C80FD56CC
- Sectigo \ Sectigo Pilot Server Authentication Root M27 \ D8156E234404B1424568B89A353F33080A33850F7AD270B8D6842F48074BD2AF
- Shanghai Electronic Certification Authority Co., Ltd. \ UniTrust Global TLS MLDSA Root R1 TEST \ DC742564D508EDF06FCBE7F681A3324C54D13DF4E5C5A9C00681DC3643F763D8
- SSL.com \ SSL.com TLS ML Root CA 2026 - Pilot \ 9474F424AB3D8E892C1EAEDED7BAD828DB13C11A4377604ADF79967E2B27962D

### Important Scope
These roots are intended only for controlled testing. They are not publicly trusted, must not be used for production or public-facing websites, and will not be added to CCADB or Certificate Transparency logs. This experimental pilot will help Microsoft and participating certificate authorities identify technical and operational barriers to PQC adoption. It is an important step toward improving cryptographic agility and preparing the certificate ecosystem for a post-quantum future.

### PQC Pilot Root Compatibility on Windows OS
Following the introduction of PQC pilot root certificates into the Microsoft Certificate Trust List (CTL) released on August 27, 2026, customers may experience ***certutil -verifyCTL*** failures on operating systems that do not support ML-DSA algorithms. This can result in errors such as NTE_BAD_ALGID (Bad Algorithm ID) when importing PQC pilot roots.

PQC pilot TLS certificate authentication using ML-DSA signature suites is currently supported only on Windows 11 systems with the July 28, 2026 updates: KB5101681 (OS Build 28000.2608) for version 26H1 and KB5101684 (OS Builds 26200.8973 and 26100.8973) for version 25H2. Support for Windows Server 2025 is planned for a future release.

Customers should ensure that the underlying operating system supports the PQC release before validating or processing CTLs that contain PQC pilot root certificates. Use of ***certutil -verifyCTL*** on unsupported or down-level operating system versions may result in failures when importing or validating PQC roots.

PQC pilot certificate functionality is supported only on the Windows versions listed above.

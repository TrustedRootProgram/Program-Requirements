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
| October 26, 2026 | Windows | October 26 out-of-band updates | Removed six eMudhra G3 root certificates and one AAA Certificate Services cross-sign from the Windows trust list. The updated trusted-root payload was distributed through the Windows CTL distribution infrastructure to devices receiving automatic CTL updates. See the [Windows 11 KB5134133 release notes](https://support.microsoft.com/en-us/servicing/os/windows-11/2026/10/kb5134133-windows-11-24h2-25h2-26h2-update) and [Windows Server 2025 KB5134137 release notes](https://support.microsoft.com/en-us/servicing/os/windows-server/2026/10/kb5134137-windows-server-2025-update).|
| October 27, 2026 | Microsoft Edge / WebView2 | PKI Metadata component (Version: 72.0.0.0). | Removed six eMudhra G3 root certificates and one AAA Certificate Services cross-sign. See the [Microsoft Edge Stable Channel release notes](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-relnote-stable-channel#announcements). |

## Certificate Revocation and Removal

eMudhra has revoked the affected CA certificates. Certificates cross-signed using the compromised key material have also been revoked. Microsoft's Windows and Microsoft Edge mitigations provide additional protection independent of CA-issued revocation by explicitly blocking the compromised key material.

Microsoft also made a separate decision to remove certificates associated with the affected hierarchies from its default trust lists. Microsoft released an out-of-band Windows update removing seven certificates associated with the affected hierarchies—six eMudhra G3 roots and one AAA Certificate Services cross-sign—from the Windows trust list. Microsoft removed the same seven certificates from the Microsoft Edge trust list on October 27. Once these changes reach a device, the removed certificates are no longer trusted by default through the respective trust lists. 

These removed certificates provided trust paths for the affected intermediates, including through cross-signing. In software that does not reliably check revocation or Microsoft’s disallowed-certificate list, retaining or locally restoring those trust paths could allow certificates associated with the compromised intermediates to validate. 

Revocation and removal are distinct actions. Revocation addresses the known affected intermediate CAs; removal is a broader decision about which certificates Microsoft trusts by default. Organizations with a specific compatibility need may choose to trust a certificate locally, subject to their own security assessment and policies, but should not restore trust in an affected hierarchy without understanding the associated risk.

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

## Revoked intermediate CA certificates

| Certificate | Issuer | SHA-256 fingerprint | Action |
|---|---|---|---|
| EM DV TLS CA - G3B | emSign Root TLS CA - G3 | `42C4ACCD12C4F59597925E1A08A7A90102608543809308D50EC427E118BA1493` | Revoked by eMudhra |
| EM DV TLS CA - G3B | AAA Certificate Services | `45A883F349AEDFD5F3A649B5498FFB121712BA8B448F3F2A91DBC5A766FCDDBE` | Cross-sign revoked by Sectigo |
| EM DV TLS CA - G3C | emSign Root TLS CA - G3 | `0164D7CEAE5BB909C272AF151FF44B1177AE9B47D9424B94F1D9558C30934D19` | Revoked by eMudhra |
| EM DV TLS CA - G3C | AAA Certificate Services | `62B7F9868263F72F6911FC78CEAF72C1979158B7368BF648683BB2AA39B02E72` | Cross-sign revoked by Sectigo |
| EM EV TLS CA - G3B | emSign Root TLS CA - G3 | `E7568FE6E12331F4FD7DE61DA4C7559D0F8EB192A218D4741A3BA75184333838` | Revoked by eMudhra |
| EM EV TLS CA - G3B | AAA Certificate Services | `579480AEA166290BD3C643589E795FC0D0E54E86505D180F1DFF99EFD3199512` | Cross-sign revoked by Sectigo |
| EM EV TLS CA - G3C | emSign Root TLS CA - G3 | `432EC25F0D28DE9006D97BF752F17BBB2CD41F669933FCB072D9A1148D0261F3` | Revoked by eMudhra |
| EM EV TLS CA - G3C | AAA Certificate Services | `FD9D5C2DBBD4995AB69B8D50C439D9527B00529199C2FD01B2174EB58F07021F` | Cross-sign revoked by Sectigo |
| EM OV TLS CA - G3B | emSign Root TLS CA - G3 | `98B896625C0C230ADEEC3EB2CF6AAD5001ECF9156A68644E82374CE5833BC25B` | Revoked by eMudhra |
| EM OV TLS CA - G3B | AAA Certificate Services | `5F1DED4DD590AF74631290CF073B122A2AAC6A1FA479778A0BD43579BD832699` | Cross-sign revoked by Sectigo |
| EM OV TLS CA - G3C | emSign Root TLS CA - G3 | `CB6E15165AC802E9B3F993F16C25D41F4E81C21EBDE71AE1B012AC00BF9C7C3F` | Revoked by eMudhra |
| EM OV TLS CA - G3C | AAA Certificate Services | `7485B51C0ED192878FA1D2F948FB529AE1842CC5086C4B67F7BE5B2039DE9489` | Cross-sign revoked by Sectigo |
| EM OV CS CA - G3B | emSign Root CS CA - G3 | `9E39DE2881273ACC225A149C72BA3E0F51424963669AB633EE1DC7DF5DB067B4` | Revoked by eMudhra |
| EM OV CS CA - G3B | AAA Certificate Services | `A496E23AC0CAB8155FC9B117B97EAE368EFCBB9041AEC8804D5A308D2D01C2D8` | Cross-sign revoked by Sectigo |
| EM OV CS CA - G3C | emSign Root CS CA - G3 | `4B2460A466F95FD40113BCDCCA2CEB29B3B093921DE45474DA7DF48874C630B1` | Revoked by eMudhra |
| EM OV CS CA - G3C | AAA Certificate Services | `84112972B8E59D14560AE7E7119654474AAD119990CF3722BFC1E3B91615E1FD` | Cross-sign revoked by Sectigo |

## Certificates removed from the Windows and Microsoft Edge trust lists

| Certificate | SHA-256 thumbprint | Action |
|---|---|---|
| emSign ECC Root CA - G3 | `86A1ECBA089C4A8D3BBE2734C612BA341D813E043CF9E8A862CD5C57A36BBE6B` | Removed from default trust lists |
| emSign Root Client Auth CA - G3 | `BBD8B3D745EFB79198D93B9C482B9D934537325729EA2F02C129261F91BE2E3D` | Removed from default trust lists |
| emSign Root CS CA - G3 | `F2EDAAFF3D9B701FB4D14C9F285F8C0BAD90FC3BCC1FA07D47F4718EDABA34A5` | Removed from default trust lists |
| emSign Root SMIME CA - G3 | `F76A0D440C418DC5B362BE8E11E0A5D06023F4396093E4F455827BF55153D8A4` | Removed from default trust lists |
| emSign Root TLS CA - G3 | `7DD78D5F4F13459A83DFF9ABBBA62EDBAF6F2D102BF257FD712F4D9F2746ED8D` | Removed from default trust lists |
| emSign Root TSA CA - G3 | `75D2CE75979CF2A43B172C9F89F733DDA2136031DB4BBF3698B053714C077155` | Removed from default trust lists |
| AAA Certificate Services (Sectigo) | `D7A7A0FB5D7E2731D771E9484EBCDEF71D5F0C3E0A2948782BC83EE0EA699EF4` | Removed from default trust lists |


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

---
title: November 2026 Deployment Notice - Microsoft Trusted Root Program
description: This document provides details about the changes made in November 2026 to the root store.
ms.date: 11/16/2026
ms.service: security
author: tahmad2
ms.author: tahminaahmad
ms.topic: conceptual
---

# November 2026 Microsoft Trusted Root Program deployment notice

On November 16, 2026, Microsoft released an update to the Microsoft Trusted Root Certificate Program, removing the remaining ten eMudhra root certificates from the Windows and Microsoft Edge trusted root lists.

Once these updates reach a device, the affected root certificates will no longer be trusted by default through the respective Microsoft trust lists. Certificates that depend on these roots for trust may no longer validate unless an alternative trusted certification path exists.

Organizations that rely on certificates issued under these hierarchies should assess potential impacts and transition to certificates chaining to trusted Certificate Authorities.

Organizations with specific compatibility requirements may choose to establish local trust, subject to their own security assessments and organizational policies. Microsoft recommends carefully evaluating the associated risks before doing so. For more information on how to do this, please see: [Manager Certificate Stores in Windows Server] (https://learn.microsoft.com/en-us/windows-server/identity/ad-cs/inspect-certificates-manage-certificate-stores).

This release will Remove the following roots (CA \ Root Certificate \ SHA-256 Thumbprint):

- eMudhra Inc \ emSign ECC Root CA - C3 \ BC4D809B15189D78DB3E1D8CF4F9726A795DA1643CA5F1358E1DDB0EDC0D7EB3
- eMudhra Inc \ emSign Root CA - C1 \ 125609AA301DA0A249B97A8239CB6A34216F44DCAC9F3954B14292F2E8C8608F
- eMudhra Inc \ emSign Root CA - C2 \ 46CD083B47E80402028DF493960EA19C85FE851950D5165F1C7DA4FAA951E2F8
- eMudhra Technologies Limited \ emSign Root CA - G1 \ 40F6AF0346A99AA1CD1D555A4E9CCE62C7F9634603EE406615833DC8C8D00367
- eMudhra Technologies Limited \ emSign Root CA - G2 \ 1AA0C2709E831BD6E3B5129A00BA41F7EEEF020872F1E6504BF0F6C3F24F3AF3
- eMudhra Technologies Limited \ emSign Root Client Auth CA - G1 \ 8ABFC40FAEAF13CBC8BB67B61C8D097A321CD2FEE047C54256927E0F8BFEADFD
- eMudhra Technologies Limited \ emSign Root CS CA - G2 \ 0D74EF67C88DE3560365E225AEF976F915E901347B73352D81AB5B4132BB2150
- eMudhra Technologies Limited \ emSign Root SMIME CA - G1 \ 47911BC8F32A11B029E0BB10A348B459404B87731B870A2F3FA97B4705DC4C25
- eMudhra Technologies Limited \ emSign Root TLS CA - G1 \ CEF71E70B7C29ADDF6C30CD19E614B38FD5F02A435A0EEDDD0087E183D101A51
- eMudhra Technologies Limited \ emSign Root TSA CA - G2 \ 1997770A5633FB6D0440ABF7D7E87E15D795F094F8C2959DADB00E785866BF48
-----------------------------------------------------------------

**Certificate Transparency Log Monitor (CTLM) policy** <br />

The Certificate Transparency Log Monitor (CTLM) policy is now included in the monthly Windows CTL. It's a list of publicly trusted logging servers that is for validating certificate transparency on Windows. The list of logging servers is expected to change over time as they're retired or replaced, and this list reflects the CT logging servers that Microsoft trusts. In the upcoming Windows release, users are able to opt in to certificate transparency validation, which will check for the presence of two Signed Certificate Timestamps (SCTs) from different logging servers in the CTLM. This functionality is currently being tested with event logging only to ensure it's reliable before individual applications can opt in to enforcement.

> [!NOTE]
> As part of this release, Microsoft also updated the Untrusted CTL time stamp and sequence number. No changes were made to the contents of the Untrusted CTL but this will cause your system to download/refresh the Untrusted CTL. This is a normal update that is sometimes done when the Trusted Root CTL is updated.
>
> * The update package is available for download and testing at: [https://aka.ms/CTLDownload](https://aka.ms/CTLDownload)
> * Signatures on the Certificate Trust Lists (CTLs) for the Microsoft Trusted Root Program changed from dual-signed (SHA-1/SHA-2) to SHA-2 only. No customer action required. For more information, please visit: [https://support.microsoft.com/help/4472027/2019-sha-2-code-signing-support-requirement-for-windows-and-wsus](https://support.microsoft.com/help/4472027/2019-sha-2-code-signing-support-requirement-for-windows-and-wsus)

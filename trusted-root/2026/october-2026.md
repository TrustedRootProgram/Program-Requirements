---
title: October 2026 Deployment Notice - Microsoft Trusted Root Program
description: This document provides details about the changes made in October 2026 to the root store.
ms.date: 10/20/2026
ms.service: security
author: tahmad2
ms.author: tahminaahmad
ms.topic: conceptual
---

# October 2026 Microsoft Trusted Root Program deployment notice

On October 20, 2026, Microsoft released an update to the Microsoft Trusted Root Certificate Program, due to the compromise of private keys associated with eight eMudhra G3B/G3C subordinate Certificate Authorities (CAs), consisting of six TLS CAs and two Code Signing CAs. This is a third-party incident with eMudhra and not a compromise of Microsoft systems.

The affected keys were also used by cross-signed certificates, creating additional certificate paths using the same compromised key material.

Microsoft has taken the following CTL related actions to protect customers; please see the announcements tab for further mitigations and updates.

This release will Remove the following roots (CA \ Root Certificate \ SHA-256 Thumbprint):

- eMudhra Technologies Limited \ emSign ECC Root CA - G3 \ 86A1ECBA089C4A8D3BBE2734C612BA341D813E043CF9E8A862CD5C57A36BBE6B
- eMudhra Technologies Limited \ emSign Root Client Auth CA - G3 \ BBD8B3D745EFB79198D93B9C482B9D934537325729EA2F02C129261F91BE2E3D
- eMudhra Technologies Limited \ emSign Root CS CA - G3 \ F2EDAAFF3D9B701FB4D14C9F285F8C0BAD90FC3BCC1FA07D47F4718EDABA34A5
- eMudhra Technologies Limited \ emSign Root SMIME CA - G3 \ F76A0D440C418DC5B362BE8E11E0A5D06023F4396093E4F455827BF55153D8A4
- eMudhra Technologies Limited \ emSign Root TLS CA - G3 \ 7DD78D5F4F13459A83DFF9ABBBA62EDBAF6F2D102BF257FD712F4D9F2746ED8D
- eMudhra Technologies Limited \ emSign Root TSA CA - G3 \ 75D2CE75979CF2A43B172C9F89F733DDA2136031DB4BBF3698B053714C077155
- Sectigo \ AAA Certificate Services \ D7A7A0FB5D7E2731D771E9484EBCDEF71D5F0C3E0A2948782BC83EE0EA699EF4

-----------------------------------------------------------------

**Certificate Transparency Log Monitor (CTLM) policy** <br />

The Certificate Transparency Log Monitor (CTLM) policy is now included in the monthly Windows CTL. It's a list of publicly trusted logging servers that is for validating certificate transparency on Windows. The list of logging servers is expected to change over time as they're retired or replaced, and this list reflects the CT logging servers that Microsoft trusts. In the upcoming Windows release, users are able to opt in to certificate transparency validation, which will check for the presence of two Signed Certificate Timestamps (SCTs) from different logging servers in the CTLM. This functionality is currently being tested with event logging only to ensure it's reliable before individual applications can opt in to enforcement.

> [!NOTE]
> As part of this release, Microsoft also updated the Untrusted CTL time stamp and sequence number. No changes were made to the contents of the Untrusted CTL but this will cause your system to download/refresh the Untrusted CTL. This is a normal update that is sometimes done when the Trusted Root CTL is updated.
>
> * The update package is available for download and testing at: [https://aka.ms/CTLDownload](https://aka.ms/CTLDownload)
> * Signatures on the Certificate Trust Lists (CTLs) for the Microsoft Trusted Root Program changed from dual-signed (SHA-1/SHA-2) to SHA-2 only. No customer action required. For more information, please visit: [https://support.microsoft.com/help/4472027/2019-sha-2-code-signing-support-requirement-for-windows-and-wsus](https://support.microsoft.com/help/4472027/2019-sha-2-code-signing-support-requirement-for-windows-and-wsus)

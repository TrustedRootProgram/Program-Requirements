---
title: June 2026 Deployment Notice - Microsoft Trusted Root Program 
description: This document provides details about the changes made in August 2025 to the root store.
date published: 6/30/2026
date updated: 6/30/2026
---


# June 2026 Microsoft Trusted Root Program deployment notice
<br>
On Tuesday, June 30, 2026, Microsoft will release an update to the Microsoft Trusted Root Certificate Program. 

This release will Add the following roots (CA \ Root Certificate \ SHA-1 Thumbprint):
- CA \ root(33EA1C) \ thumbprint   
<br>
-----------------------------------------------------------------


**Certificate Transparency Log Monitor (CTLM) policy** <br />
The Certificate Transparency Log Monitor (CTLM) policy is now included in the monthly Windows CTL. It's a list of publicly trusted logging servers that is for validating certificate transparency on Windows. The list of logging servers is expected to change over time as they're retired or replaced, and this list reflects the CT logging servers that Microsoft trusts. 
In the upcoming Windows release, users are able to opt in to certificate transparency validation, which will check for the presence of two Signed Certificate Timestamps (SCTs) from different logging servers in the CTLM. This functionality is currently being tested with event logging only to ensure it's reliable before individual applications can opt in to enforcement.

> [!NOTE]
> As part of this release, Microsoft also updated the Untrusted CTL time stamp and sequence number. No changes were made to the contents of the Untrusted CTL but this will cause your system to download/refresh the Untrusted CTL. This is a normal update that is sometimes done when the Trusted Root CTL is updated.
> 
> * The update package is available for download and testing at: [https://aka.ms/CTLDownload](https://aka.ms/CTLDownload)

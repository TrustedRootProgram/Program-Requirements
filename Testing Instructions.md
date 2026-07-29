---
title: Testing  - Microsoft Trusted Root Certificate Program
description: This document provides details about the changes made monthly to the root store.
ms.date: 02/15/2024
ms.service: security
author: kasirota
ms.author: kasirota
ms.topic: conceptual
---

# Testing Instruction - Microsoft Trusted Root Certificate Program

Before releasing a new Certificate Trust List (CTL) to production, Microsoft requests that Certificate Authorities who have requested additions or changes to the CTL validate that the changes they expect are present. Testing is also available to any users of the operating system. Changes are generally posted one week before the release on the test server. 

To achieve this, the user will need to make the following modifications to a PC running Windows: 


## Testing Configuration
1. Within the Windows registry, change [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\systemCertificates\AuthRoot\AutoUpdate] "RootDirUrl" to http://ctldl.windowsupdate.com/msdownload/update/v3/static/trustedr/en/test
2. HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SystemCertificates\AuthRoot\AutoUpdate\SyncFromDirUrl]
=http://ctldl.windowsupdate.com/msdownload/update/v3/static/trustedr/en/test


3. Delete the following registry keys
 * [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SystemCertificates\AuthRoot\AutoUpdate\EncodedCtl]
 * [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SystemCertificates\AuthRoot\AutoUpdate\LastSyncTime]
 * [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SystemCertificates\AuthRoot\Certificates] (deleting all cached certificates)

 

 
## Reset to Normal Configuration
1. Within the Windows registry, change [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\systemCertificates\AuthRoot\AutoUpdate] "RootDirUrl"  to http://ctldl.windowsupdate.com/msdownload/update/v3/static/trustedr/en (note it is the same without the test at the end)
2. [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SystemCertificates\AuthRoot\AutoUpdate\SyncFromDirUrl]
=http://ctldl.windowsupdate.com/msdownload/update/v3/static/trustedr/en


3. Delete the following registry keys
 * [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SystemCertificates\AuthRoot\AutoUpdate\EncodedCtl]
 * [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SystemCertificates\AuthRoot\AutoUpdate\LastSyncTime]
 * [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SystemCertificates\AuthRoot\Certificates] (deleting all cached certificates)
 
Please note, deleting these registry keys can also force an update of the CTL at any time. 

## Additional Testing + Expected Behaviors
Depending on what change has been made to your root (NotBefore, NotBefore EKU, Disable, Remove), testing will yield different results. 

### NotBefore
1. Issue a new certificate that chains to the root. When evaluated in an applicable validation scenario, the certificate should not be trusted. This state is not reflected in the user interface, including Certificate Manager or the certificate file view.
2.	Confirm that content signed before the NotBefore restriction remains valid and continues to function as expected.

### NotBefore by Enhanced Key Usage (EKU)
####	Client Authentication and Document Signing
   - Issue a new certificate that chains to the root. When evaluated for the restricted EKU in an applicable scenario, the certificate should not be trusted. This state is not reflected in the user interface, including Certificate Manager or the certificate file view.
   - Confirm that content signed before the EKU restriction remains valid and continues to function as expected.
####	Time Stamping and Code Signing
   - Issue a new certificate that chains to the root. When evaluated for the restricted EKU in an applicable scenario, the certificate should not be trusted. This state is not reflected in the user interface, including Certificate Manager or the certificate file view.
   - Sign a binary and then validate it. The signature should be reported as invalid.
   - Confirm that binaries signed before the EKU restriction remain valid and continue to function as expected.

###	Disable
- Validate the expected behavior of the certificate file under the disabled state. You may receive a message similar to this on the certificate file on your machine.

  <img width="228" height="313" alt="image" src="https://github.com/user-attachments/assets/fd6f5416-0913-4eea-af22-1e15247d92f7" />


### Remove
- Confirm that the root certificate is no longer visible in the CTL.
- Attempt to use an artifact or scenario that depends on the removed root. The resulting certificate chain should be reported as untrusted.


## Frequented Asked Questions
#### Why is the root certificate still visible in the CTL?
- The root certificate remains visible in the Certificate Trust List (CTL) during the NotBefore (Stage 1) and Disable (Stage 2) stages. It is no longer visible only if it reaches Remove (Stage 3, only for TLS roots).

#### Does the certutil -verifyctl AuthRoot command force the download of certificates?
- No. By default, the command displays the certificates without downloading them. Adding the -f option (certutil -verifyctl -f  authrootwu) forces the certificates to be downloaded.

#### Is HKLM\SOFTWARE\Microsoft\SystemCertificates\AuthRoot\Certificates the only registry location in which AuthRoot certificates are stored through CTL updates?
- Yes. This is the only registry location used for this purpose.


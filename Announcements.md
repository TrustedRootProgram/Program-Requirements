# Announcements - Microsoft Trusted Root Certificate Program

Check here for official Trusted Root Program announcements and communications.

# August 25, 2026
## Microsoft Launches Post-Quantum Cryptography TLS Pilot Roots
On August 25, 2026, Microsoft plans to launch seven post-quantum cryptography (PQC) pilot roots through the Microsoft Trusted Root Program.

The pilot will enable approved certificate authorities to test PQC-enabled TLS certificate hierarchies using ML-DSA-87. Testing will focus on interoperability, compatibility, and ecosystem readiness for server authentication.

For more information, please visit:[ PQC Pilot Program.md](https://github.com/TrustedRootProgram/Program-Requirements/blob/main/PQC%20Pilot%20Program.md)

## Pilot Roots
This release will add the following PQC roots (CA \ Root Certificate \ SHA-256 Thumbprint):

- ComSign \ ComSign Dev Root PQ CA \ 01AD5BE684509B24E9AAA5F20B67CA9534C7BD6E442F21DC68FAF91A201719D3
- DigiCert \ DigiCert PQC TLS PILOT MLDSA87 Root CA \ 28999F984E12FE25EDFF2472ACB17CA195A1C5DCD64BEE6F14D5DFC82DFFEBE6
- HARICA \ HARICA TLS ML Root CA 2026 - Pilot \ 14872608F2B05FA79583F19057CBE95DA8153D6DF201DBF3E449FA5E9414AFC6
- IdenTrust Services, LLC \ IdenTrust Pilot Root TLS ML-DSA CA 1 \ F6041FB4B500F2927B98BBAD9C60DF84960ECD2DF88DCF967E7F1D2C80FD56CC
- Sectigo \ Sectigo Pilot Server Authentication Root M27 \ D8156E234404B1424568B89A353F33080A33850F7AD270B8D6842F48074BD2AF
- Shanghai Electronic Certification Authority Co., Ltd. \ UniTrust Global TLS MLDSA Root R1 TEST \ DC742564D508EDF06FCBE7F681A3324C54D13DF4E5C5A9C00681DC3643F763D8
- SSL.com \ SSL.com TLS ML Root CA 2026 - Pilot \ 9474F424AB3D8E892C1EAEDED7BAD828DB13C11A4377604ADF79967E2B27962D

## Important Scope
These roots are intended only for controlled testing. They are not publicly trusted, must not be used for production or public-facing websites, and will not be added to CCADB or Certificate Transparency logs. This experimental pilot will help Microsoft and participating certificate authorities identify technical and operational barriers to PQC adoption. It is an important step toward improving cryptographic agility and preparing the certificate ecosystem for a post-quantum future.

# ATT&CK Mapping — SolarWinds (SUNBURST)

Each section maps directly to a stage in `attack-flow.md`. Technique IDs are from the official MITRE ATT&CK campaign entry C0024.

---

## Stage 1 — Supply Chain Injection

| ID        | Technique               | What APT29 did                                                          |
| --------- | ----------------------- | ----------------------------------------------------------------------- |
| T1195.002 | Supply Chain Compromise | Injected SUNBURST into the Orion build so it shipped as a normal update |
| T1553.002 | Code Signing            | SUNBURST was signed with SolarWinds' own valid certificate              |
| T1036.005 | Masquerading            | Malicious code lived inside a legitimate Orion DLL filename             |

---

## Stage 3 — Evasion and Activation

| ID        | Technique                     | What APT29 did                                                                 |
| --------- | ----------------------------- | ------------------------------------------------------------------------------ |
| T1057     | Process Discovery             | Scanned for security tools before activating; stayed dormant if any were found |
| T1562.001 | Disable or Modify Tools       | Disabled security monitoring services on compromised systems                   |
| T1562.002 | Disable Windows Event Logging | Used `AUDITPOL` to stop audit logs from being collected                        |
| T1070.006 | Timestomp                     | Modified backdoor file timestamps to match legitimate Windows files            |

---

## Stage 4 — Command and Control

| ID        | Technique           | What APT29 did                                                                          |
| --------- | ------------------- | --------------------------------------------------------------------------------------- |
| T1568     | Dynamic Resolution  | Used a DGA to generate subdomains of `avsvmcloud.com` for C2                            |
| T1071.001 | Web Protocols       | C2 traffic over HTTPS was made to mimic normal Orion network activity                   |
| T1665     | Hide Infrastructure | C2 hostnames matched the victim's own environment; VPN IPs matched the victim's country |

---

## Stage 5 — Second-Stage Payload

| ID        | Technique              | What APT29 did                                                                          |
| --------- | ---------------------- | --------------------------------------------------------------------------------------- |
| T1105     | Ingress Tool Transfer  | Downloaded TEARDROP and Cobalt Strike onto compromised hosts                            |
| T1140     | Deobfuscate/Decode     | TEARDROP decrypted a payload hidden inside a fake `.jpg` file and loaded it into memory |
| T1546.003 | WMI Event Subscription | Used WMI to auto-launch the backdoor at system boot for persistence                     |

---

## Stage 6 — Lateral Movement & Credential Theft

| ID        | Technique               | What APT29 did                                                                               |
| --------- | ----------------------- | -------------------------------------------------------------------------------------------- |
| T1078     | Valid Accounts          | Used stolen credentials — deliberately different ones for remote access vs. lateral movement |
| T1003.006 | DCSync                  | Replicated credential hashes from domain controllers                                         |
| T1558.003 | Kerberoasting           | Grabbed service account tickets and cracked them offline                                     |
| T1021.001 | Remote Desktop Protocol | Used RDP from public-facing systems to reach internal servers                                |
| T1059.001 | PowerShell              | Primary tool for running commands, moving laterally, and exfiltrating data                   |

---

## Stage 7 — Exfiltration

| ID        | Technique                            | What APT29 did                                                               |
| --------- | ------------------------------------ | ---------------------------------------------------------------------------- |
| T1114.002 | Remote Email Collection              | Collected emails from executives and IT staff via `New-MailboxExportRequest` |
| T1560.001 | Archive via Utility                  | Compressed stolen data into password-protected archives using 7-Zip          |
| T1048.002 | Exfiltration Over Encrypted Protocol | Exfiltrated data over HTTPS through the victim's own OWA server              |
| T1070.008 | Clear Mailbox Data                   | Cleaned up evidence by removing the export requests afterward                |

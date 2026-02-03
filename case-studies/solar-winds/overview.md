# Case Study 01 — SolarWinds (SUNBURST)

## Overview

**Incident name:** SUNBURST  
**Threat actor:** UNC2724 / Dark Halo (also attributed to a Russian state-sponsored group)  
**Timeline:** Roughly March–December 2020 (discovered December 2020)  
**Affected software:** SolarWinds Orion platform

## What happened

Attackers inserted malicious code into a routine software update for SolarWinds Orion, an IT monitoring tool used by thousands of organizations — including U.S. government agencies and major corporations. Machines that installed the update unknowingly gave the attacker persistent, trusted access into their networks.

The malicious component, named SUNBURST, was designed to blend in with normal Orion traffic. It lay dormant for up to two weeks after installation before activating, making it difficult to detect through standard monitoring.

## Why it matters

- **Supply chain attack:** The attacker didn't break into each victim directly. They compromised the software vendor, turning a trusted update into a weapon.
- **Scale:** Potentially 18,000+ organizations installed the update. Confirmed breaches included U.S. government agencies (Treasury, Commerce, State) and private companies.
- **Sophistication:** The malware was designed to evade detection — it mimicked legitimate network traffic and was compiled into a signed, legitimate software build.
- **MITRE ATT&CK relevance:** This incident touches on a wide range of tactics including Initial Access, Execution, Persistence, Defense Evasion, Command and Control, and Exfiltration.

## Key sources

- CISA Advisory AA20-280A
- Mandiant (FireEye) public incident reports
- Microsoft threat intelligence blog posts on SUNBURST
- SolarWinds official incident statements

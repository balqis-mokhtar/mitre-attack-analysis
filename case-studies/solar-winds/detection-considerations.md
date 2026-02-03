# Detection Considerations — SolarWinds (SUNBURST)

What signals could have caught this, and at which stage.

---

## Supply chain integrity

The build process itself was compromised. Monitoring for unexpected changes to compiled DLLs or anomalous activity during the build pipeline could have flagged SUNBURST before it was ever distributed.

## Unusual outbound DNS

SUNBURST communicated via DNS queries to randomly generated subdomains. Monitoring for high volumes of DNS queries to unusual or new domains — especially ones using DGA patterns — is a standard detection signal for this type of C2.

## Network traffic anomalies

The C2 traffic was designed to look like normal Orion activity, but it still went to external infrastructure. Baselining what normal Orion traffic looks like and alerting on deviations could have helped.

## Credential misuse

APT29 used stolen credentials to move laterally — but they deliberately used different credentials for remote access vs. internal movement. Alerting on credentials being used from unusual locations or at unusual times would have been useful here.

## Audit log gaps

APT29 disabled Windows event logging using `AUDITPOL`. Any gap or failure in audit log collection should trigger an alert — missing logs are themselves a red flag.

## Known tool usage

Tools like Cobalt Strike, Mimikatz, and AdFind were used. While these are legitimate tools, their presence in an environment — especially together — is worth investigating.

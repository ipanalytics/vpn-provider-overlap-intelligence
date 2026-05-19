# Safe Interpretation

This project publishes infrastructure relationship signals. It does not publish a complete VPN IP database and does not make ownership or misconduct claims.

## Do

- Treat exact-IP overlap as a strong technical signal.
- Treat `/24` and ASN overlap as supporting context.
- Combine these signals with freshness, source quality, and provider-specific evidence.
- Use the data for enrichment, research, and prioritization.

## Do Not

- Do not block entire ASNs because they appear in this dataset.
- Do not label every IP in a shared `/24` as VPN.
- Do not infer common ownership from overlap alone.
- Do not claim a provider is compromised because it uses common hosting infrastructure.
- Do not treat absence from this dataset as proof that an IP is not VPN.

## Suggested Language

Use:

- "shared infrastructure signal"
- "observed exact-IP overlap"
- "hosting dependency"
- "provider relationship candidate"
- "requires IP-level confirmation"

Avoid:

- "same owner"
- "malicious ASN"
- "spy infrastructure"
- "all IPs are VPN"
- "confirmed relationship" without additional evidence

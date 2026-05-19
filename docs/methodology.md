# Methodology

This analysis uses aggregate VPN infrastructure observations and intentionally avoids publishing full raw IP lists.

## Inputs

The source dataset contains normalized VPN records with provider name, IP, ASN, ASN organization, country, city, network, source name, and confidence.

Generic proxy-only attribution and Tor are excluded from provider-overlap scoring because they are different signals and would dominate the overlap tables with noise.

## Evidence Layers

### Exact shared IP

A strong signal. The same exact IP appears under more than one VPN provider name.

This can indicate shared backend infrastructure, reseller platforms, white-label systems, provider migrations, or stale source artifacts.

### Shared `/24`

A medium signal. Providers appear in the same `/24` prefix. This does not mean they share a server. It means they share a small network block or nearby hosting footprint.

### Shared ASN / hosting org

A context signal. Providers use the same network operator. This is useful for concentration analysis but weak for direct relationship claims.

### Hosting dependency

For each provider, records are grouped by ASN organization. The top-host share shows how much of a provider's observed footprint depends on its largest hosting org.

### Independence score

A heuristic score based on distribution across hosting organizations and ASNs, penalized by top-host concentration.

High score means the provider appears more distributed. Low score means the observed footprint is concentrated in a small number of hosting operators.

## Limitations

- Public datasets and provider sources can contain stale records.
- IP geolocation and ASN registration do not prove physical location.
- Shared infrastructure does not prove common ownership.
- Some provider names may be aliases or brand variants.
- The dataset is a snapshot, not a permanent truth.

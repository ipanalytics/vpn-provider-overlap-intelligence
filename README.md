# VPN Provider Overlap Intelligence

Public aggregate analysis of VPN provider infrastructure relationships.

This repository does **not** publish raw VPN IP lists. It publishes aggregate signals that can help researchers understand when VPN brands appear to share backend infrastructure, hosting operators, or network footprints.

The analysis is designed for defensive research, fraud/risk feature engineering, source-quality review, and VPN/proxy detection methodology.

## What This Is

VPN brands often market themselves as independent services, but the infrastructure layer can be less independent than the brand layer. This project looks at observable infrastructure relationships using several evidence layers:

| Evidence Layer | Strength | Meaning |
|---|---:|---|
| Exact shared IP | Strong | The same IP was observed under multiple VPN provider names. |
| Shared `/24` prefix | Medium | Providers appear in the same small network block, without publishing raw IPs. |
| Shared ASN / hosting org | Context | Providers use the same network operator or hosting footprint. |
| Provider concentration | Context | A provider depends heavily on one hosting operator or is broadly distributed. |
| Relationship cluster | Derived | Providers connected by repeated exact-IP overlap. |

## What This Is Not

This is not a blocklist. It is not a claim of common ownership, malicious behavior, provider compromise, or affiliation.

Shared infrastructure can happen for many ordinary reasons:

- reseller or white-label VPN platforms;
- common hosting providers;
- provider migrations;
- reused IP pools;
- public source artifacts;
- stale or duplicated source names.

Use this as an enrichment signal, not as final attribution.

## Key Findings From This Snapshot

### Strong exact-IP overlap cluster

The strongest observed cluster is:

```text
Anonine, BoxPN, EasyHideIP, Froot, FrootVPN
```

This cluster has high exact-IP overlap across many ASNs and `/24` prefixes. It is a strong infrastructure-overlap signal, but it should not be interpreted as proof of ownership.

### Top provider pairs by exact shared IPs

| Provider A | Provider B | Score | Confidence | Shared Exact IPs | Shared /24 | Shared ASNs |
|---|---|---:|---|---:|---:|---:|
| Anonine | BoxPN | 100 | high | 290 | 56 | 31 |
| Anonine | EasyHideIP | 100 | high | 285 | 55 | 30 |
| Anonine | FrootVPN | 100 | high | 285 | 55 | 30 |
| BoxPN | EasyHideIP | 100 | high | 285 | 55 | 30 |
| BoxPN | FrootVPN | 100 | high | 285 | 55 | 30 |
| EasyHideIP | FrootVPN | 100 | high | 285 | 55 | 30 |
| Ivacy | PureVPN | 79 | high | 27 | 20 | 9 |
| Getflix | Smartdnsproxy | 65 | medium | 18 | 18 | 15 |
| GhostPath | SlickVPN | 56 | medium | 11 | 11 | 10 |

### Top hosting footprints

| Hosting / ASN Org | Unique VPN IPs | Providers | Top Providers |
|---|---:|---:|---|
| CDNEXT | 5,282 | 21 | NordVPN, CyberGhost, ProtonVPN, Windscribe, Astrill |
| M247 | 4,709 | 50 | NordVPN, CyberGhost, AirVPN, ProtonVPN, TorGuard |
| NETPROTECT-62651 | 3,190 | 3 | WLVPN, IPVanish, StrongVPN |
| CLOUVIDER Clouvider - Global ASN | 2,844 | 10 | NordVPN, WLVPN, IPVanish, Astrill |
| PACKETHUBSA-AS-AP PacketHub S.A. | 2,186 | 1 | NordVPN |

## Data Files

| File | Description |
|---|---|
| [`data/provider_pair_exact_overlap.csv`](data/provider_pair_exact_overlap.csv) | Provider-pair relationship scores based on exact shared IPs, shared `/24`, and shared ASNs. |
| [`data/provider_relationship_clusters.csv`](data/provider_relationship_clusters.csv) | Provider clusters connected by repeated exact-IP overlap. |
| [`data/shared_prefix_examples.csv`](data/shared_prefix_examples.csv) | Safe `/24` examples where 3+ VPN provider names overlap. No raw IPs. |
| [`data/provider_hosting_dependency.csv`](data/provider_hosting_dependency.csv) | Per-provider dependency on hosting / ASN organizations. |
| [`data/hosting_company_footprint.csv`](data/hosting_company_footprint.csv) | Hosting organizations ranked by VPN IP footprint and provider count. |
| [`data/provider_independence_score.csv`](data/provider_independence_score.csv) | Provider distribution and concentration score. |

## Relationship Score

The public score is a bounded heuristic, not a legal or ownership conclusion.

Signals used:

- exact shared IP count;
- shared `/24` prefix count;
- shared ASN count.

Confidence levels:

| Confidence | Meaning |
|---|---|
| high | Strong repeated exact-IP evidence. |
| medium | Meaningful overlap, but needs additional context. |
| low | Weak signal; useful only for investigation. |

## Safe Use

Good uses:

- VPN/proxy detection enrichment;
- provider clustering research;
- risk feature engineering;
- source quality review;
- identifying infrastructure concentration.

Bad uses:

- blocking an entire ASN;
- claiming common ownership from overlap alone;
- labeling every IP in a `/24` as VPN;
- using old overlap without freshness checks;
- treating this as a complete VPN database.

## Methodology

See [`docs/methodology.md`](docs/methodology.md).

## Safe Interpretation Notes

See [`docs/safe_interpretation.md`](docs/safe_interpretation.md).

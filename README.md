# VPN Provider Overlap Intelligence


<p align="center">
  <a href="LICENSE">
    <img src="https://img.shields.io/badge/license-CC%20BY--NC%204.0-blue" alt="License">
  </a>

  <a href="https://github.com/ipanalytics/vpn-provider-overlap-intelligence">
    <img src="https://img.shields.io/github/last-commit/ipanalytics/vpn-provider-overlap-intelligence" alt="Last Commit">
  </a>
  <a href="https://github.com/ipanalytics/vpn-provider-overlap-intelligence">
    <img src="https://img.shields.io/badge/dataset-active-success" alt="Dataset">
  </a>
  <a href="https://github.com/ipanalytics/vpn-provider-overlap-intelligence">
    <img src="https://img.shields.io/badge/focus-provider_overlap-informational" alt="Focus">
  </a>
  <a href="https://github.com/ipanalytics/vpn-provider-overlap-intelligence">
    <img src="https://img.shields.io/badge/exports-csv-informational" alt="Exports">
  </a>
</p>

---

VPN Provider Overlap Intelligence is a public aggregate dataset for analyzing shared VPN infrastructure patterns across providers, hosting operators, ASNs, and network ranges.

The project focuses on infrastructure overlap signals derived from observed VPN network footprints, including exact shared IP observations, shared `/24` prefixes, hosting concentration, and provider relationship clustering.

The repository intentionally avoids publishing raw VPN IP inventories.

---

## Overview

VPN providers frequently depend on overlapping infrastructure ecosystems:

* shared hosting providers
* leased datacenter ranges
* reseller platforms
* recycled address pools
* common backend operators

This repository analyzes observable overlap relationships and publishes aggregate signals suitable for:

* fraud detection
* VPN/proxy research
* infrastructure clustering
* IP reputation enrichment
* source quality analysis
* risk feature engineering

The project is designed for analytical and defensive workflows rather than enforcement automation.

---

## Evidence Model

Relationship analysis combines multiple independent infrastructure signals.

| Evidence Layer        | Strength | Description                                           |
| --------------------- | -------: | ----------------------------------------------------- |
| Exact shared IP       |   Strong | Same IP observed under multiple provider identities   |
| Shared `/24`          |   Medium | Providers overlap inside the same small network block |
| Shared ASN            |  Context | Providers share hosting/operator footprint            |
| Hosting concentration |  Context | Provider dependence on infrastructure operators       |
| Relationship cluster  |  Derived | Repeated overlap across providers and networks        |

The public score is heuristic and bounded. It is not an ownership assertion.

---

## Architecture

```text id="jlwm31"
             VPN Infrastructure Sources
                          │
       ┌──────────────────┼──────────────────┐
       │                  │                  │
       ▼                  ▼                  ▼
   IP Observations    ASN Enrichment    Prefix Analysis
       │                  │                  │
       └──────────────────┴─────────┬────────┘
                                    ▼
                         Relationship Engine
                 exact IP /24 / ASN correlation
                                    ▼
                           Cluster Analysis
                                    ▼
                              CSV Exports
```

---

## Key Snapshot Findings

### Strong Exact-IP Overlap Cluster

```text id="jlwm32"
Anonine, BoxPN, EasyHideIP, Froot, FrootVPN
```

This cluster shows repeated exact-IP overlap across multiple ASNs and network ranges.

The signal indicates strong infrastructure relationship evidence, but should not be interpreted as definitive ownership attribution.

---

## Top Provider Pairs

| Provider A | Provider B    | Score | Confidence | Shared Exact IPs | Shared `/24` | Shared ASNs |
| ---------- | ------------- | ----: | ---------- | ---------------: | -----------: | ----------: |
| Anonine    | BoxPN         |   100 | high       |              290 |           56 |          31 |
| Anonine    | EasyHideIP    |   100 | high       |              285 |           55 |          30 |
| Anonine    | FrootVPN      |   100 | high       |              285 |           55 |          30 |
| BoxPN      | EasyHideIP    |   100 | high       |              285 |           55 |          30 |
| BoxPN      | FrootVPN      |   100 | high       |              285 |           55 |          30 |
| EasyHideIP | FrootVPN      |   100 | high       |              285 |           55 |          30 |
| Ivacy      | PureVPN       |    79 | high       |               27 |           20 |           9 |
| Getflix    | Smartdnsproxy |    65 | medium     |               18 |           18 |          15 |
| GhostPath  | SlickVPN      |    56 | medium     |               11 |           11 |          10 |

---

## Top Hosting Footprints

| Hosting Organization | VPN IPs | Providers | Example Providers              |
| -------------------- | ------: | --------: | ------------------------------ |
| CDNEXT               |   5,282 |        21 | NordVPN, CyberGhost, ProtonVPN |
| M247                 |   4,709 |        50 | NordVPN, AirVPN, ProtonVPN     |
| NETPROTECT-62651     |   3,190 |         3 | WLVPN, IPVanish, StrongVPN     |
| CLOUVIDER            |   2,844 |        10 | NordVPN, Astrill, IPVanish     |
| PACKETHUBSA-AS-AP    |   2,186 |         1 | NordVPN                        |

---

## Published Datasets

| File                                 | Description                                      |
| ------------------------------------ | ------------------------------------------------ |
| `provider_pair_exact_overlap.csv`    | Provider overlap relationship scores             |
| `provider_relationship_clusters.csv` | Multi-provider overlap clusters                  |
| `shared_prefix_examples.csv`         | `/24` overlap examples without raw IP disclosure |
| `provider_hosting_dependency.csv`    | Per-provider hosting concentration               |
| `hosting_company_footprint.csv`      | Hosting footprint rankings                       |
| `provider_independence_score.csv`    | Infrastructure concentration metrics             |

---

## Relationship Scoring

The scoring model combines:

* exact shared IP counts
* shared `/24` counts
* shared ASN counts

### Confidence Levels

| Confidence | Meaning                              |
| ---------- | ------------------------------------ |
| `high`     | Repeated strong exact-IP overlap     |
| `medium`   | Meaningful overlap requiring context |
| `low`      | Weak or sparse overlap signal        |

Scores are intended for analytical weighting, not binary classification.

---

## Usage Examples

### Download overlap scores

```bash id="jlwm33"
curl -fsSLO \
  https://raw.githubusercontent.com/ipanalytics/vpn-provider-overlap-intelligence/main/data/provider_pair_exact_overlap.csv
```

### Extract high-confidence provider pairs

```bash id="jlwm34"
awk -F, '$4 == "high" { print }' \
  provider_pair_exact_overlap.csv
```

### Find infrastructure clusters

```bash id="jlwm35"
grep -i "NordVPN" \
  provider_relationship_clusters.csv
```

### Analyze hosting concentration

```bash id="jlwm36"
sort -t, -k2 -nr \
  hosting_company_footprint.csv | head
```

---

## Operational Use Cases

| Domain           | Example                              |
| ---------------- | ------------------------------------ |
| Fraud Detection  | VPN infrastructure correlation       |
| SIEM Enrichment  | Provider relationship context        |
| Threat Hunting   | Shared-hosting analysis              |
| Research         | VPN ecosystem mapping                |
| Abuse Prevention | Infrastructure concentration signals |
| Analytics        | Hosting dependency analysis          |

---

## Safe Interpretation

Infrastructure overlap alone does not imply:

* common ownership
* provider compromise
* malicious activity
* operational coordination

Shared infrastructure can result from:

* reseller platforms
* datacenter reuse
* leased address pools
* provider migrations
* stale upstream datasets
* white-label VPN ecosystems

The datasets should be treated as contextual infrastructure signals.

---

## Methodology

Additional methodology details:

```text id="jlwm37"
docs/methodology.md
```

Safe interpretation guidance:

```text id="jlwm38"
docs/safe_interpretation.md
```

---

## Design Goals

* aggregate-only publication
* infrastructure-focused analysis
* no raw VPN endpoint disclosure
* lightweight CSV exports
* reproducible overlap analysis
* operationally safe enrichment signals

---

## Not Intended For

The project is not intended for:

* ASN-wide blocking
* ownership attribution
* legal/compliance conclusions
* standalone VPN detection
* automated enforcement without additional telemetry

---

## Repository Layout

```text id="jlwm39"
.
├── data/
├── docs/
├── scripts/
├── LICENSE
└── README.md
```

---

## Roadmap

Planned additions:

* temporal overlap analysis
* ASN historical trends
* IPv6 overlap support
* confidence weighting improvements
* provider alias normalization
* infrastructure lineage tracking

---

## License

Licensed under CC BY-NC 4.0.

See [`LICENSE`](./LICENSE).

---

## Disclaimer

This repository publishes aggregate infrastructure overlap signals derived from observed VPN network patterns. The datasets are intended for analytical, operational, and defensive research workflows and should not be treated as definitive attribution evidence.

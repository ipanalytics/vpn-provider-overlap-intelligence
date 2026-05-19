# VPN Provider Infrastructure Overlap

This is a small public sample from IPAnalytics showing VPN brands that share exact observed exit IPs.

It does **not** claim common ownership, malicious behavior, or affiliation between providers. Shared IPs can happen because of reseller platforms, white-label VPN infrastructure, provider migrations, shared hosting pools, or stale source artifacts.

Raw IP addresses are intentionally not published here. The examples use provider-pair counts and `/24` prefixes only.

## Files

| File | Description |
|---|---|
| `vpn_provider_overlap_pairs_public.csv` | Provider pairs with exact shared IP counts. |
| `vpn_shared_prefix_examples_public.csv` | Masked `/24` examples where 3+ VPN brands overlap. |

## Method

The analysis starts from IPs observed under more than one VPN provider name. Generic proxy-only attribution and Tor are excluded from this public view because they are different signals and add noise to VPN-provider overlap analysis.

For each shared IP, provider pairs are generated. The final table counts:

- exact shared IPs between provider pairs;
- number of ASNs where the overlap appears;
- a top ASN organization for context;
- sample shared `/24` prefixes, without publishing exact IPs.

## Top Provider Pairs

| Provider A | Provider B | Shared Exact IPs | Shared ASNs | Top ASN Org |
|---|---|---:|---:|---|
| Anonine | BoxPN | 290 | 31 | M247 |
| Anonine | EasyHideIP | 285 | 30 | M247 |
| Anonine | FrootVPN | 285 | 30 | M247 |
| BoxPN | EasyHideIP | 285 | 30 | M247 |
| BoxPN | FrootVPN | 285 | 30 | M247 |
| EasyHideIP | FrootVPN | 285 | 30 | M247 |
| Ivacy | PureVPN | 27 | 9 | CDNEXT |
| Froot | FrootVPN | 21 | 10 | GLESYS glesys.com |
| Getflix | Smartdnsproxy | 18 | 15 | AS-VULTR |
| Sentinel dVPN | TorGuard | 17 | 5 | M247 |
| GhostPath | SlickVPN | 11 | 10 | UK2NET-AS |

## Likely Infrastructure Clusters

Clusters below connect provider pairs that share at least 5 exact IPs.

| Cluster | Providers | Pair Shared-IP Sum | Shared ASNs |
|---:|---|---:|---:|
| 1 | Anonine, BoxPN, EasyHideIP, Froot, FrootVPN | 1766 | 32 |
| 2 | Ivacy, PureVPN | 27 | 9 |
| 3 | Getflix, Smartdnsproxy | 18 | 15 |
| 4 | Sentinel dVPN, TorGuard | 17 | 5 |
| 5 | GhostPath, SlickVPN | 11 | 10 |

## Safe Interpretation

- Large exact-IP overlaps are strong infrastructure-overlap signals.
- Small overlaps are weaker and may come from migrations, stale data, temporary reuse, or source noise.
- This is not a blocklist.
- This does not mean every IP in the ASN or `/24` is a VPN.
- This does not prove shared ownership.
- IP-level freshness and source quality still matter.

## Why This Is Useful

VPN detection is not just a list of IPs. Provider overlap can reveal when several VPN brands depend on the same backend infrastructure, reseller platform, or hosting footprint.

This helps with:

- VPN/proxy detection research;
- provider clustering;
- source quality review;
- fraud/risk feature engineering;
- identifying white-label or reseller infrastructure patterns.

## Related Project

https://github.com/ipanalytics/ASN-VPN-Network-Intelligence

# Gateway Selection – Evaluation Criteria

> Gateways below are anonymised (A, B, C) and scores are **illustrative**. In a real engagement I would replace them with vendor demos, sandbox testing and commercial quotes.

## Criteria and weights
| Criterion | Weight | What I'd check |
|-----------|--------|----------------|
| Payment method coverage | 20% | UPI, cards, netbanking, wallets, EMI/pay-later |
| WooCommerce / WordPress support | 15% | Maintained official plugin, hooks, documentation |
| Reliability and success rates | 15% | Uptime SLA, bank-level success rates, retry features |
| Pricing and settlement | 15% | MDR per method, settlement cycle (T+1 / T+2), hidden fees |
| Security and compliance | 15% | PCI DSS level, tokenisation, hosted checkout (keeps UrbanLoom at the simplest PCI scope) |
| Refunds, webhooks and APIs | 10% | Partial refunds, webhook signing, idempotency, sandbox quality |
| Reporting and reconciliation | 10% | Settlement reports, downloadable exports, API access |

## Illustrative scoring (1–5)
| Criterion | Weight | Gateway A | Gateway B | Gateway C |
|-----------|--------|-----------|-----------|-----------|
| Payment methods | 20% | 5 | 4 | 4 |
| WooCommerce support | 15% | 5 | 4 | 3 |
| Reliability | 15% | 4 | 4 | 3 |
| Pricing and settlement | 15% | 3 | 4 | 5 |
| Security and compliance | 15% | 5 | 5 | 4 |
| Refunds / webhooks / APIs | 10% | 5 | 4 | 3 |
| Reporting | 10% | 4 | 3 | 3 |
| **Weighted score** | 100% | **4.40** | **4.05** | **3.65** |

Weighted score = Σ (weight × score). Example for Gateway A: 0.20×5 + 0.15×5 + 0.15×4 + 0.15×3 + 0.15×5 + 0.10×5 + 0.10×4 = 4.40.

**Recommendation (illustrative):** Gateway A, with a sandbox pilot of the top two before commitment. The decision should be validated with Finance on pricing and settlement terms.

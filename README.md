# Payment Gateway Integration for E-commerce – Business Analysis Project

> **Disclaimer:** Independent project. *UrbanLoom* is a fictional company. Figures, interviews and gateway scores are assumed for demonstration and do not represent any real vendor's performance.

## 1. Scenario
**UrbanLoom** is a fictional direct-to-consumer home-décor brand selling through a WordPress/WooCommerce store (about 2,500 orders/month). Payments currently run through a basic redirect plugin with these issues:

1. **Checkout failures:** 14% of payment attempts fail and customers rarely retry.
2. **Order mismatches:** some orders stay "Pending payment" even though money was debited.
3. **Manual refunds:** staff process refunds by logging in to the gateway dashboard separately.
4. **Weak reconciliation:** finance matches settlements to orders by hand.

UrbanLoom wants to integrate a more capable payment gateway supporting UPI, cards, netbanking and wallets with reliable order-status handling.

## 2. My role
Business Analyst: gateway evaluation criteria, requirements, flows, status mapping, test cases and go-live readiness.

## 3. Business objectives (assumed baselines)
| ID | Objective | Baseline | Target |
|----|-----------|----------|--------|
| BO-1 | Increase payment success rate | 86% | 94% |
| BO-2 | Eliminate "paid but pending" orders | ~40 / month | under 3 / month |
| BO-3 | Cut refund processing effort | 15 min per refund, manual | under 2 min, from the admin panel |
| BO-4 | Speed up finance reconciliation | 2 days / month-end | same day, automated report |

## 4. Scope
**In scope:** gateway evaluation, checkout payment methods, order and payment status handling, webhooks, failure/retry, refunds, notifications, reconciliation report, admin visibility, testing and go-live checklist.
**Out of scope:** subscriptions, marketplace split payments, international currencies, loyalty points.

## 5. Deliverables
| File | Description |
|------|-------------|
| [01-gateway-selection.md](01-gateway-selection.md) | Evaluation criteria and weighted scoring |
| [02-brd.md](02-brd.md) | Business Requirements Document |
| [03-user-stories.md](03-user-stories.md) | User stories with acceptance criteria |
| [04-process-flows.md](04-process-flows.md) | Checkout, webhook, failure and refund flows |
| [05-status-mapping-and-error-handling.md](05-status-mapping-and-error-handling.md) | Gateway to order status mapping, error handling |
| [06-uat-and-traceability.md](06-uat-and-traceability.md) | UAT cases, RTM, go-live checklist, risks |

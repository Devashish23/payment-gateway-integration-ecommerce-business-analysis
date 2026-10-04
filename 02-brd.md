# Business Requirements Document – UrbanLoom Payment Gateway Integration

| Field | Value |
|-------|-------|
| Version | 1.0 (Draft) |
| Author | Devashish Kale, Business Analyst |
| Sponsor | Head of E-commerce (fictional) |

## 1. Purpose
Specify requirements for integrating a payment gateway into the UrbanLoom WooCommerce store so customers can pay reliably and the business can track, refund and reconcile payments.

## 2. Stakeholders
| Stakeholder | Interest |
|-------------|----------|
| Head of E-commerce (sponsor) | Higher conversion, fewer abandoned checkouts |
| Finance Manager | Accurate settlement and reconciliation |
| Customer Support Lead | Fewer "I paid but no order" tickets; easy refunds |
| WordPress Developer | Clear integration spec and error cases |
| QA Tester | Testable criteria |
| Customer | Fast, safe checkout with preferred payment method |
| Gateway account manager | Go-live approval, technical support |

## 3. Business rules
| ID | Rule |
|----|------|
| BR-01 | An order is created with status *Pending payment* before the customer is sent to pay, and is confirmed only after a verified success from the gateway. |
| BR-02 | Payment success is confirmed by the **server-side webhook**, not only by the browser redirect. |
| BR-03 | A pending order with no payment result after 30 minutes is checked against the gateway and, if unpaid, set to *Failed/Cancelled* and stock is released. |
| BR-04 | A refund cannot exceed the amount captured less previous refunds. |
| BR-05 | Card details are never stored or processed on UrbanLoom servers (hosted checkout). |
| BR-06 | Each order has a single payment reference; duplicate webhook events must not create duplicate state changes. |

## 4. Functional requirements
| ID | Requirement | Priority |
|----|-------------|----------|
| FR-01 | Offer UPI, credit/debit cards, netbanking and wallets at checkout through the gateway's hosted page or secure overlay. | Must |
| FR-02 | Create the order and a gateway payment order (amount, currency, order reference) before payment starts (BR-01). | Must |
| FR-03 | Receive and verify the gateway webhook (signature check) and update the order status (BR-02, BR-06). | Must |
| FR-04 | Verify the payment signature on the customer return/callback and show the correct success or failure page. | Must |
| FR-05 | On failure or abandonment, show the reason in plain language and let the customer retry with another method without re-entering the cart. | Must |
| FR-06 | Auto-expire unpaid pending orders after 30 minutes and release stock (BR-03). | Must |
| FR-07 | Allow admin to issue full or partial refunds from the order screen, calling the gateway refund API and updating the order notes (BR-04). | Must |
| FR-08 | Send customer emails/SMS for payment success, failure, and refund initiated/completed. | Must |
| FR-09 | Generate a daily reconciliation report matching orders to gateway settlements, with an exceptions list. | Must |
| FR-10 | Log all gateway requests, responses and webhook events with order reference for troubleshooting. | Should |
| FR-11 | Save cards with the gateway's tokenisation for returning customers (explicit consent). | Could |
| FR-12 | Provide a sandbox/test mode toggle and go-live checklist. | Must |

## 5. Non-functional requirements
| ID | Category | Requirement |
|----|----------|-------------|
| NFR-01 | Security | HTTPS everywhere; webhook secret stored securely; API keys not exposed to the front end. |
| NFR-02 | Compliance | Hosted checkout so PCI scope stays minimal; follow gateway and RBI guidelines. |
| NFR-03 | Performance | Redirect to payment page in under 3 seconds; webhook processed in under 5 seconds. |
| NFR-04 | Reliability | Webhook handler is idempotent and retried safely; no lost updates if the gateway retries. |
| NFR-05 | Usability | Mobile-first checkout (about 70% of traffic is mobile, assumed). |
| NFR-06 | Auditability | Payment and refund events retained for at least 12 months. |

## 6. Assumptions and dependencies
- Gateway merchant account approved (KYC and business documents complete).
- Store is on WooCommerce with a maintained gateway plugin or a custom integration.
- Finance defines settlement and refund policy (timelines communicated to customers).

## 7. Constraints
- 8-week delivery; go-live before the festive season sale (assumed).
- Small team: one developer, one QA.

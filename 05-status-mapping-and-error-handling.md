# Status Mapping and Error Handling

Gateway status names vary by vendor; the table uses generic terms.

## Gateway payment status to order status
| Gateway event / status | Meaning | Order status | Customer message | Stock |
|------------------------|---------|--------------|------------------|-------|
| Created | Payment order created, not paid | Pending payment | (payment page shown) | Reserved |
| Authorized / Captured | Payment successful | Processing | "Order confirmed" email | Reduced |
| Failed | Bank/customer failure | Pending payment (retry allowed) | Failure reason and Retry | Reserved up to 30 min |
| Pending (e.g. UPI awaiting approval) | Awaiting customer or bank | Pending payment | "Payment is being processed" | Reserved |
| Expired / Abandoned (30 min) | No success | Cancelled | "Order cancelled, retry anytime" | Released |
| Refund initiated | Refund requested | Processing (note added) | "Refund initiated" email | – |
| Refund processed | Refund completed | Refunded / Partially refunded | "Refund completed" email | Restocked if returned |
| Dispute / chargeback | Bank-initiated reversal | On hold, flagged | Internal alert only | – |

## Error scenarios
| Scenario | System behaviour |
|----------|------------------|
| Customer closes browser after paying | Webhook confirms the order; email sent |
| Webhook arrives before browser return | Order confirmed once; callback shows result without re-processing |
| Webhook delivered twice | Second event ignored (idempotency on event ID) |
| Invalid webhook signature | Rejected with 4xx, logged, alert to admin |
| Amount mismatch (paid ≠ order total) | Order placed On hold; finance alert |
| Gateway API timeout at order creation | Show friendly error, no duplicate order; retry allowed |
| Duplicate payment on one order | Flag and queue refund of the duplicate |
| Bank downtime | Show method-specific message and suggest another method |
| Refund API failure | Error shown, event logged, admin can retry |
